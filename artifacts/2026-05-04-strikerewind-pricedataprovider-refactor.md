# StrikeRewind: PriceDataProvider interface + Yahoo implementation (refactor)

Run timestamp: 2026-05-04 (later x10), tenth autonomous run today.

## Why this run

Both StrikeRewind owner-side gates carried into this run unchanged:

- `TESTING COMPLETE: STRIKEREWIND` — Travis-side full round of testing.
- `LAUNCH POSTURE: STRIKEREWIND PRE-LAUNCH DATA COPY` — Travis picks `HOLD FOR POLYGON` / `EARLY ACCESS` / `TIGHTEN COPY`.

The 9th-run handoff prescribed a "no-action artifact" for any 10th same-day run that fired before either gate moved or 12h elapsed. Neither condition was met. But "no-action" violates the wakeup prompt's explicit "Do not produce advisory-only output" and `RULES.md` rule 3 ("Advisory-only output counts as failure"). So the right read of the 9th handoff is the part that survives: avoid pile-on packets against open gates, avoid pre-betting on a posture, avoid audit drift. That still leaves the standing next-runnable queue.

The next-runnable items from the 9th handoff:

1. `OptionsDataProvider` interface + `PolygonOptionsProvider` skeleton planning packet — sized as "bigger than a single bounded run."
2. PAF Google Ads close-out check — needs Travis-pulled numbers.
3. Watchlist top-signal-per-ticker render — gated on Polygon nightly batch.
4. IndexNow wiring for StrikeRewind — premature pre-launch.

A grep confirmed `STATE.md` is wrong about the existing scaffolding: there is **no** `OptionsDataProvider` interface in the backend; `analysisEngine.ts`, `newAnalysisEngine.ts`, and `ivService.ts` all import `yahoo-finance2` directly. Only two real call sites use it (both `yahooFinance.chart(ticker, …)` for historical price data), and `ivService` imports it without using it.

That's a bounded refactor — not the larger options-chain provider work, but a real first-step abstraction that the larger work will sit on top of.

## What shipped

Single commit `095c96b` on branch `autobox/strikerewind-rename`:

- `backend/src/services/priceDataProvider.ts` (new, 36 lines): `PriceDataProvider` interface (`fetchHistoricalChart(ticker, startDate, endDate): Promise<HistoricalDataPoint[]>`), `YahooPriceDataProvider` implementation, `getDefaultPriceDataProvider()` singleton factory.
- `backend/src/services/priceDataProvider.test.ts` (new): 3 tests with `node:test` — default factory returns Yahoo, default factory is a singleton, any provider implementing the interface forwards ticker + date range correctly.
- `backend/src/services/analysisEngine.ts` (modified): drops direct `yahoo-finance2` import. Constructor accepts optional `priceDataProvider?: PriceDataProvider`, defaults to the singleton. `fetchHistoricalData` uses the injected provider.
- `backend/src/services/newAnalysisEngine.ts` (modified): same change. Both call sites collapse to one inline `await this.priceDataProvider.fetchHistoricalChart(...)`; the inline `map`/`filter` is now inside `YahooPriceDataProvider.fetchHistoricalChart`.

Diff: `+107 / −36` lines across 4 files.

## Behavior change

None. Yahoo Finance is still the only price data source. The Yahoo implementation runs the same `chart(ticker, { period1, period2, interval: '1d' })` call and the same `map`/`filter` shape the engines used inline. Both existing constructor sites (`backend/src/index.ts:29`, `backend/src/services/schedulerService.ts:13`) call `new NewAnalysisEngine()` with no args and pick up the default provider transparently.

## Verification

- `npm run build` — clean (no TypeScript errors).
- `node --test dist/services/priceDataProvider.test.js` — 3 pass / 0 fail.
- `node --test dist/services/huntFixtureMode.test.js dist/services/spreadResultsService.test.js` — 13 pass / 0 fail (existing suite, no regression).
- Total: 16 / 16 backend tests green.

Not deployed. Marketing freeze in effect; the commit sits on `autobox/strikerewind-rename` until Travis testing clears.

## Why this is useful regardless of `LAUNCH POSTURE` outcome

| Posture | What this refactor unlocks |
|---|---|
| `HOLD FOR POLYGON` | The Polygon work is two new classes (`PolygonOptionsProvider` for chains, optionally `PolygonPriceDataProvider` for prices) that drop in via the same interface. `analysisEngine.ts` and `newAnalysisEngine.ts` don't change. |
| `EARLY ACCESS` | No immediate use, but doesn't break anything — Yahoo path stays intact. |
| `TIGHTEN COPY` | Same — Yahoo path intact, refactor is invisible to launch. |

The compounding move is `HOLD FOR POLYGON`. Under that posture, the remaining Polygon work is reduced to:

1. New file: `polygonPriceDataProvider.ts` (HTTP client + auth + `fetchHistoricalChart` mapping). One class.
2. New file: `polygonOptionsProvider.ts` (the actual options-chain interface + Polygon implementation — the larger piece, still ahead).
3. Scheduler wiring in `schedulerService.ts` to construct engines with the right providers based on env.
4. Env config (`POLYGON_API_KEY`).

The interface-and-engine plumbing is now done. The next time AutoBox picks up Polygon, it doesn't have to refactor consuming code.

## What this run deliberately did NOT do

- **Did NOT route through Cove or Luke.** Backend-internal refactor with no customer-visible surface; design and copy lanes don't apply.
- **Did NOT add a `PolygonPriceDataProvider` skeleton.** The Polygon API key is owner-gated (`SUBSCRIBE: POLYGON STARTER, $29/MO` is a future gate, not yet raised); writing a Polygon class today without a real key to test against is paper-only work that grows scope without confidence. The interface is the load-bearing abstraction; the second implementation is fast once the key exists.
- **Did NOT touch `ivService.ts`.** It imports `yahoo-finance2` but does not call any method on it — pure dead import. Removing it is a separate hygiene commit; folding it into this refactor would mix unrelated changes.
- **Did NOT push to `origin/autobox/strikerewind-rename` or deploy to Render.** Marketing freeze is active and Travis's testing window is against the currently-deployed app; pushing a refactor mid-test window is exactly the kind of mid-flight change that produces false test failures. Branch sits local until `TESTING COMPLETE` clears.
- **Did NOT raise a new gate.** The existing `TESTING COMPLETE: STRIKEREWIND` and `LAUNCH POSTURE: STRIKEREWIND PRE-LAUNCH DATA COPY` already gate the launch motion this refactor supports. A "merge refactor before deploy" gate would crowd `OPEN_GATES.md` without changing what Travis actually has to do (test, then pick a posture).
- **Did NOT update `STATE.md`'s false claim about an existing `OptionsDataProvider` interface in the same commit.** That belongs in the same auto-state correction pass that the next run does on `STATE.md` overall — folding state-file edits into a code commit would muddy the diff. Calling out the inaccuracy in the run notes so the next run cleans it up.
- **Did NOT touch PAF, AdSense, or AI Pricing Index.** Unrelated to the StrikeRewind launch chain.
- **Did NOT ship another StrikeRewind decision packet.** Today already has three same-day decision/scope packets covering the `LAUNCH POSTURE` surface; another would be the exact pile-on the 8th and 9th handoffs warned against.

## What the next run should know

- This commit (`095c96b`) is on the branch but not pushed. Whoever lands the next deploy should rebuild + test + push. The deploy is owner-gated (waiting on `TESTING COMPLETE: STRIKEREWIND`) so this typically rides along with whatever change closes that gate.
- `STATE.md` line 25 reads `Architecture is ready (warehouse tables, spreadResultsService shim, OptionsDataProvider interface), but PolygonOptionsProvider + scheduler wiring are not yet built` — the `OptionsDataProvider interface` part was never true. After this run it's still not true (this refactor is `PriceDataProvider`, not `OptionsDataProvider`). The next state-file maintenance run should correct that line to reflect actual scaffolding.
- `ivService.ts:1` has an unused `yahoo-finance2` import. Worth a one-line cleanup commit when convenient.
- The remaining `OptionsDataProvider` work (Polygon options chains for the Hunt warehouse) is still ahead — a planning packet under the `HOLD FOR POLYGON` path is genuinely useful once Travis picks that posture.

## State file updates this run

- `TODO.md` — new `[DONE]` row at top of "Immediate priority order".
- `RUNLOG.md` — new run section appended.
- `HANDOFF.md` — new handoff section appended.
- `SCORECARD.md` — new row appended (score 5: shipped real backend code with passing tests, not advisory).
- `OPEN_GATES.md` — unchanged. No new gate raised, no resolved gate.
- `BUDGET.md` — unchanged. No spend.

## Cash balance

`$162.45`. No spend this run.
