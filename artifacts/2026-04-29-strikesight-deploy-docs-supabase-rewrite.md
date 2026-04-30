# StrikeSight deploy docs Supabase rewrite

Date: 2026-04-29
Branch: `autobox/strikesight-scanner-mvp`
Commit: `965c543`

## Why now
Travis priority shift puts StrikeSight on the build → polish → deploy → market path. Step #1 of the locked HANDOFF queue (Supabase `spread_results` warehouse SQL) is gated on Travis applying SQL via dashboard; step #6 (full delta × DTE matrix) needs a backend payload change too risky to bundle one-shot.

A real deploy blocker was already on TODO.md as autonomous-runnable:
> [TODO] StrikeSight: rewrite `DEPLOYMENT.md` and `HTTPS_DEPLOYMENT_GUIDE.md` Supabase sections (currently still reference XATA_API_KEY / XATA_DATABASE_URL; small, no approval needed; do this before production deploy).

After the Xata SDK purge (commit `ffdc8ba`, 2026-04-29) the codebase no longer uses Xata, but the two deploy docs still listed `XATA_API_KEY` / `XATA_DATABASE_URL` in their production env-var examples and credited Xata for automatic backups. If Travis (or AutoBox post tier-model-approval) followed those docs verbatim, the production backend would boot with no database connection and `SupabaseDatabaseService.getInstance()` would throw on first call.

## What changed

**`DEPLOYMENT.md`** (2 edits):
- Backend `.env` example block: replaced `XATA_API_KEY=your_production_xata_key` + `XATA_DATABASE_URL=your_production_database_url` with `SUPABASE_URL=https://your-project-ref.supabase.co` + `SUPABASE_SECRET_KEY=your_supabase_service_role_key` (matches `backend/.env.example`); added Supabase Dashboard URL pointer.
- "Backup & Recovery → Database" bullet: replaced "Xata provides automatic backups" with the accurate Supabase split — Pro tier ships daily automated backups with 7-day retention; Free tier does not, so the operator runs scheduled `pg_dump` against the Supabase connection string. Also kept the "test restore procedures" reminder.

**`HTTPS_DEPLOYMENT_GUIDE.md`** (1 edit):
- Production backend `.env.production` example: replaced `XATA_API_KEY=your_production_api_key` + `DATABASE_URL=your_production_database_url` with `SUPABASE_URL=https://your-project-ref.supabase.co` + `SUPABASE_SECRET_KEY=your_supabase_service_role_key`.

## Deliberately NOT changed
- `SECURITY_AUDIT.md` — incident report describing the leaked Xata key (`xau_ncIRLvD0ac8cIczjxF0vZbHzW6nCArva4`) that Travis still needs to rotate (`ROTATED: STRIKESIGHT KEYS READY` open gate). Frozen historical record; rewriting it would obscure the incident.
- `journal/site/artifacts/2026-04-26-strikesight-scanner-mvp-verification.md` — frozen verification artifact in the journal site; not a deploy doc.
- `STRIPE_STANDARD_PRICE_ID` / `STRIPE_PRO_PRICE_ID` env vars in `DEPLOYMENT.md` — left as-is. These map to the current Stripe Dashboard products (`Standard $9.99` / `Pro $29.99`). When Travis approves `TIER MODEL: FREE/PRO/ULTRA` the Stripe products get renamed to `Pro $29` / `Ultra $99` and AutoBox repoints env in the same deploy run. Until that approval lands, the deploy docs match the live Stripe configuration.

## Verification
```
$ cd /home/autoproj/projects/StrikeSight && grep -nE 'Xata|XATA|DATABASE_URL' DEPLOYMENT.md HTTPS_DEPLOYMENT_GUIDE.md
(no matches)
```

`backend/.env.example` was the source of truth for variable names — `SUPABASE_URL` + `SUPABASE_SECRET_KEY` — verified before the rewrite.

No code touched; no build changes; no fixture-test impact.

## Public copy hygiene
Internal docs, not customer-facing. RULES.md rule 14/15 do not apply, but every line still reads as accurate operator-facing instruction with no AutoBox/run-process scaffolding.

## State
- `OWNER_MESSAGES.md`: no fresh owner input handled this run.
- `BUDGET.md`: no spend; current cash balance remains $162.45.
- `OPEN_GATES.md`: unchanged. Existing gate `TIER MODEL: FREE/PRO/ULTRA APPROVED` still pending; no new gate raised.
- `TODO.md`: deploy-docs Supabase rewrite line marked DONE.
- `RUNLOG.md` / `HANDOFF.md`: appended.
- `SCORECARD.md`: appended.

## What this unblocks
After Travis (a) replies `TIER MODEL: FREE/PRO/ULTRA APPROVED`, (b) renames Stripe products in Dashboard, and (c) rotates the Xata API key (`ROTATED: STRIKESIGHT KEYS READY`), AutoBox can run a single autonomous deploy session that points the StrikeRewind.com DNS at Vercel, sets the production env vars per these now-correct docs, and ships. No third deploy-doc rewrite needed mid-deploy.
