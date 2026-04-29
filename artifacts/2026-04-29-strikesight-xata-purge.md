# StrikeSight — purge Xata SDK, point all consumers at Supabase

Date: 2026-04-29
Branch: `autobox/strikesight-scanner-mvp`
Commit: `ffdc8ba`

## What changed

Last session migrated the StrikeSight database from Xata to Supabase but left the old `XataDatabaseServiceWithFallback` wrapper in place as a thin alias (importing `SupabaseDatabaseService as XataDatabaseService`). Six files still imported the wrapper, the `@xata.io/client` package was still in `backend/package.json`, the generated `xata.ts` client and old `xataDatabaseService.ts` still existed, and `.env.example` still listed `XATA_API_KEY` / `XATA_DATABASE_URL`. Boot worked, but the surface area was confusing and any new contributor (or future autonomous run) would think Xata was still load-bearing.

This run cut Xata out cleanly:

- Repointed every consumer to `SupabaseDatabaseService.getInstance()` directly:
  - `backend/src/index.ts`
  - `backend/src/services/stripeServiceDB.ts`
  - `backend/src/services/usageServiceDB.ts`
  - `backend/src/services/watchlistServiceDB.ts`
  - `backend/src/services/schedulerService.ts`
  - `backend/src/services/cacheService.ts`
- Added `getFromStorage` / `setInStorage` / `removeFromStorage` to `SupabaseDatabaseService` backed by an in-process `Map`. This preserves the exact behavior the wrapper had — those methods were always in-memory anyway (the wrapper's "would query Xata cache table" comments were never wired up).
- Deleted `backend/src/xata.ts`, `backend/src/services/xataDatabaseService.ts`, `backend/src/services/xataDatabaseServiceWithFallback.ts`.
- Removed `@xata.io/client` from `backend/package.json`; ran `npm install` (one package removed; lockfile updated).
- Replaced `XATA_API_KEY` / `XATA_DATABASE_URL` in `backend/.env.example` with `SUPABASE_URL` / `SUPABASE_SECRET_KEY`.
- Removed tracked Xata codegen directories `.xata/` and `backend/.xata/` (compatibility/version JSON + migration ledger).

Net diff: `18 files changed, 353 insertions(+), 894 deletions(-)`. About 800 lines of dead Xata code removed.

## Verification

- `cd backend && npm run build` → `tsc` passes clean (no errors).
- `cd / (root) && npm run build` → backend `tsc` + frontend `tsc -b && vite build` both pass; `dist/assets/index-BDGG0Dbb.js 445.78 kB`.
- Backend boot test with **only** `SUPABASE_URL` + `SUPABASE_SECRET_KEY` set (no `XATA_*` vars, no `STRIPE_*`, no `SENTRY_DSN`, no `ENABLE_SCHEDULER`):
  ```
  Sentry DSN not found, error tracking disabled
  Scheduler disabled (set ENABLE_SCHEDULER=true to enable)
  StrikeSight backend running on port 3099
  ```
- Existing fixture tests (`huntFixtureMode.test.ts`) pass `3/3`.
- `grep -i "xata\|XATA" backend/src/` returns zero matches.

## Remaining Xata mentions in the repo

Three internal deployment/security docs still mention Xata:
- `DEPLOYMENT.md`
- `HTTPS_DEPLOYMENT_GUIDE.md`
- `SECURITY_AUDIT.md`

Plus one frozen historical artifact under `journal/site/artifacts/`. None of these are user-facing and none load at runtime, but the deployment docs will need a Supabase rewrite before production deploy. Logged in TODO.md.

## Why this was the right next move

The HANDOFF explicitly listed this audit as the first follow-up after the Supabase migration. It's blocking the production deploy: the deploy README still names Xata env vars, the package still pulls a 0.30.x SDK we don't use, and consumers were one-step-removed from the actual database. With this gone, the deploy pipeline reads cleanly: only `SUPABASE_URL` and `SUPABASE_SECRET_KEY` are required to boot, and the only deferred database wiring is Stripe (which is already gated behind `STRIPE_SECRET_KEY` lazy init) and the paid options data provider (still pending owner approval).

The Travis directive was "polish up StrikeSight, then drive traffic." This is part of polish — visible to the next pair of eyes touching the repo (Travis, a future autonomous run, a contractor), and it removes a surface that would create deployment confusion. It cost zero dollars, did not cross any approval gate, and shrinks the change set by ~800 lines.

## Next concrete moves on StrikeSight (in dependency order)

1. Rewrite `DEPLOYMENT.md` and `HTTPS_DEPLOYMENT_GUIDE.md` Supabase sections (small, no approval).
2. Polish landing page copy — route through Luke for the "scans the whole S&P, returns the exact tickers, strikes, and expirations that have been consistently profitable over time" story.
3. On `ROTATED: STRIKESIGHT KEYS READY` from Travis (Xata key rotation in Xata dashboard — independent of the SDK removal above; the leaked key still needs to be invalidated).
4. On `APPROVED: SUBSCRIBE MARKETDATA.APP TRADER ...` — wire real chain data behind the existing scanner.
5. On `APPROVED: BUY STRIKEREWIND.COM, MAX $15` (or `GETSTRIKESIGHT.COM`) — purchase, point DNS.
6. Production deploy — Vercel or Render with Supabase env.
7. Stripe production keys + end-to-end subscription test.

## Owner-side asks (no new approval gate from this run)

- `ROTATED: STRIKESIGHT KEYS READY` (rotate Xata key in Xata dashboard so the leaked key is invalidated)
- `APPROVED: SUBSCRIBE MARKETDATA.APP TRADER ...` (paid options chain data; ~$60/mo or Polygon Starter ~$29/mo equivalent)
- `APPROVED: BUY STRIKEREWIND.COM, MAX $15` (or `GETSTRIKESIGHT.COM`)
- PAF-side: confirm Smart Bidding strategy and total Google Ads spend so far against the `$50` stop-loss

## Cash balance

`$188.75`. No spend this run.
