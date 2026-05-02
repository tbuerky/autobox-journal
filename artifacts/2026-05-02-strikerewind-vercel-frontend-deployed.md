# StrikeRewind frontend deployed to Vercel — 2026-05-02

## What shipped
- Vercel project `strikerewind` created under `travis-4599s-projects` (the-shepherd-stack account).
- Production deployment `dpl_2ep9LU5FSy1fA76TbMMUf5Tav4vR` is live (`READY`).
  - Primary URL: `https://strikerewind-dy2xyp3mr-travis-4599s-projects.vercel.app`
  - Vercel alias: `https://strikerewind.vercel.app`
  - Inspector: `https://vercel.com/travis-4599s-projects/strikerewind/2ep9LU5FSy1fA76TbMMUf5Tav4vR`
- Backend at `https://strikerewind-api.onrender.com` is `live`, `/api/health` returns `200 {"status":"ok"}`.
- `frontend/.env.production` updated: `VITE_API_URL=https://strikerewind-api.onrender.com` (was stale `https://api.strikesight.com`); Stripe key set to `pk_test_placeholder` until production keys land. File is gitignored — values committed via Vercel project env vars instead (see below).
- Root `vercel.json` rewritten to a frontend-only static config; previous serverless backend declaration would never have booted (Express `app.listen` + `node-cron`, not a handler). Commit `5d27cfc` pushed to `autobox/strikerewind-rename`.

## Vercel env vars set (production scope)
- `VITE_API_URL=https://strikerewind-api.onrender.com`
- `VITE_APP_NAME=StrikeRewind`
- `VITE_APP_VERSION=1.0.0`
- `VITE_STRIPE_PUBLISHABLE_KEY=pk_test_placeholder`
- `VITE_ENABLE_HUNT=true`
- `VITE_ENABLE_PAYMENTS=true`

## Smoke-test results (Vercel preview URL)
- `GET /` → HTTP 200, 2286 bytes, `<title>StrikeRewind — Credit spread optimizer</title>` ✓
- `GET /robots.txt` → HTTP 200, sitemap pointer present ✓
- `GET /sitemap.xml` → HTTP 200, 3 `<url>` entries ✓
- `og:url` content is `https://strikerewind.com/` (matches DNS target).

## What does NOT work yet (expected, gates raised)
- Authenticated / Hunt / Stripe flows: backend `FRONTEND_URL=https://strikerewind.com` is set to the apex DNS target, not the Vercel preview URL. End-to-end browser auth + CORS will fail at the `*.vercel.app` URL but will work at `strikerewind.com` once DNS lands.
- Stripe routes 500 until production keys land in Render env.

## Deploy pipeline status (TODO.md `[ACTIVE — DEPLOY PIPELINE]`)
| Step | Status | Notes |
|------|--------|-------|
| 1. DEV_MODE env-driven | done 2026-05-01 (`d070a8f`) | |
| 2. Render service created | done 2026-05-02 (`srv-d7r408favr4c73fb3670`) | |
| 3. Render env vars set | done 2026-05-02 | 5 vars in same call |
| 4. Vercel frontend deploy | **done this run** (`dpl_2ep9LU5FSy1fA76TbMMUf5Tav4vR`) | |
| 5. DNS records | **owner action** | gate raised this run |
| 6. Stripe production keys | **owner action** | gate raised this run |
| 7. DEV_MODE off + smoke test | autonomous after step 5+6 | |
| 8. Notify Travis ready for E2E test | autonomous after step 7 | |

## Gates raised this run

### `DNS RECORDS: STRIKEREWIND`
At the strikerewind.com registrar, add three records:
- `A @ → 76.76.21.21` (Vercel apex)
- `CNAME www → cname.vercel-dns.com` (Vercel www)
- `CNAME api → strikerewind-api.onrender.com` (Render backend custom subdomain)

After DNS propagates, AutoBox attaches `strikerewind.com`, `www.strikerewind.com`, and `api.strikerewind.com` as custom domains via the Vercel and Render APIs (no further owner action).

Discord reply expected: `DNS UPDATED: STRIKEREWIND`.

### `STRIPE PROD KEYS: STRIKEREWIND`
In Stripe Dashboard:
1. Generate live API keys for the StrikeRewind account (`pk_live_*` + `sk_live_*`).
2. Create a webhook endpoint pointed at `https://api.strikerewind.com/api/webhooks/stripe` (or the Render direct URL `https://strikerewind-api.onrender.com/api/webhooks/stripe` until DNS lands). Copy the signing secret (`whsec_*`).
3. Reply with all three values.

AutoBox follow-up: set `STRIPE_SECRET_KEY` + `STRIPE_WEBHOOK_SECRET` in Render env, set `VITE_STRIPE_PUBLISHABLE_KEY` in Vercel env, redeploy frontend.

Discord reply expected (with values redacted in HANDOFF after handling):
`STRIPE PROD KEYS: STRIKEREWIND <pk_live_…> <sk_live_…> <whsec_…>`.

## What this unblocks
With the frontend live on Vercel and backend live on Render, the StrikeRewind product is one DNS update + one Stripe key drop away from a production-quality URL that real users can hit. Both remaining gates are owner-only mechanical actions; AutoBox can finish the remaining four pipeline steps deterministically once they land.
