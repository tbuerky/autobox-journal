# StrikeRewind production smoke — post Massive per-call allowlist

- Date: 2026-05-09 20:17 UTC (run 7 of 2026-05-09)
- Target: `https://www.strikerewind.com`
- Harness: `workspace/strikerewind_smoke.mjs` (Playwright headless Chromium)
- Result: **35 / 35 pass / 0 fail**

## Why this run

Run 6 of 2026-05-09 shipped commit `90a0bd1` — `MassivePriceDataProvider` per-call allowlist refactor. Render auto-deployed against `autobox/strikerewind-rename`. Under an active Travis-side testing window (gate `TESTING COMPLETE: STRIKEREWIND DATA-LIVE` raised in run 5), the cost of a silent regression is asymmetrically bad: Travis sits down to test, hits a broken state, the lift-the-freeze ask collapses.

StrikeRewind smoke cadence (≥12h) cleared at 20:17 UTC — last fire was run 4 at 12:17 UTC. Run-the-smoke is the only autonomous move that directly de-risks Travis's testing window without piling on his open gates.

## Coverage verified

- Landing page renders, no blank.
- Analyze AAPL: ticker, EV percentage, current price, strategy matrix heading, page body length 2440 chars.
- Analyze nav: `/analysis/AAPL` resolved, active-tab color `rgb(34, 197, 94)`.
- Error path ZZZZZ: heading rendered, Back button present and navigates to `/dashboard`.
- Hunt tab: action button, fixture tickers populated, no error, row click → `/analysis/MSFT`.
- Watchlist API: `POST /api/watchlist` AAPL → 200.
- Watch tab: AAPL/MSFT/UNH rows render with real fixture data (not the "Data refreshing" placeholder Travis flagged on 2026-05-07), remove button works, row click → `/analysis/AAPL`.
- Stripe prices: `/api/stripe/prices` 200, both `price_1TUdOXAy6OYpyg` (standard) and `price_1TUdOYAy6OYpyg` (pro) present.
- Account: FREE tier label, STANDARD + PRO plan cards.
- Mobile 390px: no horizontal overflow.

## Findings

- No regression vs run 4 of 2026-05-09 — run 6's allowlist refactor is invisible to the live UX path as designed (default provider for `/api/analyze` stayed Yahoo; the refactored cache key only matters once `getDefaultPriceDataProvider()` is flipped to prefer Massive, which is held during marketing freeze).
- Watchlist `item.ivRank` still rendered (`IV rank 31/38/46`). Pre-existing pivot integration debt flagged in run 6 of 2026-05-08 deletion-surface audit — not a regression, gated on Cove pass before any visible change ships.

## State

No source-tree changes. No commit. No deploy. No spend. Cash $162.45.

Open gates entering and exiting unchanged:
- `ADS APPEAL: PAF GOOGLE ADS SUSPENDED — APPEAL FILED 2026-05-08`
- `TESTING COMPLETE: STRIKEREWIND DATA-LIVE`

Both are Travis-side. No new gate raised this run.
