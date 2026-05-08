# StrikeRewind — MassivePriceDataProvider wired (S3 flat-files)

Date: 2026-05-08
Run: autonomous run 11 of 2026-05-08
Owner directive: 2026-05-08T20:30:38+00:00 — Travis subscribed to Massive (rebranded Polygon) and asked AutoBox to build the provider as `massivePriceDataProvider.ts` against the S3 flat-files model rather than per-ticker REST.

## What shipped

Commit `9a1e69d` on `autobox/strikerewind-rename`, pushed to `origin`.

1. `backend/src/services/massivePriceDataProvider.ts` — S3-backed `PriceDataProvider`. Lazy-fetches each daily flat-file once into an in-memory `Map<ticker, DailyRow>`, then serves every ticker for that day from the cached map. `primeDateRange(startDate, endDate, concurrency=8)` prefetches a date window in parallel for batch use. `fromEnv()` returns `null` when `MASSIVE_*` vars are unset, so local dev still falls through to Yahoo.
2. `backend/src/services/priceDataProvider.ts` — `getDefaultPriceDataProvider()` now prefers Massive when env present, Yahoo otherwise. Existing tests untouched.
3. `backend/scripts/run-spread-results-batch.ts` — picks Massive when available, calls `primeDateRange` for the 5yr window up front, then runs the per-ticker loop against the cache.
4. `backend/scripts/probe-massive.ts` — single-ticker live S3 smoke runner.
5. `backend/scripts/probe-yahoo.ts` — committed alongside (carried over from run 9 tooling).
6. `backend/src/services/massivePriceDataProvider.test.ts` — 5 deterministic tests covering CSV header order, blank-line skip, missing-column throw, and the inclusive UTC date iterator.
7. `@aws-sdk/client-s3 ^3.1045.0` added to `backend/package.json`.

## Render env vars set

Pushed via Render API to service `srv-d7r408favr4c73fb3670` earlier in this run (HTTP 200 on each PUT):

- `MASSIVE_ACCESS_KEY_ID`
- `MASSIVE_SECRET_ACCESS_KEY`
- `MASSIVE_S3_ENDPOINT=https://files.massive.com`
- `MASSIVE_S3_BUCKET=flatfiles`

Render auto-deploys on push to `autobox/strikerewind-rename`, so the new commit will roll the four env vars into a live build.

## Live data verification

Probed the bucket directly with the supplied credentials before writing any code. Top-level prefixes confirmed: `global_crypto/ global_forex/ us_futures_* us_indices/ us_options_opra/ us_stocks_sip/`. Stocks layout: `us_stocks_sip/{day_aggs_v1, minute_aggs_v1, quotes_v1, trades_v1}/`.

Daily aggregate path: `us_stocks_sip/day_aggs_v1/YYYY/MM/YYYY-MM-DD.csv.gz`.
File size: ~300KB gzipped, ~12k tickers per file.
CSV header: `ticker,volume,open,close,high,low,window_start,transactions`.

End-to-end probe via `scripts/probe-massive.ts AAPL 2026-05-01 2026-05-07`:
- 5 bars returned (Mon–Fri; weekends skipped server-side and client-side).
- First bar: 2026-05-01 close 280.14, volume 79.9M. Last bar: 2026-05-07 close 287.44.
- 5 day-files cached, 0 missing.

## Architecture decision: flat-files over REST

The supplied credentials are S3-only — they don't authenticate to the REST API. More importantly, the win-rate engine wants a fixed 5yr daily window for ~500 S&P tickers nightly. That's two access patterns:

- REST: 500 tickers × 1260 trading days = 630k rows. At Massive Stocks Starter, that's 500 individual GET requests, each pulling its own 5yr range. Per-ticker latency × 500.
- Flat-files: 1260 daily GETs, each ~300KB. Each file fans out to all 500 tickers. ~378MB total, downloadable in parallel in a couple of minutes.

The flat-file model is strictly better for the batch architecture and matches Travis's instruction. The provider implements the existing `PriceDataProvider` interface so it's a drop-in replacement.

## Test + typecheck

- `npx tsc --noEmit` — clean.
- `npx tsx --test src/**/*.test.ts` — 58/58 pass (was 53; +5 new Massive tests).

## What this does NOT do

- **Did not fire `runSpreadResultsBatch` against S&P 500.** That's the next slice. The batch fires from Render egress (or a cron-triggered job), populates `spread_results` with `data_source='price_history_5yr'`, and turns `/api/hunt`'s pivot path from `[]` into real win-rate rows. The current run already burned meaningful budget building the provider; the batch fire deserves its own run with attention to cost (5y × ~1260 daily files × ~300KB ≈ 378MB of S3 GETs) and to the Render service memory ceiling on starter plan.
- **Did not delete legacy IV / `analysisEngine` code.** Per run 8's audit those are dead-code candidates but their removal is a separate concern.
- **Did not change Travis's fixture-mode smoke path.** `HUNT_USE_FIXTURES=true` is unchanged on Render; `/api/hunt` short-circuits to fixtures in production exactly as before.

## Cost note

Massive Stocks Starter $29/mo recurring spend now active. Logged to `BUDGET.md`. Render starter $7/mo continues. Total recurring: $36/mo.

## Next-run prescription

When this run's deploy completes (Render auto-deploy on `9a1e69d`), the next eligible move is to fire `runSpreadResultsBatch` from a Render shell or admin-keyed route, verify rows landed in `spread_results` with sane win-rate distribution, then re-confirm Travis's 35/35 fixture-mode Playwright smoke. No new gate is needed — Travis already authorized the live execution in directive 1 (2026-05-08T20:00).

## Cash balance

`$162.45` cash + new $29/mo Massive recurring spend (first invoice end of cycle). Render starter still accruing $7/mo.
