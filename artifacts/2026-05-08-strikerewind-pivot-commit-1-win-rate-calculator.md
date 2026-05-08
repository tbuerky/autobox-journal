# StrikeRewind pivot — Commit 1: win rate calculator

**Date:** 2026-05-08
**Branch:** `autobox/strikerewind-rename`
**Commit:** `8bf752f` (pushed to origin)
**Spec:** `artifacts/2026-05-08-strikerewind-price-history-pivot-spec.md`

## What this is
First of seven commits in the pivot from synthetic options data to a pure
price-history edge scanner. Adds the win rate calculator service — the
load-bearing math the entire pivot sits on top of.

## What shipped
- `backend/src/services/winRateCalculator.ts` (new)
  - `calculateWinRate(input)` — walks Friday entries in a daily price
    series, measures expiration-day outcomes against a strike defined by
    `otmPct` + `direction`, returns empirical win rate plus
    `minPremiumPct = 1 - winRate` and dollar floors for $100/$500-wide
    spreads. Returns `null` if observations < 20. Flags
    `lowConfidence: true` when 20 ≤ observations < 40.
  - Exports `OTM_GRID`, `DTE_WEEKS_GRID`, `DIRECTIONS`, and
    `calculateGrid(ticker, prices)` for the overnight batch in Commit 2.
- `backend/src/services/winRateCalculator.test.ts` (new) — 10
  deterministic cases.

## Verification
- `npm run build` clean.
- `node --test dist/services/winRateCalculator.test.js` — 10/10 pass.
- Existing backend tests (`priceDataProvider`, `huntFixtureMode`,
  `spreadResultsService`) — 16/16 pass; no regression.
- 26/26 backend tests green.

## Deliberately NOT done in this commit
- Did NOT delete `ivService.ts` or Black-Scholes premium estimation —
  callers still depend on them; that removal is bundled with Commit 3
  (Hunt API rewrite) so the diff stays coherent.
- Did NOT add Supabase schema migration columns yet — written in a
  separate Commit 1b once the calculator API is stable. No production
  data depends on this commit.
- Did NOT touch the scheduler — that is Commit 2.
- Did NOT change Hunt response — that is Commit 3.
- Did NOT route through Cove or Luke — backend-internal pure function,
  no customer-visible surface.
- Did NOT subscribe to Polygon — not in this commit's scope, and Travis
  said in the addendum he handles that purchase manually.

## Why push to origin
This commit is additive only — two new files, zero callers. Render
auto-deploys the branch but live behavior is unchanged because nothing
imports the new module yet. Safe to put it on the remote so the next
autonomous run can build on it without re-stashing local state.

## Next runnable steps
1. **Commit 1b — Supabase schema migration** for `spread_results` (new
   columns: `otm_pct`, `dte_weeks`, `direction`, `win_rate`,
   `observation_count`, `min_premium_pct`, `min_premium_100`,
   `min_premium_500`, `low_confidence`, `data_source`). Migration SQL
   ready to apply via Supabase dashboard.
2. **Commit 2 — Overnight scheduler** swap. Replace the existing
   scheduler with a nightly price-history batch that calls
   `calculateGrid()` per ticker and writes to `spread_results`.
3. **First real batch run** to populate `spread_results` with actual
   price-history results — per Travis's addendum, this is the move
   that takes Hunt out of fixture mode for real.
4. **Commit 3** — Hunt API rewrite + delete `ivService.ts` /
   `estimateCreditSpreadPremium`.

## Cash balance
$162.45. No spend.
