# StrikeRewind pivot — Commit 2: overnight scheduler job

**Run:** 5 of 2026-05-08
**Branch:** `autobox/strikerewind-rename`
**Commit:** `eed78fc`
**Status:** shipped to GitHub; not yet wired into any cron; not yet executed against the live DB

## What shipped

`backend/src/jobs/computeSpreadResults.ts` (new file, 137 lines) plus `computeSpreadResults.test.ts` (14 deterministic tests). One small additive change to `backend/src/services/supabaseDatabaseService.ts` — extended `SpreadResultRow` with the optional pivot columns added in Commit 1b so the TS type matches the post-migration physical schema.

### Pieces

1. **`winRateResultsToWarehouseRows(results, asOfDate)`** — pure mapping from `WinRateResult[]` to `SpreadResultRow[]`. Bridges:
   - `direction` ∈ {`bull_put`,`bear_call`} → `spread_type` ∈ {`PUT`,`CALL`} (legacy NOT NULL)
   - `otmPct` (decimal) → `otm_percentage` (×100, two decimals; legacy NOT NULL)
   - `dteWeeks` → `timeframe_weeks` (legacy NOT NULL)
   - `winRate` → `win_rate` (decimal 0..1; pivot semantics; spec §5 expects `>= 0.60` filter)
   - `minPremium100` → `premium` (legacy NOT NULL repurposed as the credit floor)
   - `observationCount` → `total_trades` (legacy NOT NULL repurposed as sample size)
   - All eight new pivot columns populated: `otm_pct`, `dte_weeks`, `direction`, `observation_count`, `min_premium_pct`, `min_premium_100`, `min_premium_500`, `low_confidence`
   - `analysis_years = 5`, `data_source = 'price_history_5yr'`, `current_price = null`, `iv_rank = null`, `ev_percent = 0`
2. **`fetchPricesForTicker(ticker, asOfDate, historyYears, provider)`** — fetches a 5yr window ending at `asOfDate` via the `PriceDataProvider` interface (already abstracted; default is Yahoo).
3. **`runSpreadResultsBatch(opts)`** — orchestrator. Per ticker: fetch → `calculateGrid` → `upsertResults`. Records `batch_runs` start/complete. Per-ticker failures do not abort the batch; final status resolves to `succeeded` / `partial` / `failed` based on processed-vs-failed counts.

### Tests

40/40 pass (was 26/26). Net new tests cover:
- Mapping invariants (one row per WinRateResult; direction→spread_type; otm_percentage = otm_pct × 100; legacy NOT NULL columns populated; premium = min_premium_100; total_trades = observation_count; win_rate is decimal 0..1; ticker uppercased)
- The algebraic invariant `min_premium_100 = (1 − win_rate) × 100` across the full grid on synthetic oscillating prices
- `fetchPricesForTicker` requests exactly `historyYears × 365` days back from `asOfDate`
- Orchestrator: batch-of-2 happy path; per-ticker failure → `partial`; all-fail → `failed`; batch_runs lifecycle calls fired

`npx tsc --noEmit` clean.

## Why now

Run 4's handoff named this exact move: "best autonomous move is **StrikeRewind pivot Commit 2 — overnight scheduler**: write `backend/src/jobs/computeSpreadResults.ts` that pulls 5yr daily history per S&P 500 ticker via `priceDataProvider`, calls `calculateGrid` (shipped in Commit 1), and writes one row per `(ticker, otm_pct, dte_weeks, direction)` into `spread_results` with `data_source='price_history_5yr'`." Took it.

Window for this move per run 4's table: "Now through 2026-05-08 20:17 UTC". Fired at 12:17 UTC.

## Deliberately NOT done

- Did not replace `SchedulerService` or wire the new job into cron. The spec calls for a 8:00 PM ET nightly trigger; that lands once Commit 3 repoints Hunt to filter `data_source = 'price_history_5yr'` so pivot rows do not leak into the legacy Hunt response.
- Did not execute the batch against the live DB. The pure unit test on the mapping function is bounded; a live single-ticker AAPL smoke would write rows that the current Hunt query (no `data_source` filter) would surface to users with `win_rate` semantics that don't match the legacy 0..100 column. Defer to Commit 3.
- Did not delete `ivService.ts` or the synthetic Black-Scholes premium estimator. Spec §"What gets deleted" — but those still feed the live legacy path. Drop them in the same commit that repoints Hunt.
- Did not route through Cove / Luke (backend-only, no customer-visible surface).
- Did not raise a new gate.

## Live behavior

Unchanged. New file is not imported anywhere yet outside its test. Hunt, Ticker Analysis, Watchlist, Account, scheduler, all untouched.

## Next move

**Commit 3 — Hunt API repoint.** New request schema (`min_win_rate`, `max_otm_pct`, `max_dte_weeks`, `direction`); new response schema (drop synthetic `currentIV`/`ivRank`/`ivPercentile`, add the new pivot fields); query path uses `data_source = 'price_history_5yr'` + `observation_count >= 20`; remove `ivService.ts` and Black-Scholes premium math. After Commit 3 lands, Commit 2's job is safe to execute against live (a single AAPL smoke will populate ~80–100 rows into a fresh `as_of_date`, and Hunt will read them through the new query).

## Cash

`$162.45`. No spend. Render starter accruing ~$0.23/day.

## Suggested post copy

> Run 5 today: shipped pivot Commit 2 — overnight scheduler job. New `computeSpreadResults.ts` plus 14 deterministic tests; pure mapping function bridges legacy NOT NULL columns to the new pivot columns added in Commit 1b. 40/40 tests green; live behavior unchanged because the job isn't wired into cron yet — that lands once Commit 3 repoints Hunt. Commit `eed78fc` pushed. Two gates still on you: POLYGON KEY READY, ADS DECISION. Cash $162.45.
