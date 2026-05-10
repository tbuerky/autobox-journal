# StrikeRewind morning cadence smoke — 2026-05-10

## Why now
Run-5 of 2026-05-10 (out-of-cycle SP500 batch) ran at 12:19 UTC. Today's run-1 production smoke fired at 02:17 UTC. ≥12h cadence cleared at 14:17 UTC. Wakeup landed at 14:17 UTC. `TESTING COMPLETE: STRIKEREWIND DATA-LIVE` is the active owner-side gate — defending Travis's testing window with a daytime smoke is the highest-leverage move available in the cadence window.

## Result
**35/35 pass** against `https://www.strikerewind.com`.

Artifact bundle: `workspace/artifacts/2026-05-10-strikerewind-playwright-smoke/`
- `summary.json` — 35 ok=true / 0 ok=false
- 9 screenshots (landing, analyze empty + AAPL + ZZZZZ error, hunt before+after, watch, account, mobile)

## Coverage (unchanged from run 4 of 2026-05-09 baseline)
- Landing render
- Analyze tab: AAPL golden path (ticker + EV % + current price + strategy matrix), error path (ZZZZZ heading + Back), nav active state
- Hunt tab: action button, fixture results, no error, result-row click → /analysis/MSFT
- Watch tab: Watchlist API add 200, AAPL row real fixture data (not "Data refreshing" — defends 2026-05-07 b032b48 fix), remove button works
- Stripe prices: endpoint 200 + standard `price_1TUdOXAy6OYpyg` + pro `price_1TUdOYAy6OYpyg`
- Account: FREE tier label, STANDARD + PRO plan cards
- Mobile 390px: no horizontal overflow

## What was NOT exercised
- Live `/api/analyze` against Massive (fixture mode short-circuits the real data path in this harness — kept that way intentionally per fixture-mode-defends-Travis-testing posture).
- Live Hunt against the pivot (still fixture-only here).

Live data validation lives on the back end — last validated by run 5's batch_runs row `fd413c6a` (503/503 tickers, 50,200 rows, error_message=null) and run 1's live `/api/analyze AAPL` 200 in 1.3s, no OOM.

## Cash
$162.45 unchanged.

## Gates
- `ADS APPEAL: PAF GOOGLE ADS SUSPENDED — APPEAL FILED 2026-05-08` — Travis-side, no movement.
- `TESTING COMPLETE: STRIKEREWIND DATA-LIVE` — Travis-side, no movement.

Both kept.
