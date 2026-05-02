# StrikeRewind deploy blocked: Render workspace has no payment method

**Date**: 2026-05-02
**Run**: Deploy pipeline step 2 (create Render web service via API)
**Status**: BLOCKED on Travis — owner-only action

## What happened

Tried to create the StrikeRewind backend web service on Render via API per the
`[ACTIVE — DEPLOY PIPELINE]` step 2 in `config/TODO.md`.

Request: `POST https://api.render.com/v1/services` with the configuration from
`artifacts/2026-04-30-strikerewind-deploy-architecture-packet.md` (web_service,
Starter plan $7/mo, repo `https://github.com/tbuerky/StrikeSight`, branch
`autobox/strikerewind-rename`, `rootDir: backend`, env vars: `NODE_ENV=production`,
`PORT=10000`, `SUPABASE_URL`, `SUPABASE_SECRET_KEY`, `FRONTEND_URL=https://strikerewind.com`,
build `npm install --include=dev && npm run build`, start `npm start`,
healthcheck `/api/health`).

Render API responded:

```
{"message":"Payment information is required to complete this request. To add a card, visit https://dashboard.render.com/billing"}
```

The workspace ID on file (`tea-d7qhmmf7f7vs73fc4pk0`, "My Workspace",
travis@theshepherdstack.com) has the API key working — auth is fine, owner ID is
fine, the workspace exists — but no card is on file. Render gates ALL service
creation behind billing setup, even for the $7/mo Starter plan, even for what
would have been a brand-new workspace's first service.

Stripe production keys are also still missing from the deploy env (no
`STRIPE_SECRET_KEY` / `STRIPE_WEBHOOK_SECRET` in `.env`); this is a separate
follow-up that fires after billing is unblocked, since the backend boots
without Stripe (Stripe routes 500 until configured).

## Exact next action — Travis

1. Go to **https://dashboard.render.com/billing**
2. Add a payment method (credit card) for the "My Workspace" workspace
3. Reply: `CARD ADDED: RENDER WORKSPACE` so the next autonomous run can re-fire
   the service-creation API call and continue the deploy pipeline

The next autonomous run after that reply does NOT need any further input from
Travis to complete steps 2–4 of the deploy pipeline (Render service creation
+ env vars + Vercel frontend deploy). Steps 5 (DNS) and 6 (Stripe production
keys + webhook) remain owner-actions; step 7 (smoke test) and 8 (notify Travis)
are AutoBox-runnable once 5 and 6 land.

## Why this matters now

The `[ACTIVE — DEPLOY PIPELINE]` block in TODO.md is the only path to
StrikeRewind revenue. Step 1 (DEV_MODE env-driven) shipped 2026-05-01 commit
`d070a8f`. Step 2 is the next-in-line, and it's hard-blocked. Without a card
on the Render workspace, no autonomous run can move this forward — adding
the card is the single bottleneck on the whole revenue path right now.

## What's NOT blocked

- Pre-deploy quality work continues to be autonomous-runnable (FAQ, methodology,
  metadata, robots.txt, sitemap.xml all already shipped — landing-page +
  pre-deploy chain is substantially complete).
- PAF revenue path is intact, AdSense live, no regressions.
- AI utility properties unchanged.

## Cash impact

None this run — Render rejected the call before any billable resource was
created. Cash balance stays at `$162.45`. When the card lands and the service
deploys, Render Starter plan = `$7/mo` (already pre-approved per closed gate
`APPROVED: DEPLOY ON VERCEL+RENDER STARTER, $7/MO`).

## Artifact files referenced

- `artifacts/2026-04-30-strikerewind-deploy-architecture-packet.md` — full deploy
  architecture and ordered step list
- `config/TODO.md` `[ACTIVE — DEPLOY PIPELINE]` block — canonical step list
- `config/HANDOFF.md` 2026-05-01 INTERACTIVE entry — Travis's queue-deploy-for-autonomous-runs direction
