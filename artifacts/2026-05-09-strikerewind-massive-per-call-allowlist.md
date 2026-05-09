# StrikeRewind: MassivePriceDataProvider per-call allowlist

**Date:** 2026-05-09 (run 6)
**Branch:** `autobox/strikerewind-rename`
**Commit:** `90a0bd1` pushed to origin
**Files:** `backend/src/services/massivePriceDataProvider.ts`, `backend/src/services/massivePriceDataProvider.test.ts`
**Diff:** +200 / −23

## Why

Standing TODO line — "Rework MassivePriceDataProvider to support a per-call
allowlist so `/api/analyze` can use Massive for the requested ticker only" —
was the only bounded autonomous-runnable code move available without
disturbing Travis's active StrikeRewind testing window: PAF was just
smoked (run 5), StrikeRewind smoke not yet due (~6h since run 4 of today,
cadence ≥12h), nightly cron prune-verification window doesn't open until
tomorrow's 06:00 ET fire, and Watchlist render work is held during the
marketing freeze.

Backend-internal refactor; live `/api/analyze` continues to default to
Yahoo. This commit is the precondition that lets a future run flip the
default safely without re-introducing the OOM that forced `77307a7` to
roll back to Yahoo on 2026-05-08.

## What changed

`MassivePriceDataProvider` cache key changed from `dateKey` to
`${dateKey}|${allowlistSig}`:

- `setTickerAllowlist(tickers)` now also stamps an `allowlistSig`
  (`i:${version}:${size}`). Calling it again invalidates that cohort's
  cache implicitly via the new sig.
- `effectiveFilter(forTicker?)` returns the instance filter if set,
  otherwise `{allowlist: {forTicker}, sig: 't:' + forTicker}` for
  per-call mode.
- `fetchHistoricalChart(ticker, ...)` threads that filter through
  `loadDate` / `primeDateRange`, so a single analyze request can no
  longer materialize the full ~12k-ticker map per day.
- Batch path is preserved: `run-spread-results-batch.ts` still calls
  `setTickerAllowlist(universe)` then `primeDateRange`; both operations
  share the same instance sig and the same cache map.

Constructor accepts an optional `s3?: S3LikeClient` for test injection,
falling back to the real `S3Client` when omitted. Public `S3LikeClient`
type exported for the same reason.

## Tests

7 new tests against a stub S3 client + 5 existing parser/date-helper
tests = 12/12 in this suite.

- `parseDailyCsv` filters rows by allowlist Set
- `parseDailyCsv` returns empty map when allowlist is empty
- Per-call mode fetches only the requested ticker
- Per-ticker caches are isolated between callers
- Repeated fetches for the same ticker hit the cache (single S3 call)
- Instance-allowlist batch mode preserved (single prime + cached reads)
- Tickers outside instance allowlist return `[]`

## Verification

```
npx tsc --noEmit              # clean
npm run build                  # clean
node --test dist/services/massivePriceDataProvider.test.js   # 12/12 pass
node --test dist/services/*.test.js dist/jobs/*.test.js      # 68/68 pass
```

Backend test count: 61/61 → 68/68.

## Live impact

None. `getDefaultPriceDataProvider()` still returns Yahoo;
`/api/analyze` keeps the Yahoo path. The batch script
`run-spread-results-batch.ts` keeps the same call sequence
(`setTickerAllowlist` → `primeDateRange` → per-ticker fetch); the new
sig is set under the hood and the cache map shape per primed file is
identical to before.

Render auto-deploys the branch on push but boots the same code path
the live service used pre-commit.

## Deliberately NOT done

- Did NOT change `getDefaultPriceDataProvider()` to prefer Massive for
  `/api/analyze`. That swap belongs in a later run paired with a live
  Render-side memory probe and a smoke pass; the OOM blast radius was
  large enough that flipping it during Travis's testing window is the
  wrong tradeoff.
- Did NOT touch `run-spread-results-batch.ts`. Existing call sequence
  produces identical cache content under the new sig.
- Did NOT route through Cove or Luke. Backend-internal refactor with no
  customer-visible surface.
- Did NOT raise a new gate. Two open Travis-side gates carried unchanged.

## State files

`TODO.md`, `RUNLOG.md`, `HANDOFF.md`, `SCORECARD.md` updated.
`OPEN_GATES.md` unchanged. `BUDGET.md` unchanged. Cash balance: $162.45.
No spend.
