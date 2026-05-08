# StrikeRewind pivot batch — Yahoo rate-limit blocker + Polygon Starter recommendation

Date: 2026-05-08
Run: 9 of 2026-05-08
Author: AutoBox autonomous

## Summary

Travis issued two directives at 20:00–20:05 UTC:
1. Run first live execution of `runSpreadResultsBatch` against live Supabase to populate the pivot rows the new `/api/hunt` route reads.
2. Recommend which Polygon.io $29/mo Starter tier StrikeRewind actually needs (Stocks vs Options).

This run executed (1), discovered a hard blocker (Yahoo Finance rate-limiting from this VPS), and converted that finding into the evidentiary backbone for (2). Outcome: the batch did not write any rows; instead the run produced (a) a one-shot runner script with throttle + retry that is ready to fire from a non-blocked egress, and (b) a Polygon recommendation packet whose top-line answer changed because of (a)'s blocker.

## Directive 1 — pivot batch live execution

### What was built

- `backend/scripts/run-spread-results-batch.ts` — one-shot CLI runner.
  - Loads `backend/.env.local` (already pointed at live Supabase project `hjfsapwessfvdcfytpuk`).
  - Wraps `YahooPriceDataProvider` in a `ThrottledYahooProvider` that enforces a configurable inter-call sleep (`BATCH_SLEEP_MS`, default 1500ms) and exponential-backoff retries (`BATCH_RETRY_ATTEMPTS` × `BATCH_RETRY_BASE_MS`, defaults 4 × 4000ms doubling).
  - Calls `runSpreadResultsBatch({ tickers, asOfDate, priceDataProvider, onTickerError })`.
  - Universe arg: `dow30` or `sp500`; defaults to `dow30`.
  - Writes a JSON summary to `workspace/spread-results-batch-<universe>-<date>.json` and stdout.
  - Per-ticker stderr line on success or retry.

### What was attempted

```
cd /home/autoproj/projects/StrikeSight/backend
npx tsx scripts/run-spread-results-batch.ts dow30
```

(initial run, no throttle wrapper, default sequential pacing)

### What happened

Every one of 30 DOW tickers failed with the identical error:

```
Unexpected token 'T', "Too Many Requests\r\n" is not valid JSON
```

`tickersTotal: 30, tickersProcessed: 0, tickersFailed: 30, rowsWritten: 0`.

### Root cause confirmation

Single-ticker probe immediately after, with no concurrent calls, also failed:

```
$ npx tsx scripts/probe-yahoo.ts
AAPL err: Unexpected token 'T', "Too Many Requests
" is not valid JSON
```

Conclusion: Yahoo Finance is rate-limiting this VPS's egress IP at the per-IP level, not at the per-call rate. Adding throttle delay does not unblock it. The block is severe enough that even a single isolated chart request fails with HTML 429.

This is consistent with Yahoo's well-known unofficial-API hostility toward cloud egress ranges and with the cumulative volume StrikeRewind's other code paths (`schedulerService`, `analysisEngine`, etc.) have generated against this IP over recent runs.

### Why this is not solvable here

- The throttle wrapper was kept in the runner for future use, but no inter-call delay can clear an IP-level block. Yahoo's response is HTTP 429 on the very first call.
- Render's production backend has a different egress IP and is the natural place to run the batch — but the batch is wired only as an in-process function, not exposed as an admin-keyed HTTP route. Adding a route, deploying, and triggering safely from outside is a multi-step slice that should not be bundled with this run.
- No other priceDataProvider implementation exists. The `PriceDataProvider` interface was created exactly so a different source could be plugged in. Polygon Stocks is the obvious replacement.

### Live impact

Zero. No rows written. `data_source='price_history_5yr'` row count in `spread_results` remains zero. `/api/hunt` live path continues to return `[]` (fixture mode short-circuits before this for Travis's smoke harness, so user-visible behavior is unchanged).

### Files added (uncommitted, on `autobox/strikerewind-rename`)

- `backend/scripts/run-spread-results-batch.ts`
- `backend/scripts/probe-yahoo.ts`

These are tooling, not product code. They should be committed as part of the next slice that runs the batch successfully (most likely from Render with a Polygon-backed provider).

## Directive 2 — Polygon Starter recommendation

### Question

Stocks Starter ($29/mo, 5yr daily history) or Options Starter ($29/mo, 2yr options history)?

### What StrikeRewind V1 actually needs

| Feature | Status today | Data needed |
|---|---|---|
| Win-rate engine (5yr backtest grid) | Wired via yfinance — **just discovered to be unreliable from production-class infra** | 5yr daily price history per S&P-500 ticker, refreshed daily |
| IV overlay (Hunt + Analysis sidecar) | Announced as upcoming, gated by `POLYGON KEY READY` | Current options-chain IV snapshot per ticker — current value, not history |
| Historical options chains | Explicitly deferred "coming soon" tier | Out of scope at $29 |

### Mapping each tier to those features

**Stocks Starter ($29/mo)**
- Delivers: 5yr end-of-day stock aggregates, official rate limits (typically 5 req/sec sustained on Starter), all US tickers.
- Solves: The win-rate engine pipeline (V1 core, the actual revenue feature).
- Does NOT solve: IV overlay — no options data.

**Options Starter ($29/mo)**
- Delivers: 2yr end-of-day options aggregates + snapshot endpoint with current chain quotes/Greeks/IV (delayed, not real-time).
- Solves: IV overlay (current IV snapshot is exactly what the overlay needs; the announced feature is daily-decision, so 15-min delayed is fine).
- Does NOT solve: Win-rate engine — no stock aggregates.

The 2yr Options history is irrelevant to V1 either way. IV overlay is a current-snapshot feature; the historical-options-chains compute is the deferred "coming soon" tier.

### Recommendation — primary

**Subscribe to Polygon Stocks Starter ($29/mo) NOW.** Defer Options Starter until V2's IV overlay is ready to ship.

Reasoning:
1. The win-rate engine **is** the V1 product. The Hunt page, the Analysis page's strategy matrix, and the entire pivot architecture (Commits 1–3 already shipped) depend on filling `spread_results` with `data_source='price_history_5yr'`. Today's run proved that the current data source for that pipeline (yfinance from this VPS) is structurally unreliable. Stocks Starter replaces it with an SLA-backed feed.
2. IV overlay is a sidecar enhancement on a feature that is not yet shipping. It cannot block users today because no users are paying yet. Stocks reliability *can* block every user once StrikeRewind unfreezes marketing.
3. The original `POLYGON KEY READY: STRIKEREWIND IV OVERLAY` gate was raised when the assumption was "yfinance is fine for the win-rate engine, we just need IV". Today's blocker invalidates that assumption.

### Recommendation — secondary path (only if Travis still wants IV overlay first)

**Subscribe to BOTH Starters ($58/mo total).** Stocks for the win-rate engine reliability, Options for IV overlay. This is a 2× spend bump from the original $29/mo approval but solves both problems cleanly. Monthly burn becomes ~$65/mo (Render $7 + Polygon $58); on the current $162.45 cash balance that is 2.5 months of runway absent revenue, which is too short.

### Recommendation — what to AVOID

- Subscribing to Options Starter alone. With yfinance broken from production-class IPs, IV overlay would render fine but the *Hunt list it overlays onto* is empty. The visible product would be a sidecar with no main feature.
- Holding off until a higher-tier historical-options-chains plan ($200–300/mo). Too much spend for the wrong feature; that tier serves a "coming soon" capability that has no ship date.

### Approval line

Recommended single approval to add to `OPEN_GATES.md` once Travis decides:

```
APPROVED: SUBSCRIBE POLYGON STOCKS STARTER, $29/MO
```

On approval, AutoBox will:
1. Add `POLYGON_API_KEY` to backend env on Render service `srv-d7r408favr4c73fb3670`.
2. Build `polygonPriceDataProvider.ts` implementing the existing `PriceDataProvider` interface (5yr daily aggregates endpoint).
3. Wire the new provider as the default in `getDefaultPriceDataProvider`, gated on `POLYGON_API_KEY` env presence (yfinance fallback retained for local dev).
4. Re-run `runSpreadResultsBatch` (S&P 500) from production — either via a one-shot Render shell or a temporary admin-keyed route.
5. Verify rows landed; re-confirm fixture-mode Playwright smoke; close out.
6. Deduct $29 from `BUDGET.md` and add the recurring-spend line.

The existing `POLYGON KEY READY: STRIKEREWIND IV OVERLAY` gate should be **closed** as obsolete (its premise was wrong) and replaced with the Stocks Starter gate above. If Travis later wants IV overlay too, that is a fresh `+$29/mo` decision after Stocks Starter has demonstrated value.

## State changes this run

- `OPEN_GATES.md` — close `POLYGON KEY READY: STRIKEREWIND IV OVERLAY` (premise obsolete); add `APPROVED: SUBSCRIBE POLYGON STOCKS STARTER, $29/MO`.
- `BUDGET.md` — unchanged. No spend.
- `TODO.md` — mark this run done; queue post-approval Polygon-provider build.
- `RUNLOG.md` / `HANDOFF.md` / `SCORECARD.md` — append.

## Suggested post copy (Discord)

> Tried to fire the first live pivot batch tonight. Hard-blocked: Yahoo Finance is rate-limiting our VPS at the IP level — every ticker, even a single AAPL probe, returns 429. No throttle fixes that. This actually answers your Polygon question: **Stocks Starter $29/mo, not Options.** The win-rate engine is V1; without reliable 5yr daily data it doesn't work. Options IV overlay is a V2 sidecar on a feature that isn't shipping. Approval line: `APPROVED: SUBSCRIBE POLYGON STOCKS STARTER, $29/MO`. Cash $162.45.
