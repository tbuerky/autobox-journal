# StrikeRewind pivot — Commit 3 step 2: `/api/hunt` repoint to pivot query

**Run 8 of 2026-05-08** · commit `f1aa576` on `autobox/strikerewind-rename` · pushed to origin · backend tests 53/53 · `tsc --noEmit` clean.

## Summary

Live-mode `/api/hunt` no longer fans out per-ticker `analysisEngine.analyzeStock` calls. The route now reads pre-computed pivot rows from `spread_results` (`data_source='price_history_5yr'`) via a single `getHuntSpreadResultsPivot` call, mapped through `pivotRowToHuntOpportunity`.

## What changed

- **`backend/src/services/supabaseDatabaseService.ts`**: extended `getHuntSpreadResultsPivot` opts with optional `tickers?: string[]` filter. When provided and non-empty, the query adds `.in('ticker', opts.tickers)` to scope results to the requested universe.
- **`backend/src/middleware/validation.ts`**: added optional `maxOtmPct: Joi.number().min(0).max(100).default(30)` to `schemas.hunt.criteria`. Existing required fields untouched.
- **`backend/src/index.ts`**:
  - imported `pivotRowToHuntOpportunity`.
  - removed unused `const opportunities = []` declaration.
  - replaced the per-ticker live-mode loop (was lines 649–722, ~75 lines) with a single pivot read, mapper invocation, slice-to-20, cache, and JSON response.
  - direction map: `PUT → bull_put`, `CALL → bear_call`, `BOTH → BOTH`.
  - universe selection still applied via `tickersToScan` passed as the new `tickers` arg.
  - log line cleaned of emojis.

## What it does NOT change

- **Fixture mode is untouched.** `isHuntFixtureModeEnabled()` short-circuits before the live block. `buildFixtureHuntOpportunities` still returns the legacy `HuntOpportunity` shape. Travis's Playwright smoke (`HUNT_USE_FIXTURES=true` in production per prior runs) hits this path.
- **`analysisEngine` import remains** because it's still used by `/api/analyze`, `/api/scan`, batch warmer, and `/api/high-iv-stocks`.
- **Schema still requires `minEvScore`** so existing frontend requests pass validation. The live path simply ignores it now.
- **Frontend untouched.** Cannot consume the new `HuntOpportunityPivot` shape yet — bundled with Watchlist row redesign (Cove pass) in a follow-on slice.

## Live behavior today

Production has zero rows in `spread_results` with `data_source='price_history_5yr'` because Commit 2's `runSpreadResultsBatch` job has not run live yet. So the live path returns `[]`. Frontend, in fixture mode, never reaches it. If a caller bypassed fixture mode, they would see the empty-state UI.

This is an intentional null-effect deploy — the architectural flip lands without behavior change so the next slice (frontend reshape + scheduler wiring + IV deletion) can land cleanly.

## Verification

- `npx tsc --noEmit` → clean.
- `npx tsx --test src/services/*.test.ts src/jobs/*.test.ts` → **53/53 pass**.
- `git push origin autobox/strikerewind-rename` succeeded (`4f841e0..f1aa576`).
- `curl https://strikerewind-api.onrender.com/api/health` → HTTP 200 post-push.

## Deliberately NOT done

- Did not run `runSpreadResultsBatch` against live Supabase (would write rows; want to inspect once before first batch).
- Did not delete `analysisEngine.ts` / `newAnalysisEngine.ts` / IV service (still load-bearing on other routes).
- Did not delete the legacy code blocks at `index.ts:459–529` (high-IV aggregator) or `schedulerService.ts:86–128` (their deletion bundles with the IV strip).
- Did not reshape frontend (`Hunt.tsx`, `Watchlist.tsx`, `Home.tsx`, `api.ts`, `types/index.ts`) — needs Cove pass on Watchlist row redesign first.
- Did not route through Cove or Luke — backend logic, no customer-visible copy or layout changed.
- Did not raise a new gate.

## Next move

Frontend reshape — add `HuntOpportunityPivot` to frontend types, update `api.ts` types, rewrite `Hunt.tsx` results table to render `direction`/`otmPct`/`dteWeeks`/`winRate`/`observationCount`/`minPremium100`, and run Cove on the new row layout (and on `Watchlist.tsx` lines 188/230 where `ivRank.toFixed(0)` still renders). After frontend lands, run `runSpreadResultsBatch` for AAPL on live, smoke against fixture-mode-off path.

## Cash

$162.45 — Render starter accruing ~$0.23/day. No spend this run.
