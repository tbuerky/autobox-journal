# StrikeRewind pivot — Commit 3 prework: pivot-side query + response mapper

**Date**: 2026-05-08 (run 7 of 2026-05-08)
**Branch**: `autobox/strikerewind-rename`
**Commit**: `4f841e0`
**Result**: 53/53 backend tests pass; `tsc --noEmit` clean; pushed to origin; live behavior unchanged.

## Why this slice now

Run 6's audit (`artifacts/2026-05-08-strikerewind-pivot-commit-3-deletion-surface-audit.md`) laid out an 8-step Commit 3. Steps 1–7 touch live code paths; step 7 includes Watchlist row redesign that warrants Cove. Within the available budget I took the **purely additive** prework that closes the data-access + response-shape questions without touching any live consumer:

1. New `getHuntSpreadResultsPivot` query method on the database service.
2. New `huntPivotMapper.ts` module — pure functions that turn a pivot-shape `SpreadResultRow` into the response payload Commit 3's repointed `/api/hunt` will return.

Both are dead code today (no consumer imports them). When the next run executes Commit 3 step 2 (the `/api/hunt` rewrite), it picks them up and the rewrite becomes mechanical.

## What shipped

### `backend/src/services/supabaseDatabaseService.ts`

Added `getHuntSpreadResultsPivot(opts)` — sister to the existing `getHuntSpreadResults`. Filters:

- `data_source = 'price_history_5yr'` — strictly the new pivot rows; never returns legacy synthetic-IV rows
- `win_rate >= opts.minWinRate` (decimal 0..1, pivot semantics)
- `otm_pct <= opts.maxOtmPct`
- `dte_weeks <= opts.maxDteWeeks`
- `observation_count >= opts.minObservationCount ?? 20` (suppress low-confidence by default)
- `direction = opts.direction` unless `'BOTH'`
- Optional `as_of_date` pin
- Order: `as_of_date DESC, win_rate DESC`; `LIMIT opts.limit`

Index `spread_results_pivot_hunt_idx` (added in Commit 1b) covers the predicate set.

### `backend/src/services/huntPivotMapper.ts` (new file)

Three exports:

- `pivotRowToHuntOpportunity(row)` — pure mapper. Throws `PivotRowMissingFieldsError(field, ticker)` when any required pivot field is null. Defaults `low_confidence=null` to `false`.
- `isPivotRow(row)` — predicate. True iff `data_source === 'price_history_5yr'` AND all five required pivot fields are non-null.
- `HuntOpportunityPivot` interface — the shape Commit 3's `/api/hunt` returns: `{ ticker, direction, otmPct, dteWeeks, winRate, observationCount, minPremium100, lowConfidence, asOfDate }`.

This pins the response-shape decision the audit left open and gives the next run a typed building block instead of inline-mapping in the route handler.

### `backend/src/services/huntPivotMapper.test.ts` (new file, 13 tests)

- field-by-field mapping happy path (`AAPL`, `bull_put`, every field round-trips)
- `low_confidence` null defaults to false
- `bear_call` direction preserved
- explicit throws for each required missing field (`direction`, `otm_pct`, `dte_weeks`, `observation_count`, `min_premium_100`)
- error message includes ticker context for debugging
- `isPivotRow` true on full row; false when `data_source` is `'polygon'`, undefined, or any pivot field is null

## Verification

- `npx tsc --noEmit` clean
- `npx tsx --test src/services/*.test.ts src/jobs/*.test.ts` → **53/53 pass** (was 40/40; +13 new)
- Commit `4f841e0`, pushed to `origin/autobox/strikerewind-rename`
- No consumer wired; `/api/hunt` still calls `analysisEngine.analyzeStock` per ticker
- No deploy, no live behavior change

## Why this is bounded

- Both new symbols are dead code on `main`. Removing or renaming either is a one-line revert.
- The query method bypasses legacy rows by hard-pinning `data_source = 'price_history_5yr'` — even if accidentally called against the live DB today, it would return zero rows (Commit 2 has not yet executed live).
- The mapper has no side effects and no I/O; tests are deterministic.

## What remains in Commit 3

In execution order from the audit:

1. ✅ (this run) Pivot-side query method + mapper
2. Update `validation.ts` schema: drop `minIVRank` / `minEvScore`, add `direction` / `maxOtmPct` / `maxDteWeeks`. Update `types/index.ts` criteria type.
3. Rewrite `/api/hunt` route to call `getHuntSpreadResultsPivot` + `pivotRowToHuntOpportunity`. Keep fixture branch but update its shape.
4. Rewrite `huntFixtureMode.ts` shape; fix tests.
5. Strip IV imports + blocks from `analysisEngine.ts`, `newAnalysisEngine.ts`, `schedulerService.ts`, `spreadResultsService.ts`.
6. Delete `ivService.ts`.
7. Delete the `/api/high-iv-stocks`-shaped block in `index.ts:459–529`.
8. Frontend: `types/index.ts`, `Hunt.tsx`, `Watchlist.tsx`, `Home.tsx`, `api.ts`. Watchlist row redesign needs Cove.
9. Single-AAPL `runSpreadResultsBatch` smoke against live DB; then deploy.
