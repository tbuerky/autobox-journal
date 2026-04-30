# StrikeRewind — `SpreadResultsService` shim shipped

**Date:** 2026-04-30
**Branch:** `autobox/strikerewind-rename`
**Commit:** `756d687`
**Files:** `backend/src/services/spreadResultsService.ts` (new, 122 lines), `backend/src/services/spreadResultsService.test.ts` (new, 123 lines), `backend/src/services/supabaseDatabaseService.ts` (+110 lines)
**Tests:** 12/12 pass (was 3/3) — 9 new `node:test` cases on the pure helpers

## What this is

Step #1 of the post-warehouse-migration build queue: a typed service in
front of the `spread_results` / `batch_runs` tables added by
`backend/supabase-migration-spread-results.sql` (commit `2a7698c`,
awaiting Travis to apply the SQL via the dashboard).

This is the read/write shim every downstream consumer will go through —
the nightly Polygon batch (write path) and Hunt / Ticker Analysis /
Watchlist top-signal (read paths).

## Why now (no approval needed)

- The migration SQL is in the repo. The next step in the latest HANDOFF
  recommendation list is exactly this shim. Whether Travis applies the
  SQL today or next week, the service code is small enough to write
  ahead-of-time, type-check, and unit-test with pure helpers; the only
  thing the migration unlocks is *running* the DB calls.
- Both top-priority owner gates remain open
  (`APPROVED: DEPLOY ON VERCEL+RENDER STARTER, $7/MO`,
  `APPROVED: STRIKEREWIND TIER COPY + LIMITS PRE-DEPLOY`). Building
  this service while waiting does not require approval, does not
  change the deploy candidate's behavior (no read-path repoint), and
  prepares the next autonomous run (wiring `schedulerService` to write
  nightly snapshots once Polygon is approved).

## What ships

### `SpreadResultsService` (singleton)
Matches `WatchlistServiceDB.getInstance()` pattern. Methods:

| Method | Purpose |
|---|---|
| `upsertResults(rows)` | Bulk write from the nightly batch; returns rows-affected count |
| `upsertFromAnalysis(result, asOfDate, dataSource)` | Convenience: flattens an `AnalysisResult` and upserts in one call |
| `getHuntResults({ spreadType, analysisYears, limit, asOfDate? })` | Hunt read path; sorted by `as_of_date DESC, ev_percent DESC`; supports `'BOTH'` |
| `getTickerMatrix(ticker, analysisYears, asOfDate?)` | Ticker Analysis read path |
| `getTopSignalForTickers(tickers, analysisYears, asOfDate?)` | Watchlist top-signal-per-ticker; returns `Map<ticker, row>` |
| `recordBatchRun(runType, metadata?)` | Returns the new `batch_runs.id` for the nightly job to update on completion |
| `completeBatchRun(id, { status, tickersTotal, tickersProcessed, rowsWritten, errorMessage })` | Closes a batch run row |

### Pure helpers (testable, no I/O)

- `analysisToWarehouseRows(result, asOfDate, dataSource)` — flattens
  every `StrategyMatrixCell` on an `AnalysisResult` into one warehouse
  row. Rounds `win_rate` / `ev_percent` to 2 decimals, `premium` to 4
  decimals, `current_price` / `iv_rank` to 2 decimals — matches the
  schema column scales so float drift never overflows the `NUMERIC(...)`
  precision. Throws if `analysisYears` is not in `(1, 2, 3, 5)` to mirror
  the SQL `CHECK` constraint and fail fast at write time.
- `pickTopSignalPerTicker(rows)` — groups by ticker
  (case-insensitive), returns the highest-`ev_percent` row each.

### `SupabaseDatabaseService` additions
Six new methods following the existing `getWatchlist` / `addToWatchlist`
pattern so the `supabase` client stays private:
`upsertSpreadResults`, `getHuntSpreadResults`, `getTickerSpreadMatrix`,
`getTopSpreadSignalsByTickers`, `recordBatchRunStart`,
`recordBatchRunComplete`. Each method maps to one of the indexes from
the migration:

- `getHuntSpreadResults` — uses `spread_results_hunt_idx`
  `(as_of_date DESC, analysis_years, spread_type, ev_percent DESC)`
- `getTickerSpreadMatrix` — uses `spread_results_ticker_idx`
  `(ticker, as_of_date DESC, analysis_years)`
- `getTopSpreadSignalsByTickers` — uses `spread_results_watchlist_idx`
  `(ticker, as_of_date DESC, ev_percent DESC)`

Upsert uses
`onConflict: 'ticker,spread_type,otm_percentage,timeframe_weeks,analysis_years,as_of_date'`
which matches the `UNIQUE` constraint in the migration — every nightly
batch run is naturally idempotent.

### Exported `SpreadResultRow` interface
On `SupabaseDatabaseService`, mirrors the SQL row shape with
TypeScript-narrowed `spread_type: 'PUT' | 'CALL'` and
`analysis_years: 1 | 2 | 3 | 5`.

## What this deliberately does NOT do

- No read-path repoint. `Hunt.tsx` / `Analysis.tsx` / `Watchlist.tsx`
  still go through the existing `analysis_cache` / `hunt_cache` flow.
- No nightly job wiring. `schedulerService.ts` is unchanged. Wiring it
  to write to the warehouse is gated on `APPROVED: SUBSCRIBE POLYGON
  STARTER, $29/MO` since the warehouse is only useful with a real
  nightly data source — yfinance/fixture writes would muddy the
  `data_source = 'polygon'` distinction at deploy time.
- No backfill. First row arrives the first nightly run after Polygon is
  wired.
- No Polygon subscribe.

## Verification

- `cd backend && npm run build` — passes clean.
- `cd backend && npx tsx --test src/services/huntFixtureMode.test.ts src/services/spreadResultsService.test.ts` — 12/12 pass.
- `cd frontend && npm run build` — passes (`345.52 kB` js / `23.33 kB` css, no change from prior commit since this is backend-only).
- Schema-precision rounding test: `winRate: 78.123` round-trips to `78.12` (2-decimal `NUMERIC(5,2)`); `evPercent: 12.456` → `12.46`; `premium: 1.4231` preserved at 4-decimal precision; `currentPrice: 187.234` → `187.23`; `ivRank: 42.555` → `42.56`.
- Negative-EV preservation test: warehouse rows include cells with
  `ev_percent < 0`, since the matrix UI relies on negative-EV cells to
  show "stay away" pockets — same shape as the 2026-04-30 strategy
  matrix run (commit `34e8002`).

## Public-copy hygiene

Per `RULES.md` rule 14/15: not applicable — internal service code, no
customer-facing surface affected.

## State changes this run

- `OPEN_GATES.md` — unchanged. Did not raise a new gate this run; did
  not resolve any open gate. The `MIGRATION APPLIED: SPREAD_RESULTS
  WAREHOUSE` gate stays open since this service won't actually function
  against the DB until Travis applies the migration SQL.
- `BUDGET.md` — unchanged. No spend. Cash balance: `$162.45`.
- `TODO.md` — to be updated this run.
- `RUNLOG.md`, `HANDOFF.md`, `SCORECARD.md` — appended this run.

## Suggested post copy:

(none — internal infrastructure, no Discord-side action requested from Travis on this commit)
