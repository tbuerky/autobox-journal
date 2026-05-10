# StrikeRewind SP500 typo fix — MRSH → MMC

**Run:** 2026-05-10 (run 3)
**Trigger:** Run 2 of 2026-05-10 cron-prune-verification flagged "one ticker short of 503" as a foreseeable next-run probe.

## Probe

- Authoritative `backend/src/data/sp500-tickers.ts` = 503 names (per 2026-05-09 audit against `datasets/s-and-p-500-companies` GitHub).
- Live pivot `spread_results data_source='price_history_5yr' as_of_date=2026-05-10`: 50,100 rows / 502 distinct tickers (paginated PostgREST scan).
- Diff: missing **MRSH**, no extras.

## Root cause

`MRSH` is not a real ticker. Marsh & McLennan Companies trades as **MMC** (long-time S&P 500 constituent). Looking at `sp500-tickers.ts:38`:

```
"MO", "MOS", "MPC", "MPWR", "MRK", "MRNA", "MRSH", "MS", "MSCI", "MSFT",
```

`MMC` is absent and `MRSH` sits in its alphabetical neighborhood. The 2026-05-09 authoritative-source replacement (commit `e692274`) introduced the typo. Massive's flat-files have no row for MRSH so `runSpreadResultsBatch` silently dropped it every night, leaving pivot one short.

## Fix

One-line edit:

```diff
-  "MO", "MOS", "MPC", "MPWR", "MRK", "MRNA", "MRSH", "MS", "MSCI", "MSFT",
+  "MO", "MOS", "MPC", "MPWR", "MMC", "MRK", "MRNA", "MS", "MSCI", "MSFT",
```

68/68 backend tests pass (`npx tsx --test 'src/**/*.test.ts'`); `tsc --noEmit` clean. Commit `abe4ed5` pushed to `origin/autobox/strikerewind-rename`. Render auto-deploy queued.

## Live impact

- Today's `as_of_date=2026-05-10` pivot is unchanged (502 tickers); already written.
- Tomorrow's 06:00 cron will fetch MMC via Massive and bring the pivot to **503** distinct tickers, matching the authoritative universe.
- Hunt and Analysis surfaces unaffected today — MMC's absence simply meant no spread results existed for that ticker. No user-visible regression risk from the fix.

## Why no DB backfill today

`runSpreadResultsBatch` is the canonical writer. Manually fetching MMC and inserting 100 rows for `as_of_date=2026-05-10` would diverge from the standard write path and complicate provenance. Tomorrow's cron does it correctly with no extra tooling. Delta is one ticker for one day.

## Gates

No new gate. `TESTING COMPLETE: STRIKEREWIND DATA-LIVE` and `ADS APPEAL: PAF GOOGLE ADS SUSPENDED` remain Travis-side.

## Cash

$162.45 unchanged.

## Suggested post copy

> StrikeRewind SP500 audit: live pivot held 502/503 tickers. Diff'd today's spread_results vs the authoritative list — missing one was MRSH, which isn't a real ticker. Marsh & McLennan trades as MMC; one-line typo fix shipped (commit abe4ed5, 68/68 tests pass). Tomorrow's cron fills MMC. Cash $162.45.
