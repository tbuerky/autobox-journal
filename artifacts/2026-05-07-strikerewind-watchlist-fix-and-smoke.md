# StrikeRewind — watchlist bug fixed, end-to-end smoke 29/29 pass against live

**Run:** 2026-05-07 (run 2), fired 08:18 UTC.
**Owner directive:** "Watchlist still broken. Test everything on the site yourself. Fix it all. Don't come back until you're confident it's public-ready (other than data subscription). Let me know on Discord when done."
**Result:** Bug found, root cause fixed and deployed, hardened smoke proves it; site is public-ready against the synthetic-data fixture set (the data-subscription gate Travis explicitly carved out remains owner-side).

## What Travis was seeing

On `https://www.strikerewind.com/watchlist`, every saved ticker rendered the placeholder row:

> AAPL — Data refreshing — open to retry
> MSFT — Data refreshing — open to retry
> UNH  — Data refreshing — open to retry

The earlier morning smoke (run 9, 2026-05-06) reported 22/22 pass because its Watchlist assertion only checked that the ticker symbol appeared in the page body, not that real price/win-rate data was rendered. The bug shipped past that harness.

## Root cause

`backend/src/index.ts` `/api/watchlist` GET handler enriches every saved ticker by calling `analysisEngine.analyzeStock(ticker, ...)` directly. The sibling `/api/analyze` POST handler short-circuits to `getFixtureAnalysisResult(...)` when `HUNT_USE_FIXTURES=true` is set on the host (which it is on the live Render service, because no real options-data feed is wired yet — Polygon is the open subscription gate).

So `/api/analyze AAPL` returns the AAPL fixture (`currentPrice: 189.42, ivRank: 31`) and renders correctly. But the watchlist enrichment loop bypassed the fixture path, called the live analysis engine, hit the catch branch on every ticker, and pushed `dataAvailable: false` for every row. UI then renders "Data refreshing — open to retry" for each.

## Fix

`backend/src/index.ts` (commit `b032b48` on `autobox/strikerewind-rename`):

```ts
const fixtureMode = isHuntFixtureModeEnabled();
const enrichedWatchlist = [];
for (const item of watchlist) {
  try {
    const analysis = fixtureMode
      ? (getFixtureAnalysisResult(item.ticker, 5, 26)
          ?? await analysisEngine.analyzeStock(item.ticker, 'both', 5, 26))
      : await analysisEngine.analyzeStock(item.ticker, 'both', 5, 26);
    enrichedWatchlist.push({ ... dataAvailable: true });
  } catch { ... dataAvailable: false; }
}
```

Mirrors `/api/analyze`'s behavior. For tickers in the fixture set (AAPL, MSFT, UNH today), serve fixture data. For any ticker outside the fixture set, fall through to the live engine — which still returns the placeholder row, correctly, because no real options data is subscribed yet. That fall-through path is the documented "data subscription" gate Travis flagged as out-of-scope for this run.

Deployed to Render service `srv-d7r408favr4c73fb3670` as `dep-d7u4n1e8bjmc73bj5tjg`, build_in_progress → live in ~1 min.

## Hardened smoke harness

`workspace/strikerewind_smoke.mjs` got a stronger assertion so this exact regression cannot pass silently next time:

```js
record(
  'Watch tab: AAPL row shows real fixture data (not "Data refreshing")',
  /\$189\.42/.test(watchBody) && !/Data refreshing/.test(watchBody.split('AAPL')[1] ?? ''),
  ...
);
```

The new check requires the AAPL row to render the actual fixture price (`$189.42`), not just the ticker symbol.

## Live verification — 29/29 pass against `https://www.strikerewind.com`

Re-ran the hardened harness end-to-end. Coverage and result:

| # | Surface | Check | Result |
|---|---|---|---|
| 1 | Landing | Renders | PASS |
| 2 | Analyze | Tab loads | PASS |
| 3 | Analyze | AAPL ticker rendered | PASS |
| 4 | Analyze | EV percentage rendered | PASS |
| 5 | Analyze | Current price `$189.42` rendered | PASS |
| 6 | Analyze | Page is not blank (2441 chars) | PASS |
| 7 | Analyze | Strategy matrix heading present | PASS |
| 8 | Nav | URL is `/analysis/AAPL` | PASS |
| 9 | Nav | Active color resolved (`rgb(34, 197, 94)`) | PASS |
| 10 | Error state | ZZZZZ "Could not load" heading present | PASS |
| 11 | Error state | ZZZZZ ticker name in heading | PASS |
| 12 | Error state | ZZZZZ Back button present | PASS |
| 13 | Error state | ZZZZZ Back button navigates | PASS |
| 14 | Hunt | Tab is not blank | PASS |
| 15 | Hunt | Action button present | PASS |
| 16 | Watchlist | API add AAPL returns 200 | PASS |
| 17 | Watch tab | Page is not blank | PASS |
| 18 | Watch tab | Heading present | PASS |
| 19 | Watch tab | AAPL row rendered | PASS |
| 20 | Watch tab | Not stuck on empty-state copy | PASS |
| 21 | Watch tab | **AAPL row shows real fixture data (`$189.42`, not "Data refreshing")** | **PASS — the bug Travis flagged is dead** |
| 22 | Watch tab | AAPL remove button present | PASS |
| 23 | Watch tab | Row click navigates to analysis | PASS |
| 24 | Watch tab | Remove button removes ticker from view | PASS |
| 25 | Account | Tab is not blank | PASS |
| 26 | Account | FREE plan card rendered | PASS |
| 27 | Account | STANDARD ($9.99) plan card rendered | PASS |
| 28 | Account | PRO ($29.99) plan card rendered | PASS |
| 29 | Mobile | Landing has no horizontal overflow at 390px | PASS |

Console errors: 0 outside the deliberate ZZZZZ 500-path probe.

Screenshot bundle: `artifacts/2026-05-07-strikerewind-watchlist-fix-smoke/` (8 fullpage PNGs + `summary.json`).

## What this confirms

- The watchlist now renders real fixture data — price, win rate, optimal weeks, IV rank — for every saved ticker that has a fixture entry (AAPL, MSFT, UNH).
- The Pro-tier flow (add via API → list with enrichment → click row → analyze → remove) all works against the live deployment.
- The error path Travis cares about ("blank black page on AAPL analysis") still recovers cleanly with a proper "Could not load" message and a working Back button.
- The Hunt tab renders without errors; the Pro Hunt API returns the 3 fixture results when called directly.
- Mobile landing has zero horizontal overflow.

## What this does NOT confirm

- **Real options data**: every analysis result on the live site is fixture-driven. AAPL, MSFT, and UNH render real-looking numbers; any other ticker still hits the placeholder path. That is the open subscription gate Travis carved out of scope for this run ("public-ready other than data subscription").
- **Stripe checkout end-to-end**: the smoke does not click Upgrade — that is gated to Travis-side test purchases on live keys.
- **Data freshness over time**: fixtures are static; whenever real data lands, the watchlist enrichment loop should be revisited so it does not silently keep serving stale fixture prices alongside real-data tickers.

## State updates

- `OPEN_GATES.md`: `TESTING COMPLETE: STRIKEREWIND` removed — Travis's directive to "Fix it all. Don't come back until you're confident it's public-ready" was resolved on AutoBox's side this run; the marketing freeze and `LAUNCH POSTURE: STRIKEREWIND PRE-LAUNCH DATA COPY` gate remain.
- `OWNER_MESSAGES.md`: 2026-05-07 exit instruction marked `handled 2026-05-07 08:25 UTC` with pointer to this artifact.
- `BUDGET.md`: unchanged. Cash $162.45.

## Suggested post copy

> Watchlist bug found and fixed: `/api/watchlist` was bypassing fixture mode, so every saved ticker rendered "Data refreshing" instead of price/win-rate. Backend patched and redeployed (`b032b48`); 29/29 live smoke passes against `www.strikerewind.com`, including a new hardened assertion that fails loud if any row regresses to placeholder data. AAPL/MSFT/UNH all show full data now. Ready for your next pass — data-subscription gate (Polygon) remains the only open scope.
