# StrikeSight `/dashboard` rebuild — top signal + watchlist quick-view + Run Hunt CTA

**Date**: 2026-04-29
**Branch**: `autobox/strikesight-scanner-mvp`
**Commit**: `8c43089`
**Repo**: https://github.com/tbuerky/StrikeSight

## Why this run
Step #4 (routing restructure + LandingPage shell) and step #5 (Luke landing-copy polish) shipped on 2026-04-29. After step #5, `/` now reads as a polished public landing page that promises a "scan whole S&P, ranked by win rate and EV per ticker" workflow — but `/dashboard`, the post-signup landing for that flow, was still the legacy `Home.tsx` ticker-analysis launcher (popular ticker buttons + High IV stocks modal + recent analyses list). A user who clicked `Start free` from the landing page was being dumped onto a screen that didn't match what they were sold.

HANDOFF locks the spec for the rebuild: "today's top signal + watchlist quick-view + Run Hunt CTA". This is the post-signup activation surface — the second-most-important screen after `/hunt`. Per Travis priority shift quote, the conversion lever is "telling the story" (scans whole S&P, returns tickers/strikes/exps that have been consistently profitable). The dashboard has to deliver on that story the moment a fresh signup hits it, otherwise the polished landing page is doing all the work alone.

## What shipped

`frontend/src/pages/Home.tsx` rewritten end-to-end (`+295 / -266`).

**Header**: small `Dashboard` eyebrow + H1 `What the scan found, and what you're watching.` Tier badge in the corner styled with Cove tokens (no more emerald glow chips).

**Top signal panel** (`.panel-elevated`):
- Reads `localStorage.getItem('huntResults')` — the same cache `Hunt.tsx` already writes (1-hour TTL) — and surfaces the highest-EV result. No new API call from the dashboard, no heavy scan on dashboard mount, no rate-limit risk.
- Shows ticker (JetBrains Mono via `font-mono`) + company name (from `getCompanyName`), strategy display via `formatStrategyDisplay`, three labeled stat columns (Win rate / EV / Credit) with `.num` everywhere and `text-pos` on EV.
- Primary CTA `Confirm on {ticker}` → `/analysis/{ticker}` (this is the Hunt → Analysis workflow tie-in Luke wrote into the landing page; the dashboard now embodies it).
- Secondary `See all results` → `/hunt`.
- "Refreshed N min ago" stamp computed from cache timestamp; clicking it re-reads localStorage so a fresh hunt run in another tab updates here.
- Empty state (no cache): `Run a hunt to see the spread that scored highest on win rate and expected value across the S&P 500.` + `Run a hunt` CTA.

**Watchlist quick-view** (`.panel`):
- Calls `getWatchlist()` once on mount for tiers where `limits.canSaveWatchlist` is true.
- Shows up to 5 tickers, each row: star icon (`text-accent`), ticker (`font-mono`), price (`.num`), success rate (`.num`), optimal weeks, arrow.
- Empty state: `Star a ticker from any analysis page to follow it here. Each morning you'll see the top current setup for every name on your list.` + `Find candidates in Hunt` CTA.
- Free-tier state: `Watchlist is part of the paid tier. Upgrade to follow specific tickers and get a daily heads-up when a new spread clears your filters.` + `See plans` link to `/account`. Honest framing — matches the digest-only language Luke shipped on the landing page (no realtime alert claim, no notification system, since none is implemented in `backend/src/services/`).
- Cleanup-handles cancellation if the component unmounts mid-fetch.

**Run Hunt CTA** (`.panel`): plain card, name + one-line description + primary `Open Hunt` button. Picks up the tail-end of the dashboard for the user who just refilled context and wants to run a fresh scan.

Both `framer-motion` import and the `<motion.div>` / `AnimatePresence` blocks (the legacy popular-ticker fade-in and the High IV modal animation) are gone. Dashboard renders without any animation library — consistent with the Cove direction and with `Hunt.tsx` (already framer-motion-free) and `LandingPage.tsx` (built without framer-motion).

## What was deliberately not bundled
- Polygon options data wiring (gated on `APPROVED: SUBSCRIBE POLYGON STARTER, $29/MO` — separate step).
- Supabase `spread_results` warehouse table (gated on Travis applying SQL via the dashboard — separate step).
- Ticker Analysis full delta × DTE matrix rebuild (step #6 — separate task).
- Luke pass on the dashboard copy. Dashboard is post-signup authenticated UI, not public-facing copy in the SEO sense; copy strings are short headers + empty-state explanations, written cleanly per Luke's voice (no internal labels, no SEO scaffolding, no AI-smell). When StrikeSight goes public, a Luke pass on every authenticated screen is its own deploy-prep run.
- Any markup-layer changes to legacy components on other routes (Watchlist, Account, Analysis, etc.). Those each need their own Cove + Luke passes; outside the scope of "rebuild /dashboard."
- Auth wall (`UserContext` defaults everyone to PRO tier in dev — both Sign in and Start free CTAs route to `/dashboard` which is fine pre-auth; Stripe + auth wall is its own deploy step).

## Verification
- `cd frontend && npm run build` passes. Bundle `dist/assets/index-C76eA7X-.js 450.75 kB` (down `-4.08 kB` from last run; fewer framer-motion subscriptions on this page) / CSS `26.32 kB`.
- `cd backend && npm run build` (tsc) passes.
- `SUPABASE_URL=http://localhost:0 SUPABASE_SECRET_KEY=dev HUNT_USE_FIXTURES=1 npx tsx --test src/services/huntFixtureMode.test.ts` passes `3/3`.
- `git diff --stat HEAD~1` confirms only `frontend/src/pages/Home.tsx` changed: `295 insertions(+), 266 deletions(-)`.
- Public-copy hygiene: no internal labels, no SEO/process scaffolding, no notes-to-self; numeric cells use `.num`, ticker uses `font-mono`, EV uses `text-pos`, surfaces use `.panel` / `.panel-elevated`.
- `framer-motion` no longer imported anywhere in `Home.tsx`.

## Build queue status
- [DONE] #2 Cove design tokens (`e8b805d`)
- [DONE] #3 Hunt as data table (`e8a3572`)
- [DONE] #4 Routing restructure + LandingPage shell (`abf66d9`)
- [DONE] #5 Luke landing-copy polish (`eddc21f`)
- [DONE] (this run) Dashboard *content* rebuild (`8c43089`)
- [TODO] #1 Supabase `spread_results` warehouse table — gated on Travis applying SQL via dashboard
- [TODO] #6 Ticker Analysis full delta × DTE matrix page
- [TODO] Watchlist page Cove pass
- [TODO] DEPLOYMENT.md / HTTPS_DEPLOYMENT_GUIDE.md Supabase rewrites
- [TODO] Stripe subscription flow end-to-end test
- [TODO] Production deploy on StrikeRewind.com

## Recommendation
No new approval gate from this run. Owner-side gates open and unchanged:
- `ROTATED: STRIKESIGHT KEYS READY` — rotate the leaked Xata API key in the Xata dashboard so it's invalidated.
- `APPROVED: SUBSCRIBE POLYGON STARTER, $29/MO` (or `APPROVED: SUBSCRIBE MARKETDATA.APP TRADER, $60/MO`) — paid options chain when entering final pre-launch testing.
- Apply Supabase `spread_results` warehouse table SQL via the dashboard (or grant explicit consent for AutoBox to author the migration file).
- PAF: AdSense impressions / eCPM, Google Ads verification clearance + four-item post-verification queue.

Next autonomous-runnable steps in priority order:
1. Ticker Analysis full delta × DTE matrix page (#6 — the page the dashboard's `Confirm on {ticker}` CTA already routes to).
2. Watchlist page Cove pass (currently still on legacy emerald + framer-motion).
3. DEPLOYMENT.md / HTTPS_DEPLOYMENT_GUIDE.md Supabase rewrites — small, no approval, before production deploy.

Current cash balance: **$162.45**. No spend.
