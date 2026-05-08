# StrikeRewind pivot Commit 3 — deletion-surface audit

**Date**: 2026-05-08 14:17 UTC (run 6 of 2026-05-08)
**Repo**: `/home/autoproj/projects/StrikeSight`
**Branch**: `autobox/strikerewind-rename`
**Scope**: read-only audit. No code changes. Goal: enumerate every file/line that references `currentIV`, `ivRank`, `ivPercentile`, `estimateCreditSpreadPremium`, `IVService`, or `ivService` so Commit 3 can be a mechanical change rather than a discovery exercise.

## Summary

14 files contain at least one reference. Splits cleanly into:

- **3 files to delete entirely**: `ivService.ts`, plus the IV-only paths inside `analysisEngine.ts` / `newAnalysisEngine.ts` are deletable along with `analyzeStock`/`analyze` once `/api/hunt` is repointed at `getHuntSpreadResults`.
- **5 backend files to edit**: `index.ts` (heaviest — hunt route, watchlist route, scheduler-shaped block), `types/index.ts`, `huntFixtureMode.ts`, `huntFixtureMode.test.ts`, `spreadResultsService.ts`, `spreadResultsService.test.ts`, `schedulerService.ts`.
- **4 frontend files to edit**: `types/index.ts`, `pages/Hunt.tsx`, `pages/Watchlist.tsx`, `pages/Home.tsx`.

The Hunt route as currently wired does NOT go through `getHuntSpreadResults` — it calls `analysisEngine.analyzeStock` per-ticker on every hunt request. Commit 3 must repoint the route, not just rename fields.

## Backend — DELETE

### `backend/src/services/ivService.ts` (entire file)
All 100% Black-Scholes / synthetic IV math. No external imports beyond inside `analysisEngine.ts` and `newAnalysisEngine.ts`. Safe delete once those two engines stop importing it.

## Backend — EDIT

### `backend/src/index.ts` — heaviest edit
| Line | Reference | Action |
|---|---|---|
| 127–129 | `result.ivRank/ivPercentile/currentIV = 0` (analysis route fallback) | Remove (analysis route can drop IV display entirely under pivot) |
| 181–183, 190 | Same triple zeroing + `criteria.minIVRank` filter | Remove `minIVRank` from criteria entirely |
| 271, 285 | `ivRank: showIV ? analysis.ivRank : 0` in analysis response | Remove |
| 459, 465–467, 473, 481 | High-IV stocks aggregator (`/api/high-iv-stocks`?) | Delete the entire block — synthetic-IV ranking has no place under pivot |
| 502, 508–510, 521, 529 | Scheduler-style aggregation block (duplicate) | Delete |
| 547–710 | `/api/hunt` route — calls `analysisEngine.analyzeStock` per ticker, applies `criteria.minWinRate`, `criteria.maxTimeframe`, `criteria.minEvScore` | **Rewrite to read from `dbService.getHuntSpreadResults` filtered by `data_source='price_history_5yr'`, `win_rate >= criteria.minWinRate`, `otm_pct <= criteria.maxOtmPct`, `dte_weeks <= criteria.maxDteWeeks`, `direction = criteria.direction`, `observation_count >= 20`. Keep fixture-mode branch but update its shape too.** |
| 697 | `ivRank: showIV ? result.ivRank : undefined` in opportunity payload | Remove |

### `backend/src/services/analysisEngine.ts`
Lines 2, 9, 13, 178, 185–187. `IVService` import + instance + `getIVData` call + ivRank/ivPercentile/currentIV in returned object. The whole `analyzeStock` method is dead once `/api/hunt` is repointed. **Defer file deletion to Commit 3.5** if the analysis page (`/analysis/:ticker`) still calls it; otherwise delete with Commit 3.

### `backend/src/services/newAnalysisEngine.ts`
Lines 2, 36, 41, 87 (`estimateCreditSpreadPremium` private method), 214 (call site), 422, 454–456. Same pattern as above. Delete the file or strip IV+premium math depending on whether `/analysis/:ticker` still uses it.

### `backend/src/services/huntFixtureMode.ts`
Lines 35, 44–46, 65, 72, 81, 90, 158–160, 219. Fixture row shape includes `ivRank`/`ivPercentile`/`currentIV`. Update fixture shape to match the new pivot response (`otm_pct`, `dte_weeks`, `direction`, `win_rate`, `observation_count`, `min_premium_100`, `low_confidence`).

### `backend/src/services/huntFixtureMode.test.ts`
Lines 36, 67. Update expectations to assert pivot fields, not `ivRank`.

### `backend/src/services/schedulerService.ts`
Lines 86, 91, 97–99, 120, 128. The legacy "best high-IV opportunities" aggregation. Delete this entire code path — it is parallel to the deletable index.ts blocks.

### `backend/src/services/spreadResultsService.ts`
Line 45: `iv_rank: round(result.ivRank, 2)`. Today this writes legacy column on warehouse upsert. Remove (the column itself was made nullable in Commit 1b; Commit 2's mapper does not populate it).

### `backend/src/services/spreadResultsService.test.ts`
Lines 12–14. Drop `ivRank`/`ivPercentile`/`currentIV` from the test fixture WinRateResult.

### `backend/src/types/index.ts`
Lines 40–42 (response type) and 59 (`minIVRank?` on criteria type). Delete fields. Add new pivot criteria type per spec §5.

### `backend/src/middleware/validation.ts`
Line 43 (`minIVRank` Joi rule), line 72 (`minWinRate`). Drop `minIVRank`. Add `direction`, `maxOtmPct`, `maxDteWeeks` rules. Keep `minWinRate` (semantics shift: 0..1 decimal, pivot column).

## Frontend — EDIT

### `frontend/src/types/index.ts` (lines 41–43)
Drop `ivRank`/`ivPercentile`/`currentIV` from the analysis/opportunity response type. Add `otm_pct`, `dte_weeks`, `direction`, `win_rate`, `observation_count`, `min_premium_100`, `low_confidence`.

### `frontend/src/pages/Hunt.tsx`
- Line 30: `ivRank?: number` on opportunity row type — remove.
- Lines 73, 212, 219–220: `criteria.minWinRate` slider — keep (semantics shift to decimal 0..1 over the wire, but UI can keep percent display).
- Lines 241, 248, etc: `criteria.minEvScore` — remove (not in pivot spec).
- Lines 261, 268: `criteria.maxTimeframe` — rename to `maxDteWeeks` to match new API.
- Lines 281, 288: `criteria.historicalYears` — remove (pivot is 5yr-only).
- Add `direction` select (PUT / CALL) and `maxOtmPct` slider.
- Update result row rendering to show OTM%, DTE, direction, win rate, min premium, observation count, low-confidence badge.

### `frontend/src/pages/Home.tsx`
Line 22: `ivRank?: number` on a hero/sample row — remove (or replace with new pivot fields if hero shows live data).

### `frontend/src/pages/Watchlist.tsx`
- Lines 14, 185–188, 227–230. Watchlist UI **renders** `item.ivRank.toFixed(0)` in two places with color-coded thresholds. Replace with a pivot-relevant cell — e.g. best win rate across the matrix for that ticker, or a "Hunt highlight" link.
- This is the most user-visible change; warrants a Cove pass before deploy.

### `frontend/src/services/api.ts`
Line 60: `api.post('/api/hunt', { criteria: backendCriteria })` — the wire shape changes. Rebuild `backendCriteria` from the new Hunt UI state.

## Tests that must move green at end of Commit 3

| File | What changes |
|---|---|
| `backend/src/services/spreadResultsService.test.ts` | Drop ivRank fixture, add pivot fields |
| `backend/src/services/huntFixtureMode.test.ts` | Update assertions to pivot fields |
| `backend/src/services/computeSpreadResults.test.ts` | No change — Commit 2's tests are pivot-clean already |
| `backend/src/services/winRateCalculator.test.ts` | No change |
| Existing `/api/hunt` integration tests, if any | Repoint criteria + assertions; same for Playwright Hunt smoke |

`tsc --noEmit` will surface every dropped-field call site.

## Out of scope for Commit 3 (per spec §5 + run-5 handoff)
- Wiring `runSpreadResultsBatch` into nightly cron — that is Commit 5 / scheduler-rewrite.
- Polygon IV overlay — gated on owner `POLYGON KEY: <key>`, then Commit 4.
- `/analysis/:ticker` page rebuild — Commit 6 if the matrix UI changes; the route itself can keep using `getTickerSpreadMatrix` against the pivot rows.

## Execution order suggested for Commit 3 itself

1. Update validation schemas + types + `getHuntSpreadResults` signature (mechanical, type-checked).
2. Rewrite `/api/hunt` to call `dbService.getHuntSpreadResults` with the new params; keep fixture branch.
3. Rewrite `huntFixtureMode.ts` shape; fix tests.
4. Strip `ivService.ts` import + IV blocks from `analysisEngine.ts`, `newAnalysisEngine.ts`, `schedulerService.ts`, `spreadResultsService.ts`.
5. Delete `ivService.ts`.
6. Delete the `/api/high-iv-stocks` (or equivalent) blocks in `index.ts`.
7. Update frontend types + Hunt.tsx + Watchlist.tsx + Home.tsx + api.ts. Route Watchlist + Hunt result-row redesigns through Cove before deploy.
8. Single-AAPL `runSpreadResultsBatch` smoke into Supabase; then live deploy.

## Risk and live-impact notes

- The hunt route currently runs synchronously through `analysisEngine.analyzeStock` per ticker — slow path that the pivot architecture is designed to eliminate. Repointing at `getHuntSpreadResults` is the load-bearing performance win.
- Watchlist `ivRank` rendering is the only user-visible pivot field today. A naive Commit 3 that only changes Hunt would leave Watchlist showing stale IV ranks; bundle the fix.
- Marketing freeze still on (Travis). Commit 3 is fine to land behind closed doors — the pivot rows must be populated for the page to be useful, but until `runSpreadResultsBatch` runs against live (Commit 3.5), Hunt will return empty results. That is acceptable while Travis is the only tester.
