# StrikeRewind production smoke — post-Massive default-flip deploy (commit `d01e46f`)

**Date**: 2026-05-10 02:17–02:35 UTC (run 1 of 2026-05-10)
**Target**: `https://www.strikerewind.com` and `https://strikerewind-api.onrender.com`
**Commit under test**: `d01e46f` "Flip default price provider back to Massive (per-call allowlist safe)" — pushed 2026-05-09 23:45 UTC by AutoBox commit author on Travis's behalf, auto-deployed via Render.

## Why this run

Travis's commit message on `d01e46f` reads "Travis is testing the live site tonight and wants the production-ready config." The default `getDefaultPriceDataProvider()` now returns Massive when env is set — first time `/api/analyze` runs against Massive in production. Prior attempt at this flip (run 11→12 of 2026-05-08) OOM'd the 512 MB Render container; rollback `77307a7` reverted it. Run 6 of 2026-05-09 (commit `90a0bd1`) introduced a per-call allowlist designed to make this flip safe. `d01e46f` is the bet that 90a0bd1 actually fixed it.

A silent regression here would crater Travis's testing pass and the open `TESTING COMPLETE: STRIKEREWIND DATA-LIVE` gate. Catching it before he does is the highest-leverage autonomous move in this window.

## Result

**35 / 35 pass / 0 fail.** Product is healthy on Massive default. `/api/analyze` for AAPL returns in 1.3 s with a real response payload (`currentPrice`, `analysis.optimal`, `topStrategies` populated). No OOM, no 5xx on the live UX path. Render container is comfortably under memory limit.

## Smoke harness fix shipped this run

First `node workspace/strikerewind_smoke.mjs` invocation failed at test 10 with `page.goto: Timeout 30000ms exceeded` on the `/analysis/ZZZZZ` error-path test, aborting the script before tests 11–35 could run.

Direct probe established the product was fine:
- `/api/analyze` for `ZZZZZ` returns HTTP 500 in 0.5 s with body `{"error":"Insufficient data for ZZZZZ: only 0 points, need 130"}`.
- The page renders the expected error UI: `Could not load ZZZZZ` heading, error detail line, Back button, full nav.
- Failure cause was the harness's `waitUntil: 'networkidle'` — under Massive the page keeps polling `/api/usage` and `/api/watchlist/tickers` so networkidle never fires within 30 s.

One-line fix in `workspace/strikerewind_smoke.mjs`: switched the error-path goto from `networkidle` → `domcontentloaded` (the Back-button navigation followup was already permissive). No test semantics changed; the Could-not-load heading + ticker name + Back button assertions all still run unchanged. Re-ran smoke: 35/35.

## Coverage post-fix

- Landing renders.
- Analyze AAPL: ticker + EV + current price + strategy matrix, no blank page, active-tab color `rgb(34, 197, 94)`, URL `/analysis/AAPL`.
- Error path ZZZZZ: heading, ticker name, Back button, navigates back to `/dashboard`.
- Hunt: tab loads, fixture rows present, row click → `/analysis/MSFT`.
- Watchlist API 200; Watch tab renders AAPL/MSFT/UNH with real fixture data (no "Data refreshing" placeholder), remove button works, row click → `/analysis/AAPL`.
- Stripe prices populated: standard `price_1TUdOXAy6OYpyg`, pro `price_1TUdOYAy6OYpyg`.
- Account: FREE tier badge, STANDARD + PRO plan cards.
- Mobile 390 × 844: zero horizontal overflow.

## What this means for Travis

The Massive-default flip is **production-stable for `/api/analyze`**. The earlier OOM mode (run 11→12 of 2026-05-08) is not reproducing — the per-call allowlist from 90a0bd1 worked as designed. Travis can keep testing tonight without a stale-deploy concern.

## Gates

- `ADS APPEAL: PAF GOOGLE ADS SUSPENDED — APPEAL FILED 2026-05-08` — unchanged, Travis-side, awaiting Google.
- `TESTING COMPLETE: STRIKEREWIND DATA-LIVE` — unchanged, Travis-side, his current testing pass is the path to closure.

No new gate raised.

## Spend

$0. Cash balance $162.45.
