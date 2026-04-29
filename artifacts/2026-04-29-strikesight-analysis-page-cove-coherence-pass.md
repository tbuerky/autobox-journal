# StrikeSight — Analysis page Cove design coherence pass

**Date:** 2026-04-29
**Branch:** `autobox/strikesight-scanner-mvp`
**Commit:** `59ea5cb` on `https://github.com/tbuerky/StrikeSight`
**Files changed:** `frontend/src/pages/Analysis.tsx` (only) — `+210 / -283`, net `-73`
**Cash impact:** none. Balance remains `$162.45`.

## Why this run

Earlier today the dashboard rebuild (`8c43089`) closed the landing → activation mismatch. The dashboard's primary CTA is `Confirm on {ticker}` → `/analysis/{ticker}`. That destination — `Analysis.tsx` — was the only authenticated page still on legacy emerald + framer-motion + `text-8xl` hero + gradient quality cards. Hunt and Dashboard are already on Cove tokens; LandingPage is post-Luke; Analysis was the visual outlier. A polished landing page that converts a stranger to a signup, a polished dashboard that gets them to "Confirm on AAPL", and then a 2024-era Tinder-grade activation page would have undone the credibility built upstream.

Distinct from build-queue step #6 (full delta × DTE matrix). That spec requires backend changes — the engine currently truncates to `topStrategies = spreadAnalyses.slice(0, 5)` (see `newAnalysisEngine.ts:462`); the full grid is 9 OTM levels × 8 DTE levels × 2 spread types = 144 combinations, which would need a non-truncated payload field. That's its own bigger run with backend + frontend changes. This run is a pure deploy-prep visual coherence pass on the existing top-5 framing.

## What changed

End-to-end rewrite of `frontend/src/pages/Analysis.tsx`. All hooks, data fetches, watchlist toggle, parameter change, and reanalyze logic preserved exactly. Visual layer + copy only.

**Stripped:**
- `import { motion } from 'framer-motion'`
- Every `motion.div initial={{ opacity: 0, y: 20 }} animate={{ opacity: 1, y: 0 }}` page-fade wrapper (4 sections)
- The reanalyzing overlay's `motion.div initial={{ opacity: 0, scale: 0.9 }}`
- `text-8xl font-black` hero scale → `text-6xl font-semibold`
- Gradient quality cards (`bg-gradient-to-br from-emerald/10 to-emerald/5`, `from-yellow/10`, `from-red/10`) → single `panel-elevated` with a small status badge (`Strong` / `Marginal` / `Weak` + annualized EV %)
- Color-wash warning blocks (`bg-yellow-500/10 border-yellow-500/20`, `bg-amber-500/10 border-amber-500/20`, `bg-blue-500/10 border-blue-500/20`) → single `border-l-2 border-l-warn pl-3` strip pattern
- Emerald loader spinner (`border-emerald`) → neutral `border-fg-muted` for initial load, `border-accent` for the reanalyze overlay (where motion is genuinely happening)

**Token swap (zero residual legacy refs — verified `grep -c emerald|dark-card|dark-bg|gray-800|gray-700|gray-400|gray-500|gray-300` returns `0`):**
- `bg-dark-card border border-gray-800 rounded-xl` → `panel` / `panel-elevated`
- `border-gray-800` / `border-gray-700` → `border-subtle` / `border-strong`
- `text-emerald` / `text-green-400` → `text-accent` / `text-pos`
- `text-red-400` → `text-neg`
- `text-gray-400` → `text-fg-secondary`
- `text-gray-500` / `text-gray-600` → `text-fg-muted`
- `text-white` → `text-fg-primary`
- `bg-emerald text-black` (CTA) → `bg-accent text-bg-base`
- `bg-emerald/20 text-emerald` (active watchlist toggle) → `bg-accent-soft text-accent border-accent`
- `bg-black/30` / `bg-black/50` → `bg-bg-surface`
- `rounded-xl` / `rounded-lg` → `rounded-md` (default)

**Numerics:**
- Header price + percent change → `.num` with `font-mono` ticker
- Hero EV% → `text-6xl font-semibold text-pos num`
- Three-column stat row (Win rate / Per $1 spread / Timeframe) → `text-2xl font-semibold num`
- Top strategies table → every numeric cell `.num`, EV column `text-pos` with signed prefix
- Today's mapped spread → every dollar/strike/expiration/days/credit/risk value `.num`

**Copy tightened (authenticated UI; not customer-facing in the SEO sense, but tightened to match Luke's voice on the public surfaces):**
- Header subhead added: `Confirm a Hunt result before you put it on. Top strategies below are ranked by historical EV at the chosen window.` — directly mirrors Luke's landing page line "Use it to confirm a Hunt result before you put it on" so the workflow vocabulary is consistent across landing → dashboard → analysis
- "Analysis Parameters" → "Window"
- "UNLIMITED" tier badge — removed (internal-label artifact)
- "Historical Data" → "Historical data"
- "Max Expiration" → "Max expiration"
- "Parameters changed - X year(s) of data, max Yw expiration" → "Pending recalculation — X yr, max Yw"
- "Reanalyze" → "Recalculate"
- "Reanalyzing..." → "Recalculating..."
- "Reanalyzing {ticker}" overlay → "Recalculating {ticker}" with monospace ticker
- "Historically Best Performing Strategy" → "Top historical strategy"
- "Average Historical Return" → "Average historical return" (uppercase tracking-wide, smaller)
- "Trade Structure" → "Spread"
- "PUT CREDIT SPREAD" → "{TYPE} credit spread" lowercase
- "Sell {ticker} {a}/{b} Put Spread" → "Sell {ticker} {a}/{b} put spread"
- "Entry Details" → "Entry"
- "Risk & Reward" → "Risk / reward"
- "Current Price:" → "Current"
- "Short Strike:" → "Short strike"
- "Long Strike:" → "Long strike"
- "Minimum Credit:" → "Min credit"
- "Max Risk:" → "Max risk"
- "Win Rate:" → "Win rate"
- "Expected Value:" → "EV"
- "Top 5 Strategies by Expected Value" → "Top strategies by EV"
- Strategy cell `PUT 5%` cell now styled with `font-medium` type, mid-dot separator, `.num` strike
- "Strategy Implementation" → "Today's mapped spread"
- "How this would look in today's market" → "Roughly how this top strategy maps onto the current price."
- "Based on historical data" badge → "Strong / Marginal / Weak (X% annualized)" badge in `text-accent` / `text-warn` / `text-neg`
- "Analysis Summary" → "What it means"
- "Note:" inside spread caveat → tightened, no inline `<strong>` wraps
- "Disclaimer:" → "Disclaimer." with `text-warn`

**Watchlist toggle:** rounded-md, panel-bordered, `bg-accent-soft text-accent border-accent` when active vs `bg-bg-panel text-fg-muted border-subtle hover:text-fg-primary hover:border-strong` when inactive. Proper `aria-label` ("Add to watchlist" / "Remove from watchlist") since it's a single icon button.

## Verification

- `cd frontend && npm run build`: passes (`dist/assets/index-mNqpQAgF.js 450.74 kB`, css `25.73 kB` — `-0.59 kB` css from removing the gradient/glow utilities; bundle js essentially flat because framer-motion is still imported by other pages: Layout's nav indicator, Hunt's setup form is already token-only, only Watchlist and Analysis still imported it — Analysis is now clean, so removing it from one more page doesn't cut the bundle).
- `cd backend && npm run build`: passes (no backend changes).
- `SUPABASE_URL=http://localhost:0 SUPABASE_SECRET_KEY=dev HUNT_USE_FIXTURES=1 npx tsx --test src/services/huntFixtureMode.test.ts`: passes 3/3.
- `grep -c "framer-motion\|motion\\." frontend/src/pages/Analysis.tsx`: `0` matches.
- `grep -c "emerald\|dark-card\|dark-bg\|gray-800\|gray-700\|gray-400\|gray-500\|gray-300" frontend/src/pages/Analysis.tsx`: `0` matches.
- `git diff --stat HEAD~1 frontend/src/pages/Analysis.tsx`: only one file changed, `+210 / -283`.

Public-copy hygiene per `RULES.md` rule 14/15: Analysis is post-signup authenticated UI, not customer-facing in the SEO sense, but every label was rewritten to match the voice Luke shipped on the public landing page (lowercase, product-shaped, no internal scaffolding, no AI-smell, no machine fingerprints). When StrikeSight goes to a public URL, a Luke pass on every authenticated screen remains its own deploy-prep run.

## What was deliberately NOT bundled

- **Backend changes for full delta × DTE matrix.** That's step #6's spec. The engine still returns top-5 strategies; this run preserved that data flow.
- **Watchlist page Cove pass.** `Watchlist.tsx` (174 lines) is still on legacy emerald + framer-motion. Smaller surface, retention-side. Pull-forward candidate for the next autonomous run.
- **Public deploy.** StrikeSight is on `autobox/strikesight-scanner-mvp` and not yet on a public URL. Production deploy is its own gated step (Polygon approval + Supabase prod creds + StrikeRewind.com DNS).
- **DEPLOYMENT.md / HTTPS_DEPLOYMENT_GUIDE.md Supabase rewrites.** Still references `XATA_API_KEY` / `XATA_DATABASE_URL`; small, no approval; should land before production deploy. Pull-forward candidate.
- **Light copy pass on the workflow tie-in subhead.** Could route through Luke for a polish before deploy, alongside Watchlist and Dashboard authenticated copy.

## Approval-gated items unchanged this run

- `ROTATED: STRIKESIGHT KEYS READY` — rotate the leaked Xata API key in the Xata dashboard so it's invalidated, independent of removing the SDK
- `APPROVED: SUBSCRIBE POLYGON STARTER, $29/MO` (or `APPROVED: SUBSCRIBE MARKETDATA.APP TRADER, $60/MO`) — paid options chain provider for final pre-launch testing
- Supabase `spread_results` warehouse migration — Travis to apply SQL via dashboard, or grant explicit consent for AutoBox to author the migration file
- PAF: AdSense impressions / eCPM, Google Ads verification clearance + four-item post-verification queue, Smart Bidding strategy + spend report against `$50` stop-loss

## Next autonomous-runnable step

The Watchlist page Cove pass is the next no-spend, customer-visible move (174 lines, retention-side, same legacy emerald + framer-motion shape) — it leaves Layout's nav-indicator `motion.div` as the sole remaining framer-motion site, after which the import can be evaluated for removal entirely. Then either step #6 (full delta × DTE matrix, requires backend grid payload), or the deployment doc rewrites before any production deploy.
