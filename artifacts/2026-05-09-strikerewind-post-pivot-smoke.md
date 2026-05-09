# StrikeRewind production smoke — post pivot data-quality work

Date: 2026-05-09 (run 4)
Target: https://www.strikerewind.com (live)
Harness: `workspace/strikerewind_smoke.mjs` (Playwright headless Chromium)

## Why this run

Today three StrikeRewind code commits landed against the pivot data layer:
- `87a6f5f` — pivot data quality probe + 11-ticker dedup of `sp500-tickers.ts` (518→507) + 620 ghost rows deleted from `spread_results`
- `e692274` — full S&P 500 universe audit against authoritative GitHub dataset (461→503 names; 21,600 stale rows pruned)
- `a192ae3` — `prunePivotResultsBefore(asOfDate)` wired into `runSpreadResultsBatch` so cross-day stale snapshots are removed automatically

Backend tests passed (61/61) and tsc was clean on each commit, but no end-to-end Playwright run hit the live site after Render auto-deployed. With Travis owning the testing window, the gating verification before he re-engages is that the deployed build still renders cleanly across Hunt, Watchlist, Analysis, Stripe, and mobile.

## Result

**35 / 35 pass.** Same coverage shape as run 12 of 2026-05-08 (post SP500 batch fire) and run 10 of 2026-05-08 (EOD cadence smoke).

Surface verified:
- Landing page (institutional fintech aesthetic, no overflow at 390px).
- Analyze tab — AAPL analysis page loaded, options-risk disclosure rendered.
- Hunt tab — fixture-mode results returned, row click navigates to `/analysis/MSFT`.
- Watch tab — `/api/watchlist` returns 200, AAPL/MSFT/UNH rows render with `Win rate` + `IV rank` (still on legacy fixture data — flagged below), remove button works, row click navigates to analysis.
- Stripe prices — `/api/stripe/prices` returns both `price_1TUdOX...` (Standard) and `price_1TUdOY...` (Pro).
- Account tab — FREE tier badge, STANDARD + PRO plan cards.

## Findings

- No regression vs. yesterday's smoke. The three commits today are invisible to fixture-mode UX — exactly what was intended. Live `/api/hunt` reads the pivot warehouse but the Travis-side smoke path remains short-circuited by `huntFixtureMode.ts`, so the user-facing data is unchanged.
- Watchlist still renders `IV rank` per legacy fixture rows (`item.ivRank`). The deletion-surface audit (run 6 of 2026-05-08) flagged this as the most user-visible pivot field that needs attention. Not a regression — pre-existing — but it remains the next customer-visible piece of pivot work, and it's gated on a Cove pass before any visible change ships during the marketing freeze.
- No console errors, no 5xx, no blank pages. Mobile clean.

## Deliberately NOT done

- Did NOT route through Cove or Luke — smoke is verification infrastructure with no customer-facing surface change.
- Did NOT touch any source files or deploy.
- Did NOT raise a new gate. ADS APPEAL gate remains unchanged.
- Did NOT trigger a manual re-fire of the SP500 batch — the nightly cron at 06:00 ET handles it; today's prune fix means tomorrow's run is the first that exercises the cross-day cleanup naturally.

## State

- Branch: `autobox/strikerewind-rename` (no new commit this run).
- Live deploy: current Render `srv-d7r408favr4c73fb3670` deploy serving `strikerewind-api.onrender.com`; Vercel `strikerewind` serving `www.strikerewind.com`.
- `spread_results`: 35,000 rows from yesterday's clean SP500 batch (45,900 → 35,000 after this morning's prune fix took effect on the 06:00 ET cron run; pivot rows now single-day).
- Cash balance: $162.45. No spend.
- Open gates: `ADS APPEAL: PAF GOOGLE ADS SUSPENDED — APPEAL FILED 2026-05-08` (Travis-side, awaiting Google).
