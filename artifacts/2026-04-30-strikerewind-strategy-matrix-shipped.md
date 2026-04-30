# StrikeRewind — full strategy matrix on `/analysis/:ticker`

**Date:** 2026-04-30
**Commit:** `34e8002` on `autobox/strikerewind-rename` (tbuerky/StrikeSight)
**Build queue step:** #6 from 2026-04-28 product-defining HANDOFF

## What shipped

The Ticker Analysis page (`/analysis/:ticker`) now renders a full historical credit-spread heat map: every (strikeType × OTM% × DTE-weeks) combination scored by expected value per trade, including the negative-EV cells the previous code dropped. This is the activation feature the HANDOFF spec called out — "first thing a new user does after signup" — and the proof point for the product's whole pitch ("find ticker-specific delta/DTE patterns that defy generic rules"). Until now the page only showed the filtered top 5, which left that pitch unproven on the surface meant to prove it.

## Backend changes

- `backend/src/types/index.ts`: new `StrategyMatrixCell` interface + `allStrategies: StrategyMatrixCell[]` on `AnalysisResult`.
- `backend/src/services/newAnalysisEngine.ts`:
  - `analyzeSpreadResults`: dropped the `expectedValue > 0` and `avgPremium * 100 >= $5` filters. Now keeps every cell with `totalTrades >= 30` (sample-size credibility threshold preserved). Sort changed from `evScore` to `expectedValue` so negative-EV cells order correctly (the old `evScore` capped negatives at 0 and tied them).
  - `analyzeStock`: builds `viableSpreadAnalyses` (the legacy filtered set) by re-applying the EV>0 and premium>=$5 filters at the consumer, so `topStrategies`, `findOptimalStrategy`, and `viableStrategies` count behave exactly as before. Then emits `allStrategies` from the unfiltered `allSpreadAnalyses` for the matrix.
- `backend/src/services/analysisEngine.ts` (legacy): returns `allStrategies: []` to satisfy the type.

## Frontend changes

- `frontend/src/types/index.ts`: mirror `StrategyMatrixCell` + `allStrategies?` on `AnalysisResult`.
- `frontend/src/components/StrategyMatrix.tsx` (new, 192 lines): PUT/CALL tabs, OTM% rows × DTE-weeks columns, cells colored by EV per trade (≥5% accent green, >0 accent-soft, ~0 elevated, <-5 neg-tinted), hover/title shows win rate + premium + sample, dashes for insufficient-data cells. Cove tokens throughout.
- `frontend/src/pages/Analysis.tsx`: import and render `<StrategyMatrix>` between the top-strategy hero and the top-5 table when `allStrategies` is non-empty.

## Verification

- `cd backend && npm run build` → clean tsc pass.
- `cd frontend && npm run build` → clean tsc + Vite build, 1920 modules.
- Bundle: JS `339.67 → 345.52 kB` (+5.85 kB / +1.7%), CSS `22.94 → 23.33 kB` (+0.39 kB).
- `node --test backend/dist/services/huntFixtureMode.test.js` → 3/3 pass.
- Standalone Playwright preview of the matrix component (`/tmp/strategy-matrix-preview.html`, mocked dataset where the ticker "pays" at 10-15% OTM × 6-8w PUT and 5-10% OTM × 4-6w CALL): both PUT and CALL tabs render correctly, the green clusters and red ITM rows read at a glance, ITM rows with `—` cells (insufficient samples at long DTE) display correctly, tab switching works.

## Why this matters for revenue

The product pitch on the landing page (Luke-shipped in `eddc21f`) is "stop selling 30-delta on every ticker — find the delta/DTE pocket where this specific ticker has historically paid." A user who signs up and lands on `/analysis/:ticker` was previously shown a generic top-5 list with no evidence the ticker had any structural pattern at all — they just saw "AAPL, 30% OTM, 6w, +5.2% EV." Now they see the full grid and can read the ticker's profile in two seconds: where it pays, where it breaks, what conventional wisdom misses. This is the first time the product visibly does the thing it sells.

## Backwards compatibility

- `topStrategies` field shape unchanged. All existing consumers (Hunt route in `backend/src/index.ts:606+`, scheduler service watchlist alerts) read the same filtered set as before.
- `analysis.optimal` and `analysis.timeframes` unchanged.
- Sort change: only affects ordering inside `analyzeSpreadResults` output. `findOptimalStrategy` and `topStrategies.slice(0, 5)` operate on the filtered viable subset (only positive EVs), so identical ordering for both old and new sort keys (positive EVs preserve their relative order).
- `viableStrategies` field now reflects the post-filter count (was always the post-filter count under the old code path, so no behavior change).

## What this does NOT do

- Does not deploy to StrikeRewind.com — the production deploy is the next priority and a separate run.
- Does not wire real options data — Polygon subscription remains gated on owner approval.
- Does not change Hunt scanner output — only the per-ticker analysis page got the matrix.

Cash balance: `$162.45`. No spend.
