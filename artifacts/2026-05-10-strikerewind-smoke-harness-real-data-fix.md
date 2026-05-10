# StrikeRewind smoke harness — real-data mode fix (run 10 of 2026-05-10)

## Why this run

22:17 UTC. Both open gates Travis-side (`TESTING COMPLETE: STRIKEREWIND DATA-LIVE`), all autonomous cadence windows closed (next StrikeRewind smoke window 2026-05-11 02:17 UTC, next PAF EOD 10:18 UTC, nightly cron prune-verification 06:00 UTC). Run 9 of 2026-05-10 at 20:17 UTC documented a no-action rationale; doing a second back-to-back no-action would violate the artifact-or-blocker rule. Took a small bounded harness-hardening slice instead.

## What I found while building the slice

Started by adding a `/api/health` assertion to `workspace/strikerewind_smoke.mjs` — that was the original intended slice. The first run of the updated harness against `https://www.strikerewind.com` then surfaced a real live regression: **6 of 38 assertions failed**. Travis is in active testing window, so this is the highest-priority work — investigated immediately.

Live probe of `https://strikerewind-api.onrender.com/api/analyze` returned a real Massive-backed payload (`currentPrice: 293.32`), not the fixture price ($189.42) the harness was asserting. Live page screenshot showed the Analyze page rendering correctly with the real price, full strategy matrix, and disclaimer. **The frontend was fine; the harness was wrong.** The cause is environmental, not code: fixture mode is no longer triggered by `userId=travis-pro-tester` in production. Real data flows end-to-end (confirmed against `/api/analyze` curl + Playwright page render). Most likely Travis flipped a `FIXTURE_MODE` env off in Render to do his data-live testing pass — exactly the gate the open gate `TESTING COMPLETE: STRIKEREWIND DATA-LIVE` is waiting on.

The previous "35/35 pass" runs (runs 1, 4, 6 of 2026-05-10) likely ran while the env was still set; this run is the first to fire after the flip, which is why the regression surfaced here.

## What I changed

All edits in `workspace/strikerewind_smoke.mjs`:

1. **`networkidle` → `domcontentloaded` everywhere.** Production pages poll `/api/usage` and `/api/watchlist/tickers` continuously, so networkidle never settles within 30s. Every navigation now waits for `domcontentloaded` plus an explicit selector or content-readiness check. Fixed the watchlist timeout that was failing the whole harness.
2. **Replaced fixture-specific value assertions with structural assertions.**
   - `bodyText.includes('189.42')` → `/\$\d+\.\d{2}/.test(bodyText)` (any `$xx.xx`).
   - `/\$189\.42/.test(watchBody)` → `/\$\d+\.\d{2}/.test(aaplSlice)` (real price next to AAPL).
   - Hunt fixture-ticker check (`/AAPL|MSFT|UNH/`) → ticker-pattern check on the rows after the `TICKER` column header (any S&P 500 ticker is valid in real-data mode).
   - Analyze percentage regex `\d+\.\d%` → `\d+\.\d+%` (real payload has 2.05%, not 2.0%).
   - Watch tab "is not blank" threshold lowered from 200 → 120 chars (real-data layout is more compact).
3. **Added `/api/health` assertion block** (the originally-intended slice). Catches env-wipe / startup breakage as the first regression signal — same class as the 2026-05-07 incident.
4. **Added explicit content-readiness waits** on Analyze (`/\$\d+\.\d{2}/`) and Watchlist (`/AAPL[\s\S]*?\$\d+\.\d{2}/`) so the harness doesn't race the API.

## Verification

`node workspace/strikerewind_smoke.mjs` against `https://www.strikerewind.com`:

```
Summary: 38 pass / 0 fail
```

Coverage now confirmed against real Massive-backed data:
- Landing render
- Analyze AAPL: ticker rendered, percentage rendered (real `+2.05%`), current price rendered (real `$293.32`), strategy matrix heading, nav active color
- Error state ZZZZZ: "Could not load" heading, ticker name, Back button, Back navigation
- Hunt: action button, results returned (real ticker rows present after `TICKER` header — first row `GEV`), no error, result-row navigation to `/analysis/GEV`
- Watch: API add 200, tab non-blank, heading, AAPL row rendered, real price `$293.32` (not "Data refreshing"), remove button, row click navigates, remove flow
- API health: 200, `status=ok`, `version=1.0.1`
- Stripe prices: 200, standard + pro price IDs present
- Account: FREE tier label, STANDARD plan card, PRO plan card
- Mobile landing: zero horizontal overflow

Artifact bundle: `workspace/artifacts/2026-05-10-strikerewind-playwright-smoke/` (`summary.json` + 9 screenshots).

## Why this is the right slice

- **High leverage during the testing-complete gate.** Travis is doing live-data testing right now. A smoke harness that fails on real-data mode is worse than useless — it would either page false-positive every run, or train me to ignore the failures. Fixing it restores the regression-detection layer protecting Travis's testing pass.
- **Bounded.** Test-only change; no production code touched; no commit pushed; no deploy; no spend; no new gate.
- **Marketing-freeze-safe.** Doesn't touch customer-visible surface.
- **Surfaces a real product observation.** AAPL with default window settings (5 yr, max 6w) shows "No viable strategies" in the strategy block — the top viable strategies returned by `/api/analyze` are all at 24-week timeframe and are filtered out by the 6-week max-DTE default. Not a bug per se; flagging for Travis as a likely UX paper cut his testing will hit.

## Open observations for Travis / next run

- If Travis's testing window includes "AAPL Analyze with default settings shows No viable strategies" — that's by design (default 6w max excludes all 24w+ EV-positive strategies from the rendered top block). Strategy matrix still renders the full grid. Worth considering whether to raise the default max-DTE or hint at "try a longer window" more prominently in the top block.
- `FIXTURE_MODE` env (or its equivalent) is now off in Render for `userId=travis-pro-tester`. This is consistent with the testing gate being live — do not flip back on without owner direction.

## No new gate

The single open gate `TESTING COMPLETE: STRIKEREWIND DATA-LIVE` is unchanged. No new gate raised.

## Cash

$162.45 unchanged. No spend.
