# StrikeRewind end-of-day production smoke — 2026-05-07 20:17 UTC

## Result
**29 / 29 PASS · 0 FAIL · 0 unfiltered console errors**

Identical pass-content to run 2's hardened smoke at 08:17 UTC — no day-over-day regression on the live revenue site.

## Cadence
- Last hardened smoke: run 2 of 2026-05-07 at 08:17 UTC (29/29).
- This run: 20:17 UTC, exactly clears the ≥12h cadence window run 7's handoff queued.
- Target: `https://www.strikerewind.com` (Vercel) and `https://strikerewind-api.onrender.com` (Render).

## What the harness covered
- **Landing**: renders, screenshot captured.
- **Analyze tab golden path**: navigate `/dashboard`, type `AAPL`, hit Enter, wait for `/api/analyze` POST, assert ticker + EV percentage + price `189.42` + body length, "Strategy matrix" heading, nav highlight on `/analysis/AAPL`.
- **Analyze error path**: navigate `/analysis/ZZZZZ`, assert "Could not load" heading + ticker echo + Back button + Back navigates to `/dashboard`. Console-error filter accepts the deliberate 500 from `/api/analyze` for the nonsense ticker.
- **Hunt tab**: page renders ≥300 chars, action button present.
- **Watch tab full mutation flow**: pre-clean via API, add `AAPL` via API (`x-user-id: travis-pro-tester`, status 200), navigate `/watchlist`, assert heading + AAPL row rendered with real fixture price `$189.42` (regression assertion against the "Data refreshing" placeholder bug Travis hit), remove button present, row click navigates to `/analysis/AAPL`, remove button removes the row.
- **Account tab**: page renders ≥200 chars, FREE tier label, STANDARD plan card with `9.99`, PRO plan card with `29.99`. (Did not click Upgrade — live Stripe.)
- **Mobile 390px**: landing renders, `scrollWidth - clientWidth = 0` (no horizontal overflow).

## Bundle
- `artifacts/2026-05-07-strikerewind-eod-smoke/` — 8 fullpage PNG screenshots + `summary.json` (29 pass entries, 0 fail, 0 unfiltered console error).

## Notes
- The `STRIPE PRICES: STRIKEREWIND PRICE IDS MISSING` gate (raised run 7) does NOT surface in this smoke. Account tab plan-card prices come from frontend hardcoded `$9.99` / `$29.99` display copy, not from `/api/stripe/prices`. The smoke deliberately avoids the upgrade button so the missing-price-IDs bug doesn't get tripped here. Future run will land a regression assertion on that bug AFTER Travis answers `APPROVED: STRIPE PRICES: STRIKEREWIND` and the env vars land — the assertion would fail today.
- Trust-proxy fix (run 5) holds: 0 ValidationError occurrences in the analyze-tab path during this run.
- Post-rate-limit-hardening run 5 confirmed no client IP issues today; this smoke ran clean from a single IP and no rate-limit shedding surfaced.

## Cash balance
$162.45 (Render starter ~$0.23/day accruing toward end-of-cycle invoice).
