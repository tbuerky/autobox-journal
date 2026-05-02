# StrikeRewind backend deployed to Render

**Date**: 2026-05-02
**Run**: Deploy pipeline steps 2 + 3 (create Render web service + set env vars)
**Status**: SUCCESS — service created, first deploy in progress

## What shipped

`POST https://api.render.com/v1/services` returned `201 Created`. The
StrikeRewind backend is now a live Render web service:

- Service ID: `srv-d7r408favr4c73fb3670`
- Service URL: `https://strikerewind-api.onrender.com`
- Dashboard: `https://dashboard.render.com/web/srv-d7r408favr4c73fb3670`
- Slug: `strikerewind-api`
- Plan: `starter` ($7/mo, pre-approved gate `APPROVED: DEPLOY ON VERCEL+RENDER STARTER, $7/MO`)
- Region: `oregon`
- Runtime: `node`
- Repo: `https://github.com/tbuerky/StrikeSight`
- Branch: `autobox/strikerewind-rename` @ commit `aa7b3d9` (latest)
- Root dir: `backend`
- Build command: `npm install --include=dev && npm run build`
- Start command: `npm start` (now `node dist/index.js` per 2026-05-01 commit `a50d8b4`)
- Health check: `/api/health`
- Auto-deploy: `yes` (commits to `autobox/strikerewind-rename` trigger redeploys)
- First deploy ID: `dep-d7r408navr4c73fb3790`, status `build_in_progress` at 18:19 UTC

## Env vars set on the service (5/5)

| Key | Source |
|---|---|
| `NODE_ENV` | `production` (literal) |
| `PORT` | `10000` (literal, matches Render's required port) |
| `SUPABASE_URL` | from `backend/.env.local` (project `hjfsapwessfvdcfytpuk`) |
| `SUPABASE_SECRET_KEY` | from `backend/.env.local` |
| `FRONTEND_URL` | `https://strikerewind.com` (literal) |

`STRIPE_SECRET_KEY` and `STRIPE_WEBHOOK_SECRET` deliberately omitted — backend
boots without them; Stripe routes 500 until configured. Travis must generate
production keys in the Stripe Dashboard and provide them in a separate gate
once the frontend is up and the webhook URL is known.

## Reproducer

`workspace/render_create_service.py` — single-shot Python script that loads
`RENDER_API_KEY` from the AutoBox `.env`, `SUPABASE_URL` and
`SUPABASE_SECRET_KEY` from `backend/.env.local`, and posts the documented
payload. Re-run it only after a clean `DELETE /v1/services/<id>` if the
service ever needs rebuilding from scratch.

## Pipeline status

- ✓ Step 1 (DEV_MODE env-driven) — 2026-05-01 commit `d070a8f`
- ✓ Step 2 (Render web service) — this run
- ✓ Step 3 (Render env vars) — this run, bundled into the create call
- ⬜ Step 4 (Vercel frontend deploy) — autonomous-runnable next, no gate
- ⬜ Step 5 (DNS for `strikerewind.com`) — owner action at registrar
- ⬜ Step 6 (Stripe production keys + webhook) — owner action
- ⬜ Step 7 (DEV_MODE off, end-to-end smoke test) — autonomous-runnable
- ⬜ Step 8 (notify Travis for end-to-end testing) — autonomous-runnable

## Cash impact

No charge fires today — Render billed by the second on Starter plan, but the
first invoice for this workspace will land at the end of the current billing
cycle. Effective new spend rate: `$7/mo` ≈ `$0.23/day`. Pre-approved.

## What the next autonomous run does

Either:
1. If the build succeeded: deploy the frontend to Vercel under
   `the-shepherd-stack` account with `VITE_API_URL=https://strikerewind-api.onrender.com`
   (the temp Render URL, until DNS lands on `api.strikerewind.com`); land step 4.
2. If the build failed: fetch `GET /v1/services/srv-d7r408favr4c73fb3670/deploys/dep-d7r408navr4c73fb3790`
   and the build logs endpoint, diagnose, push a fix commit to
   `autobox/strikerewind-rename`, auto-deploy fires.

## What needs Travis when

Two new owner-gates queued for after the frontend is live (deliberately not
raising them today — they would crowd "Waiting on" with actions Travis can't
take until the next autonomous run lands the frontend):

- DNS records at the strikerewind.com registrar (`A @ → 76.76.21.21`,
  `CNAME www → cname.vercel-dns.com`, `CNAME api → strikerewind-api.onrender.com`)
- Stripe production secret key + webhook secret (after webhook URL exists)
