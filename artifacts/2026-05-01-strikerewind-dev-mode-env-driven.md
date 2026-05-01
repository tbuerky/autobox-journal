# StrikeRewind: DEV_MODE env-driven (deploy pipeline step 1)

**Date:** 2026-05-01
**Branch:** `autobox/strikerewind-rename`
**Commit:** `d070a8f`
**Status:** Shipped

## Why

Deploy pipeline step 1, queued during the 2026-05-01 interactive session.

`backend/src/services/usageServiceDB.ts:18` was `private readonly DEV_MODE = true` — a hardcoded constant that bypasses every tier limit check. With Render production cold-starts running compiled JS (`a50d8b4`) and tier copy + limits finalized in the same interactive, the only thing left between this branch and a non-broken prod deploy was making this flag flip-able from environment.

If we deploy with the constant still `true`, prod silently gives every visitor unlimited Hunt access — the upgrade wall doesn't exist, no one ever sees a paywall, no revenue path. If we flip it to `false` in source, local dev breaks because Travis's local sessions hit the same limits as prod.

## What changed

Five files, +30 / -23.

### `backend/src/services/usageServiceDB.ts`
```ts
// before
private readonly DEV_MODE = true; // Force unlimited access

// after
// DEV_MODE: when true, bypasses all tier limits. Set DEV_MODE=true in local .env to enable.
// Production (Render) leaves this unset, so prod enforces FREE tier limits as the upgrade wall.
private readonly DEV_MODE = process.env.DEV_MODE === 'true';
```

Strict semantics: only the literal lowercase string `'true'` enables DEV_MODE. Unset, `'false'`, `'TRUE'`, `'True'`, `'1'`, anything else → `false`. Verified via direct node REPL run before commit.

### `backend/.env.example`
Added under server config:
```
# Set DEV_MODE=true locally to bypass all tier limits during development.
# Leave unset in production so FREE tier limits enforce the upgrade wall.
DEV_MODE=false
```

### `DEPLOYMENT.md`
Added under backend env block:
```
# Tier limits enforce in production. DEV_MODE is read in usageServiceDB.ts and
# only enabled when set to the literal string "true" — leave unset on Render.
```

### `frontend/src/pages/Account.tsx` + `frontend/src/pages/LandingPage.tsx`
Tier-copy gate satisfaction (left uncommitted from the interactive). Bundled into the same commit since they're the same logical unit (deploy precondition: tier model and tier-enforcement-flag both correct before Render cold-starts the service).

Tier model finalized:
- **Free**: 3 ticker analyses/day, 1 scan/day (up to 10 tickers), 1yr history, no card. Hunt locked.
- **Standard ($9.99/mo)**: unlimited analyses, unlimited scans (up to 100 tickers), full Hunt, 3yr history, 25-item watchlist.
- **Pro ($29.99/mo)**: everything in Standard + full S&P 500 scans + 5yr history + unlimited watchlist.

Account.tsx feature lists rewritten to match the actual `tierLimits` constants. Landing page FAQ ("What do I need to start?") and closing CTA both updated to "3 ticker analyses a day, 1 scan per day, one year of history."

## Verification

| Check | Result |
|-------|--------|
| `npm run build` (backend) | clean, no type errors |
| `npm run build` (frontend) | clean, 1921 modules, JS 352.81 kB / CSS 23.30 kB (CSS unchanged) |
| Backend tests | `12/12` pass (3 huntFixtureMode + 9 spreadResultsService) |
| `process.env.DEV_MODE === 'true'` semantics | unset→false, 'false'→false, 'true'→true, 'TRUE'→false |
| `git push` | `6321576..d070a8f` on `autobox/strikerewind-rename` |

## What this unblocks

Deploy pipeline can now proceed:
1. ~~Make DEV_MODE env-driven~~ ✓ (this run)
2. Create Render web service via API
3. Set Render env vars (NODE_ENV=production, PORT=10000, SUPABASE_URL/SECRET, STRIPE_SECRET/WEBHOOK, FRONTEND_URL=https://strikerewind.com — DEV_MODE deliberately omitted)
4. Deploy frontend to Vercel under the-shepherd-stack account
5. Point strikerewind.com DNS
6. Set Stripe production keys + webhook
7. Smoke test free-tier flow (this is when DEV_MODE=false actually gets exercised — visitor hits 3 analysis cap, 1 scan cap, Hunt-locked-behind-upgrade)
8. Signal Travis when ready for end-to-end testing

## Public-copy hygiene per RULES.md rule 14/15

Account.tsx + LandingPage.tsx are customer-facing. Reviewed: no internal labels, no SEO scaffolding, no AI-smell, no machine fingerprints, no process language. Sentence-case feature lists match the rest of the page. The "(up to 10 tickers)" / "(up to 100 tickers)" parentheticals match Standard's `maxTickersPerScan: 100` and Free's `maxTickersPerScan: 10` exactly — no overpromise.

## Acted on fresh owner input

No. This is the first step of the deploy pipeline Travis explicitly queued for autonomous runs in the 2026-05-01 interactive HANDOFF entry.

## Cash balance

$162.45. No spend.
