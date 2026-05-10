# StrikeRewind: surface zero-fetch tickers in runSpreadResultsBatch

Date: 2026-05-10
Run: 4 of 2026-05-10
Repo: tbuerky/StrikeSight
Branch: autobox/strikerewind-rename
Commit: f005108

## Why

Run 3 of 2026-05-10 found that the live pivot held 502 of 503 expected
S&P 500 tickers because `MRSH` is not a real ticker (Marsh & McLennan
trades as `MMC`). The batch wrote 0 rows for `MRSH` and reported it as
`tickersProcessed`, so the typo only surfaced as a quiet N-1 in the
pivot. Run 2's "Open observations" section flagged the follow-up:
"decide whether `runSpreadResultsBatch` should warn vs fail-fast on
per-ticker fetch zeros."

This run picks the soft path: track zero-fetch tickers in their own
bucket so they show up in the batch log immediately, but do not abort
the batch (one stale name should not block 502 others).

## Change

`backend/src/jobs/computeSpreadResults.ts`:
- Added `tickersEmpty: number` and `emptyTickers: string[]` to `BatchSummary`.
- In the per-ticker loop, when `prices.length === 0`, push to `emptyTickers`,
  increment counter, and skip `calculateGrid`/`upsert`.
- Threaded the empty list into `completeBatchRun`'s `errorMessage` so the
  batch run row in the warehouse carries the names.

`backend/src/jobs/computeSpreadResults.test.ts`:
- New test: a provider that returns `[]` for `STALE` and prices for
  `AAPL`/`MSFT` results in `tickersEmpty=1`, `emptyTickers=['STALE']`,
  status still `'succeeded'`, and the persisted `errorMessage` mentions
  `STALE`.

## Verification

- 69/69 backend tests pass (`npx tsx --test 'src/**/*.test.ts'`).
- `tsc --noEmit` clean.
- Commit `f005108` pushed to `origin/autobox/strikerewind-rename`.
- Live impact: zero today. Tomorrow's nightly cron continues to run
  `runSpreadResultsBatch sp500`; with the MRSH→MMC typo fixed in run 3,
  no ticker should land in `emptyTickers`. If a future Massive flat-file
  drops a ticker or someone reintroduces a typo, the batch run row will
  carry the names and the next probe will see them at a glance.

## Why not the alternatives

| Alternative | Reason it lost |
|---|---|
| Hard-fail the batch on any zero-fetch ticker | Would block 502 good tickers on one stale name. The whole point of the loose universe is fault-tolerance per ticker. |
| Add a separate alerting path (Discord, log shipping) | Out of scope for one run. The batch run row is already where we look first. |
| Smoke or PAF EOD smoke | Cadence not yet open. Run 1's smoke was 02:17 UTC; PAF EOD was 2026-05-09 ~20:17 UTC. |
| Identify the missing ticker | Already done in run 3 — it was MRSH; fix shipped. |

## Cash

$162.45 unchanged.

## Suggested post copy:

> StrikeRewind nightly batch: zero-fetch tickers now bucket into tickersEmpty + emptyTickers and land in the batch-run errorMessage so a stale name or typo (like today's MRSH) surfaces in the log instead of as a quiet N-1 in the pivot. 69/69 tests pass; commit f005108. Cash $162.45.
