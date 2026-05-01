# StrikeRewind production deploy — architecture decision packet

**Date:** 2026-04-30
**Status:** Owner-blocking. One approval line at the bottom.
**Cash balance:** $162.45.

## TL;DR

The branch is build-clean and visually correct, but the existing `vercel.json` will not actually deploy a working backend. Recommend **frontend on Vercel (free) + backend on Render Starter ($7/mo)** — matches what `DEPLOYMENT.md` already documents in the repo, lets the scheduler/cron stay in a long-running Node process, and keeps the public landing page on a global CDN. One approval line, ~$7 of recurring spend.

## Why deploy now

The 2026-04-28 product-defining HANDOFF locks production deploy as build-queue step #10 — the last gate between the current code and revenue. Everything upstream of it is shipped:

- Brand pass + favicon (`aca61b0`) — no more "StrikeSight" in the wordmark or header
- Cove tokens + framer-motion strip (`21a9963`) — production JS bundle is `339.67 → 345.52 kB`, no animation library overhead
- Full strategy matrix on `/analysis/:ticker` (`34e8002`) — the activation feature the landing page promises
- Luke landing copy (`eddc21f`) — "stop selling 30-delta on every ticker" voice locked
- Account.tsx Cove pass (`a26b588`) — billing surface matches landing tone
- Supabase migration (`ffdc8ba`) — Xata gone, Supabase wired in
- Tier model resolved (Free/Standard/Pro at $0/$9.99/$29.99 per Travis 2026-04-30)

There are no remaining autonomous code steps that materially change deploy-readiness. The next move is to put the product on a public URL.

## What's broken in the current `vercel.json`

`vercel.json` at the StrikeSight repo root declares the Express backend as a single Node 18 serverless function:

```json
"functions": { "backend/src/index.ts": { "runtime": "nodejs18.x" } },
"rewrites": [{ "source": "/api/(.*)", "destination": "/backend/src/index.ts" }]
```

This will not work as-is:

1. `backend/src/index.ts:720` ends with `app.listen(PORT, ...)` — Vercel serverless functions expect a default-exported handler, not a long-lived Express server. The function will boot, the `app.listen` call will silently bind a port that Vercel never routes to, and every `/api/*` request will time out or 500.
2. `backend/src/index.ts:713-717` starts `node-cron` schedulers for nightly options data fetches (9:30 AM ET / 6:00 AM ET per `schedulerService.ts`). Serverless functions are stateless — cron jobs won't fire because the process doesn't exist between invocations.
3. `nodejs18.x` is past Vercel's deprecation window. Latest is `nodejs22.x` (or `nodejs20.x`). Even if the rest worked, the deploy would fail on runtime selection.
4. `express-rate-limit` keeps in-memory state per process. With serverless cold starts, the rate limit would reset on every request, defeating the limiter.

This config has never been deployed. Fixing it before first deploy is cheaper than deploying-then-debugging.

## Architecture options

### Option A — Frontend on Vercel + Backend on Render Starter ($7/mo) — RECOMMENDED

| Surface | Host | Plan | Cost | Why |
|---|---|---|---|---|
| Frontend (`/`, `/dashboard`, `/hunt`, `/analysis/:ticker`, `/watchlist`, `/account`) | Vercel | Hobby | $0 | Static React build, global CDN, Git-integrated auto-deploy on push to `autobox/strikerewind-rename`. |
| Backend (`/api/*`) | Render | Starter | $7/mo | Persistent Node process, supports `node-cron`, no cold starts, $0.013/hr if scaled to zero, $7/mo flat for always-on. |

**Total recurring:** $7/mo / $84/yr — within the standing budget posture.

**Why this over the alternatives:**
- The repo's own `DEPLOYMENT.md` recommends this split (lines 6-30) — it's the path the codebase was already designed for.
- Vercel free tier gives the public landing page sub-100ms first-paint globally — institutional-fintech aesthetic + global CDN is the credibility lever for a credit-spread tool.
- Render's Starter plan is the cheapest tier that supports the persistent scheduler. Render Free spins down after inactivity and would kill the nightly cron.
- Two URLs: `strikerewind.com` (Vercel) + `api.strikerewind.com` (Render). Stripe webhook → backend domain only. Clean separation.
- No code changes needed before deploy — the existing Express server already exposes `/api/*`, and the frontend already reads `VITE_API_URL`. Need to fix `vercel.json` and `frontend/.env.production` (both stale), but no source-tree refactoring.

### Option B — Render monolith ($7/mo)

All on Render: backend serves both the React static bundle and `/api/*`. Same $7/mo. Simpler ops surface (one URL, one DNS record, one log stream), but:
- Lose Vercel's global CDN — public landing page first-paint goes from ~50ms (Vercel edge) to ~300-500ms (Render origin).
- Need to add `app.use(express.static(...))` + an SPA catchall to `backend/src/index.ts` (~5 lines) — small, but a code change before deploy.
- Less standard for the React + Vercel ecosystem; harder to hand off later.

### Option C — Vercel-only with serverless backend rewrite

Refactor the entire backend into individual `/api/*.ts` serverless functions, replace `node-cron` with Vercel Cron Jobs, replace `express-rate-limit` with a Vercel-friendly limiter, and split the scheduler into separate cron functions. **High engineering cost** (multi-day refactor), no cost savings vs Option A, breaks the "one Express app" mental model the codebase is built around. Not recommended.

### Option D — Stay on a single VPS (DigitalOcean droplet)

The autobox.theshepherdstack.com VPS (DigitalOcean, `165.227.204.19`) is already provisioned. Could host both frontend and backend via Nginx + systemd. **No marginal spend** if it shares the existing droplet. But: introduces ops surface AutoBox doesn't currently maintain (TLS cert renewal, log rotation, deploy scripts), and the VPS is currently scoped to AutoBox's own state/journal infra — colocating a real customer-facing product on it raises blast radius. Not recommended for first deploy; reasonable later if Render cost ever becomes a concern.

## What Travis owns under Option A

1. **Sign up at https://render.com** with the GitHub identity that has access to `tbuerky/StrikeSight`. Connect the repo. Approve Render's `read` access to `autobox/strikerewind-rename`.
2. **Add a payment method to Render** (Starter is `$7/mo` flat, billed monthly).
3. **Click "New Web Service"**, point at `tbuerky/StrikeSight` branch `autobox/strikerewind-rename`, set:
   - Root Directory: `backend`
   - Build Command: `npm install --include=dev && npm run build`
   - Start Command: `npm start`

   (`--include=dev` is required because `NODE_ENV=production` is in env at install time and the build needs `typescript` + `@types/*`, which now live in `devDependencies`. Without it the install would skip them and `tsc` would fail. Runtime then uses `tsx`, which is in `dependencies`.)
   - Plan: Starter ($7/mo)
4. **Paste backend env vars from a kit AutoBox prepares** (Supabase prod URL + secret key, Stripe test publishable + secret + price IDs, Sentry DSN, `ENABLE_SCHEDULER=true`, `NODE_ENV=production`, `FRONTEND_URL=https://strikerewind.com`).
5. **Confirm the Render service URL** (something like `strikerewind-api.onrender.com`) and reply with it.
6. **Add DNS records** in the StrikeRewind.com registrar (Porkbun, where the domain was bought 2026-04-28):
   - `CNAME api → strikerewind-api.onrender.com`
   - `A @ → 76.76.21.21` (Vercel) — apex domain
   - `CNAME www → cname.vercel-dns.com`

Travis-side time: ~20 minutes if everything is cached in browser; ~40 if first time on Render.

## What AutoBox does after approval

One run, single commit, no parallel surprises:

1. Fix `vercel.json` — drop the broken `functions` + `rewrites` block, leave only the static frontend config.
2. Update `frontend/.env.production` — set `VITE_API_URL=https://api.strikerewind.com`, `VITE_APP_NAME=StrikeRewind`, replace stale Stripe placeholder with the real `pk_test_*` for first deploy.
3. Backend `start` script is `node dist/index.js` (production-correct, runs the compiled JS that `npm run build` emits to `dist/`). Verified pre-deploy 2026-05-01 — `NODE_ENV=production npm install --omit=dev` followed by `node dist/index.js` boots cleanly with only Supabase env vars set.
4. `vercel link` against the existing `the-shepherd-stack` Vercel team, set Vercel env vars (Supabase URL + anon key), `vercel deploy --prod`.
5. Once Render webhook + Stripe webhook URLs are in env, smoke-test the live `/` (loads landing), `/api/health` (returns 200), Supabase auth signup flow.
6. Hand back the live URL and a verification checklist.

Stripe stays in **test mode** for first deploy. Live keys are a separate gate later — first deploy is "is the box on the public internet and rendering correctly", not "can a real card charge."

Polygon stays **not subscribed**. Hunt scanner returns fixture data via `HUNT_USE_FIXTURES=1` so the activation flow ("sign up → run hunt → see results → confirm on /analysis/:ticker") is end-to-end navigable on the live URL. Real options data is its own gate (`APPROVED: SUBSCRIBE POLYGON STARTER, $29/MO`) when entering pre-launch testing.

## What this packet is NOT

- Not a request to wire Stripe live keys. That's a later gate after at least one signup flows clean on test mode.
- Not a request to subscribe Polygon. That's a separate gate when fixture data is no longer enough.
- Not a request to publicly announce the launch. Public posting under Travis's identity is its own approval.

## Cost summary

| Item | Recurring | One-time |
|---|---|---|
| Render Starter (backend) | $7/mo | — |
| Vercel Hobby (frontend) | $0 | — |
| StrikeRewind.com (already owned) | $0 | $11.25 (paid 2026-04-28) |
| **Total recurring** | **$7/mo** | — |

Cash balance after first month: `$162.45 → $155.45`. Twelve-month runway at this burn: 22+ months from current balance, before any revenue.

## Suggested post copy:

```
Production deploy is the last gate to revenue on StrikeRewind. The current vercel.json declares the Express backend as a Node-18 serverless function, but the backend has app.listen() and node-cron schedulers — it can't actually run that way.

Recommend frontend on Vercel (free) + backend on Render Starter ($7/mo). Matches the architecture DEPLOYMENT.md already documents. Total recurring: $7/mo. Stripe stays in test mode for the first deploy; Polygon stays unsubscribed (Hunt runs on fixtures).

Travis-side: sign up Render, connect tbuerky/StrikeSight, point DNS for api.strikerewind.com → Render and apex strikerewind.com → Vercel. ~20-40 min. Full Travis-side checklist + AutoBox follow-up steps in artifacts/2026-04-30-strikerewind-deploy-architecture-packet.md.

Reply: APPROVED: DEPLOY ON VERCEL+RENDER STARTER, $7/MO
```

## Single approval line

**APPROVED: DEPLOY ON VERCEL+RENDER STARTER, $7/MO**
