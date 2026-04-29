# StrikeSight routing restructure + public landing shell

## Date
2026-04-29

## Why this run picked this task
Per the locked HANDOFF build queue from the 2026-04-28 strategy session:
- Step #1 (Supabase `spread_results` warehouse table SQL) is owner-gated — Travis applies SQL via dashboard.
- Step #2 (Cove design tokens) shipped commit `e8b805d`.
- Step #3 (Hunt as data table) shipped commit `e8a3572`.
- Step #4 — **restructure routing so `/` is unauthenticated landing, `/dashboard` is authenticated home, `/hunt` stays as scanner** — was the next autonomous-runnable step and is the prerequisite for step #5 (Luke landing-copy pass on the credit-spread-optimization story Travis cited as the conversion lever).

Travis 2026-04-28 direction: "If you can correctly tell the story (scans whole S&P, returns tickers and exact strikes and exps that have been consistently profitable over time) that is something people would pay a subscription for." Building the public landing shell now creates the surface that copy lives on — without it the Luke pass has nothing to write into.

## What changed

### `frontend/src/pages/LandingPage.tsx` (new file, 138 lines)
Public unauthenticated landing page. **No Layout wrapper** — has its own header (logo + Sign in + Start free) and uses the standard Footer. Composed entirely from the new design tokens and lucide icons; zero framer-motion.

Sections:
- **Hero** — H1 names the niche (`Credit spreads, optimized per ticker.`), subhead explains the differentiation against the generic 30-delta rule, primary CTA `Run the scanner` → `/hunt`, secondary `How it works` anchor.
- **Three modes** — Hunt / Ticker Analysis / Watchlist, each in a `.panel` card with a lucide icon (`Target`, `LineChart`, `BellRing`) and a one-line plain-English description.
- **Why ticker-specific** — two-column section: left column explains why the 30-delta-everywhere rule fails on individual tickers; right column shows a labeled "Example output" `.panel-elevated` table (AAPL/MSFT/UNH rows with Win% and EV%, all numerics in `.num` JetBrains Mono with `text-pos` accent). Footnote labels the table as a sample so the page doesn't make a live-data claim.
- **Closing CTA** — repeat of `Start free`, names the free tier limits (top 5 Hunt results / 2 ticker lookups / 1 year history, no card required).
- **Footer** — standard StrikeSight Footer (Terms / Privacy).

Public-copy pass per `RULES.md` rule 14/15: every customer-visible string is product-shaped, no internal labels, no SEO-scaffolding language ("some buyers search …", "this page exists to …"), no notes-to-self. Draft copy goes through Luke at step #5 before any public deploy — flagged in the commit message and the next-step block below.

### `frontend/src/App.tsx`
Routes restructured:
- `/` → `<LandingPage />` (no Layout — pure public surface)
- `<Layout />` wraps the authenticated routes:
  - `/dashboard` → `<Home />` (was the index route at `/`)
  - `/analysis/:ticker` → `<Analysis />`
  - `/hunt` → `<Hunt />`
  - `/watchlist` → `<Watchlist />`
  - `/account` → `<Account />`
- `/terms`, `/privacy` unchanged.

Removed the stale `console.log('App component loaded')` debug line.

### `frontend/src/components/Layout.tsx`
- Bottom-nav `Home` item path changed `/` → `/dashboard` so the icon lights up on the right route.
- Header logo `<Link>` changed `/` → `/dashboard` so a signed-in user clicking the logo lands on their dashboard, not the marketing page.

### `frontend/src/pages/Analysis.tsx`
- The `navigate('/')` redirect on initial-load failure now sends to `/dashboard` (an authenticated user hitting `/analysis/<bad-ticker>` should fall back to their dashboard, not the public landing page).

## What was deliberately *not* done

- **Dashboard rebuild.** The HANDOFF brief for `/dashboard` calls for "today's top signal + watchlist quick-view + Run Hunt CTA." The current `Home.tsx` is still the legacy ticker-analysis launcher. Rebuilding it in the same run would have bundled scope; routing-only restructure keeps the change tightly verifiable. The dashboard rebuild stays as the explicit next-step item.
- **Luke landing-copy pass.** Step #5 in the HANDOFF queue. Today's draft is structurally correct and product-shaped, but the polished customer-facing voice routes through the Luke subagent before any public deploy. No public deploy in this run.
- **Auth wall / sign-in flow.** `UserContext` currently defaults every visitor to PRO tier in dev. Both Sign in and Start free CTAs land on `/dashboard` — fine for a pre-auth dev environment; real auth wiring is a separate later task.
- **Pricing block on the landing page.** Stripe is not wired live; showing "Subscribe" CTAs would route nowhere. Pricing goes in once Stripe test mode end-to-end is in place (existing TODO).
- **Layout.tsx framer-motion `motion.div` for the nav indicator.** Cove flagged framer-motion *page fades* and the emerald-glow effect for removal. The Layout's `layoutId` indicator is a nav-state transition, not a page fade. Out of scope for the routing task.

## Verification
- `cd frontend && npm run build` passes — bundle `dist/assets/index-S8VQv2BW.js 454.49 kB` / CSS `27.40 kB` (was `446.16 kB` / `25.94 kB` last run; growth is the new LandingPage bundle and a few new utility classes).
- `cd backend && npm run build` (tsc) passes.
- `SUPABASE_URL=http://localhost:0 SUPABASE_SECRET_KEY=dev HUNT_USE_FIXTURES=1 npx tsx --test src/services/huntFixtureMode.test.ts` passes `3/3` suites — confirms backend invariants unaffected by frontend route changes.
- `grep "to=['\"]/['\"]\|navigate(['\"]/['\"]\)" frontend/src/` returns three remaining matches: LandingPage's own logo (correct — links back to itself), Privacy's `Back to Home` link, Terms' `Back to Home` link. Both legal-page back-links land on the public landing page, which is the right destination for a logged-out visitor.
- No public deploy this run — StrikeSight is on `autobox/strikesight-scanner-mvp` and not yet on a public URL. Public-copy pass + IndexNow happen on the deploy run, not before.

## Commit
`abf66d9` on branch `autobox/strikesight-scanner-mvp`, pushed to `https://github.com/tbuerky/StrikeSight`.

## Owner-side gates open (unchanged)
- `ROTATED: STRIKESIGHT KEYS READY` — rotate the leaked Xata API key in the Xata dashboard so it is invalidated.
- `APPROVED: SUBSCRIBE POLYGON STARTER, $29/MO` (or `APPROVED: SUBSCRIBE MARKETDATA.APP TRADER, $60/MO`) — paid options chain data, only when entering final pre-launch testing.
- Supabase `spread_results` warehouse table — Travis applies SQL via the dashboard, or grants explicit consent for AutoBox to author a migration file for him to apply.
- PAF: AdSense impressions / eCPM, Smart Bidding strategy + spend report against the `$50` stop-loss, Google Ads verification clearance + four-item post-verification queue.

## Next step
Step #5 in the HANDOFF queue: **route the LandingPage hero/sections through Luke for a polish pass** on the credit-spread-optimization story before any deploy. Then step #6 (Ticker Analysis page rebuild) or the Dashboard rebuild (`/dashboard` becomes "today's top signal + watchlist quick-view + Run Hunt CTA"). Production deploy stays gated on the Luke pass + the design coherence review across the now-three-page surface (Landing, Dashboard, Hunt).

## Cash balance
$162.45. No spend this run.
