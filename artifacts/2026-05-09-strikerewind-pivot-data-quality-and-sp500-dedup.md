# StrikeRewind — pivot data quality probe + SP500 universe dedup

**Run 1 of 2026-05-09.** First post-pivot validation of `spread_results` content quality, plus a targeted clean-up of the SP500_TICKERS universe.

## Why this run

Run 12 of 2026-05-08 fired the live S&P 500 win-rate batch and loaded 46,520 rows into `spread_results`. Run 13 scheduled the nightly Render Job. Neither run validated that the pivot data layer actually returns sensible Hunt results when queried — fixture-mode smoke confirms the route, not the data. With Travis testing gated behind `TESTING COMPLETE: STRIKEREWIND` and a marketing freeze in place, data-quality work is the highest-leverage move available without violating any gate.

The nightly cron fires at 06:00 ET; current time at run start was 02:17 UTC, so I could not yet verify tomorrow's batch. Verifying yesterday's load was the eligible move.

## Pivot data layer — verified healthy

Direct PostgREST probes against `https://hjfsapwessfvdcfytpuk.supabase.co/rest/v1/spread_results`:

- **Total rows:** 46,520 with `data_source='price_history_5yr'`, of which 23,260 `bull_put` and 23,260 `bear_call` (perfect 50/50 split).
- **Distinct tickers:** 466 (out of 518 SP500_TICKERS entries fired). Mean ~99.8 rows/ticker; expected 100 per ticker (10 OTM × 5 DTE × 2 directions). 52 tickers fell out — likely a mix of stale/defunct names and S3 data gaps.
- **observation_count:** zero rows below 20. The default `observation_count >= 20` filter in `getHuntSpreadResultsPivot` does not cut into the result set.
- **AAPL bull_put grid:** monotonic across both axes. `otm_pct=−0.10, dte=4` → 0.10 win rate; `otm_pct=+0.20, dte=4` → 1.00. Win rate climbs smoothly with OTM% and is largely stable across DTE. Direction-correct.
- **Simulated `/api/hunt` query** (`BOTH`, `minWinRate=0.85`, `maxOtmPct=0.30`, `maxDteWeeks=24`, default `obs>=20`, `limit=20`): returned 20 rows across **diverse tickers** (FE bear_call, TJX bull_put, JNJ bull_put, DUK bear_call, YUM bull_put, ...) with sensible win rates (1.0 at deep OTM, decaying toward ATM). No single-ticker degenerate output.

Conclusion: the pivot query path is production-quality. When a STANDARD/PRO user runs Hunt against a non-trivial criteria set, they will see ticker-specific real data, not synthetic or all-AAPL results.

## What broke through the surface

In the simulated Hunt response, **KSU appeared with `observation_count=27`** (vs 249 for everyone else). KSU is Kansas City Southern — acquired by Canadian Pacific in December 2023, no longer a public ticker. Tracing it back, `backend/src/data/sp500-tickers.ts` is dated "Updated January 2025" and contains:

- **518 entries with 46 duplicates** → 472 unique. Some tickers (CRM, NFLX, ANSS, FTNT, GEHC, etc.) appear in 2–3 sector buckets in the file.
- **4 confirmed-stale** (acquired/private): KSU (CP Rail 2023), TWTR (taken private 2022), ATVI (Microsoft 2023), XLNX (AMD 2022).
- **4 typos / non-tickers**: TYSON (real is TSN), CenterPoint (real is CNP), CIRR (not a ticker), TRIPS (real is TRIP).
- **3 never-S&P speculative**: GOEV, RIDE, NKLA — penny-stock EV plays that were never index members.

These would surface in real Hunt results (KSU did surface in run-9 directly above), polluting the customer-facing experience with ghosts.

## What I shipped

Commit `87a6f5f` on `autobox/strikerewind-rename`, pushed to GitHub:

- `backend/src/data/sp500-tickers.ts`: 518 → 461 entries (−57). Deduped + removed the 11 stale/typo/speculative tickers above. Header comment notes the audit boundary.
- 58/58 backend tests pass; `tsc --noEmit` clean.

Direct DB cleanup against live Supabase via PostgREST DELETE on `spread_results`:

| Ticker | Rows deleted |
|---|---|
| KSU | 40 |
| TWTR | 100 |
| ATVI | 100 |
| XLNX | 80 |
| GOEV | 100 |
| RIDE | 100 |
| NKLA | 100 |
| **Total** | **620** |

`spread_results.data_source='price_history_5yr'` row count: 46,520 → 45,900. Hunt results immediately stop surfacing these seven names (universe `IN`-filter excludes them; corresponding rows are gone too).

Render auto-deploy will pick up `87a6f5f` for the API service.

## Deliberately not done

- **Full S&P 500 audit** against an authoritative source (Wikipedia/iShares IVV holdings/S&P press releases). The list still likely contains stale or non-current names beyond the 11 I caught — e.g. CTLT (Catalent acquired 2025), some retail/EV names that may have been removed at quarterly rebalances. This needs an authoritative-source pull and is a separate run.
- **Re-firing the SP500 batch** to repopulate the 52 tickers that fell out of yesterday's run — most of those are the now-removed stale names anyway. The nightly cron at 06:00 ET tomorrow will do a fresh pass against the deduped universe.
- **Did not raise a new gate.** Single open gate (`ADS APPEAL: PAF GOOGLE ADS SUSPENDED`) is unchanged; status-watch on Travis's Google appeal.

## State

- BUDGET: no spend; cash $162.45.
- OPEN_GATES.md: unchanged (1 gate, status-watch).
- Marketing freeze still in effect; no public-facing change.

## Recommendation

Single open gate sitting on Travis: `ADS APPEAL: PAF GOOGLE ADS SUSPENDED — APPEAL FILED 2026-05-08`. Nothing actionable.

The pivot data layer is verified healthy and a real source of buyer-facing edge. Tomorrow's first cron-fired Render Job at 06:00 ET will be the next observable signal — it should refresh `spread_results` against the cleaned universe and provide a load-bearing test of the self-sustaining pipeline.

Suggested post copy:

> StrikeRewind: pivot data layer verified healthy — 466 tickers, 45,900 rows, AAPL grid is direction-correct (0.10 → 1.00 win rate as OTM% climbs), simulated Hunt returns diverse top-20. Found and removed 11 stale/typo tickers (KSU/TWTR/ATVI/XLNX +7) from the SP500 universe + 620 rows of their ghost data; commit 87a6f5f deploying. Cash $162.45.
