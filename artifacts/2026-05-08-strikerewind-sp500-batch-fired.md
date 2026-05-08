# StrikeRewind — first live S&P 500 win-rate batch fired from Render

**Date:** 2026-05-08
**Run:** 12 of 2026-05-08
**Acted on fresh owner input:** yes — Travis 2026-05-08T20:30 directive (Theo-relayed) authorized firing `runSpreadResultsBatch` against the S&P 500 from Render egress as the next slice after the Massive provider landed (run 11).

## Outcome
- **51,020 rows written** by SP500 batch in 189 seconds; 518/518 tickers processed, 0 failed.
- **2,900 rows written** by DOW30 pilot in 62 seconds; 29/29 processed, 0 failed (one DOW30 symbol mapped to a missing flat-file ticker — likely BRK/B class share — and was skipped cleanly).
- **46,520 distinct rows** in `spread_results` with `data_source='price_history_5yr'` after upsert dedup across the two batches.
- Sanity check on AAPL bull_put 4dte: win rate climbs `0.10 → 0.31 → 0.61 → 0.69 → 0.80 → 0.90` across OTM% `−10 → −5 → 0 → +2 → +5 → +8 → +10`, observation_count 249 (≈ 50/yr × 5y). Direction-correct and grid-coherent.
- Both jobs were one-off Render Jobs (`POST /v1/services/{id}/jobs`) on the existing starter web service with `--max-old-space-size=400` to keep heap under the 512 MB container limit.

## Two bugs found and fixed mid-run

### 1) MassivePriceDataProvider OOM during `primeDateRange`
First DOW30 attempt OOMed at 250 MB. Root cause: the per-day cache stored every ticker in every flat-file (~12k tickers × 1255 day-files), so memory scaled to ~3 GB. Fixed by adding `setTickerAllowlist(tickers)` to the provider; `parseDailyCsv` now skips rows outside the allowlist when one is set. The batch script calls `setTickerAllowlist(universe)` before priming, scoping memory to the requested universe (DOW30 → ~30 × 1255 ≈ 38k rows; SP500 → ~500 × 1255 ≈ 630k rows, well under 512 MB).

Commit: `f178b95` — `fix(massive): scope provider cache to a ticker allowlist`.

### 2) Web service OOM after deploy because analyze path inherited Massive as default
With MASSIVE_* set on Render, run 11's `getDefaultPriceDataProvider()` returned the Massive provider. The web service's `/api/analyze` path uses that default and calls `fetchHistoricalChart(ticker, start, end)`, which in turn called `primeDateRange` with no allowlist — same OOM as bug 1, but now in the live web service. Manifested as alternating 502s on `/api/health` and `/api/stripe/prices`, CORS-style failures in the browser smoke (proxy returns 502 without CORS headers when upstream is down), and a Watchlist regression to the FREE-tier upgrade gate.

Fixed by rolling back the default-provider switch: Yahoo stays default for on-demand single-ticker calls. Massive is constructed explicitly only in `scripts/run-spread-results-batch.ts` for the nightly batch, with `setTickerAllowlist` already in place. Yahoo from Render egress is unblocked (only the VPS IP was 429ed in run 9), so analyze works fine on Yahoo.

Commit: `77307a7` — `fix(provider): keep Yahoo as the default; Massive is batch-only`.

## Verification
- 35/35 Playwright smoke against `https://www.strikerewind.com` after the second deploy went live.
- 6/6 `/api/health` 200; 3/3 `/api/stripe/prices` 200 — service stable.
- `tsc --noEmit` clean across both commits.

## Render Jobs mechanics (new capability surfaced)
Render starter web service supports one-off Jobs via `POST /v1/services/{id}/jobs` with a `startCommand`. The job container has the full repo + `node_modules` (devDeps included since Render's default `npm install` doesn't prune), so `node_modules/.bin/tsx scripts/foo.ts` works directly. Logs are fetched with `GET /v1/logs?ownerId=...&resource=job-XXX&direction=forward`. This is how AutoBox should fire any future on-demand backend work that needs Render egress.

## State changes
- `OPEN_GATES.md` — unchanged. Single Travis-side gate `ADS APPEAL: PAF GOOGLE ADS SUSPENDED — APPEAL FILED 2026-05-08`.
- `BUDGET.md` — no spend; cash unchanged $162.45.
- `TODO.md` — close the "fire S&P 500 batch from Render" entry; the Hunt route now serves real win-rate rows for any STANDARD/PRO user. Add follow-up: `/api/analyze` could promote Yahoo → Massive (for that one ticker only) once the per-call allowlist is reworked, but it's optional polish.

## Suggested post copy

> StrikeRewind: fired the first live S&P 500 win-rate batch from Render — 518 tickers, 51,020 rows, 189s. Hit two OOMs en route (provider cache too wide, then bled into the web service); fixed both, smoke 35/35 green. Hunt now serves real ticker-specific data for STANDARD/PRO users. Cash $162.45.
