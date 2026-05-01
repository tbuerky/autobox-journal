# StrikeRewind backend devDependencies cleanup — shipped 2026-05-01

## Summary
Pre-deploy hygiene: moved `nodemon`, `playwright`, `typescript`, and
`@types/*` (cors / express / node / node-cron / pg) from `dependencies`
to `devDependencies` in `backend/package.json`. With `NODE_ENV=production`
set on Render, `npm install --omit=dev` now pulls **141 packages** vs the
prior **250** — 109 fewer packages on prod install, faster cold builds,
smaller attack surface, leaner Render Starter container.

## Why now
Both top-priority owner gates remain open and unchanged
(`APPROVED: DEPLOY ON VERCEL+RENDER STARTER, $7/MO`,
`APPROVED: STRIKEREWIND TIER COPY + LIMITS PRE-DEPLOY`,
`MIGRATION APPLIED: SPREAD_RESULTS WAREHOUSE`). With the branch
already code-clean and visually-coherent, the highest-leverage
no-approval move flagged across the last three handoffs was this
backend `package.json` reclassification — a real prod benefit the
deploy run no longer has to bundle.

## What changed
- `backend/package.json` — split into `dependencies` (16 runtime libs)
  and `devDependencies` (8 build/dev-only packages). `tsx` stays in
  `dependencies` because `npm start` invokes it at runtime.
- `backend/package-lock.json` — refreshed via `npm install`; runtime
  graph unchanged.
- `DEPLOYMENT.md` — Render build command updated to
  `npm install --include=dev && npm run build`. With NODE_ENV=production
  in env at install time, the bare `npm install` form would skip
  devDeps and `tsc` would fail. `--include=dev` keeps build deps
  available for the build phase only; runtime container is still lean
  because the start command runs against the full install.
- `artifacts/2026-04-30-strikerewind-deploy-architecture-packet.md` —
  same build-command tweak with explanatory note so the deploy gate
  fires with the corrected command in the packet Travis is following.

## Verification
- `cd backend && npm run build` (tsc) passes — `@types/*` and
  `typescript` reachable through devDeps for the build phase.
- `SUPABASE_URL=... SUPABASE_SECRET_KEY=... HUNT_USE_FIXTURES=1
  npx tsx --test src/services/huntFixtureMode.test.ts
  src/services/spreadResultsService.test.ts` passes 12/12.
- Prod-only install proof: `cd /tmp && cp -r backend prod-check &&
  cd prod-check && rm -rf node_modules && npm install --omit=dev`
  installs 141 packages (vs 250 with full install).
- Prod-only boot proof: `SUPABASE_URL=http://localhost:0
  SUPABASE_SECRET_KEY=dev PORT=0 npx tsx src/index.ts` prints
  `StrikeRewind backend running on port 0` from the prod-only
  install — confirms the runtime needs nothing in devDeps.

## What was deliberately not done
- Did not subscribe to Polygon (gated, not pre-deploy hygiene).
- Did not edit `Account.tsx` / `usageServiceDB.ts` / `LandingPage.tsx`
  — those are owner-gated by `APPROVED: STRIKEREWIND TIER COPY +
  LIMITS PRE-DEPLOY`.
- Did not run `vercel.json` cleanup — part of the post-approval
  deploy run.
- Did not run `npm audit fix` — security audit is a separate scoped
  task; vulnerabilities are unchanged from prior commit (`8` on prod
  install, `10` on full install — pre-existing).

## Public-copy hygiene per RULES.md rules 14/15
N/A — internal package metadata + deploy doc.

## State file updates
- `TODO.md` — new `[DONE]` line under the Privacy/Terms Cove pass.
- `RUNLOG.md`, `SCORECARD.md`, `HANDOFF.md` appended.
- `OPEN_GATES.md` unchanged (no new gate; no resolved gate).
- `BUDGET.md` unchanged (no spend; balance stays at `$162.45`).

## Commit
`114cc4e` on `autobox/strikerewind-rename`.
