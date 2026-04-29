# StrikeSight `/watchlist` — Cove design coherence pass

**Branch:** `autobox/strikesight-scanner-mvp`
**Commit:** `d92db10`
**File changed:** `frontend/src/pages/Watchlist.tsx` only — `+149 / -92`

## Why this run
The HANDOFF build queue's user-visible passes (Cove tokens, Hunt as data table, routing+landing, Luke landing copy, Dashboard rebuild, Analysis Cove pass) are all shipped. The remaining authenticated screen on legacy emerald + framer-motion + `bg-dark-card` + `text-gray-*` was `/watchlist` — the retention surface the dashboard's watchlist quick-view rows link into via `Confirm on {ticker}`. With dashboard + analysis both on Cove tokens, Watchlist was the one place a Pro-tier user would land that didn't read as part of the same product. This pass closes that.

The wakeup brief explicitly warned against defaulting to internal-only docs (rules out the deploy-doc Supabase rewrites for now), and step #6 (full delta × DTE matrix) needs a backend payload change too risky to bundle one-shot. Watchlist was the right autonomous-runnable next move.

## What shipped
End-to-end rewrite of `frontend/src/pages/Watchlist.tsx`. All hooks, data fetches (`getWatchlist`, `removeFromWatchlist`), tier-gated `canSaveWatchlist` flow, refresh logic preserved exactly.

**Stripped:**
- `import { motion } from 'framer-motion'`
- Every `motion.div` row wrapper with `initial={{ opacity: 0, x: -20 }}` per-row stagger animation
- Loading spinner using `border-emerald` → now `border-accent border-t-transparent`

**Tokenized to Cove throughout:**
- `bg-dark-card` → `panel` + `bg-bg-elevated` for hover
- `border-gray-800` → `border-border-subtle` (the *correct* utility name — see bug note below)
- `text-emerald` → `text-accent`
- `text-green-400` / `text-red-400` → `text-pos` / `text-neg`
- `text-yellow-400` → `text-warn`
- `text-gray-400` / `text-gray-500` / `text-gray-600` → `text-fg-secondary` / `text-fg-muted`
- `bg-emerald + text-white + Upgrade Now` → `bg-accent text-bg-base + See plans` (smaller, less aggressive on a paywall surface)
- `text-2xl font-bold` ticker headers → `font-mono text-base font-semibold` (institutional)
- All numeric cells (`currentPrice`, `priceChangePercent`, `successRate`, `optimalWeeks`, `ivRank`, count) carry `.num` for tabular-numerals + JetBrains Mono
- `rounded-lg` → `rounded-md` (matches Cove default radius)

**Layout shifts:**
- Pre-existing: each watchlist item was a stacked card with `<TrendingUp>`/`<TrendingDown>` icons, a `grid grid-cols-3` stat block, and a delete button.
- Now: a `panel divide-y divide-border-subtle` list. Each row renders `[★] TICKER  $price  ±%change` as a horizontal headline with stats inline on desktop (`hidden sm:flex`), then an `ArrowRight` chevron to make "open analysis" affordance explicit + the delete trash icon. Mobile keeps the same headline and drops the stats below in a single horizontal strip.
- `<TrendingUp>` / `<TrendingDown>` icons removed — the signed `+/-%` with `text-pos`/`text-neg` color encoding carries the same signal more compactly and matches Hunt's table.

**Copy aligned with the rest of the app:**
- Page subtitle: `Track the names you trade. Get a daily heads-up when a new spread clears your filters.` — same digest framing Luke shipped on the landing page and the dashboard, no realtime alert claim.
- Free-tier upsell: `Watchlist is part of Pro. Save up to 25 tickers, get a daily digest when a new bull put or bear call setup clears your filters, and jump straight into Ticker Analysis from any saved name.` — names the actual feature mechanic (limit + digest cadence + cross-page jump) instead of "Save your favorite stocks and track them in one place."
- Empty state nudges to `/hunt` with `Run a hunt` CTA + tells the user the dashboard surfaces the current top spread per saved ticker (closes the loop with the dashboard's watchlist quick-view).
- Stat labels: `Success Rate` → `Win rate` (matches Hunt and Analysis), `Optimal` → `Optimal` (kept), `IV Rank` → `IV rank` (lowercased for Luke voice).

**Accessibility:**
- Refresh, open-analysis, delete, ticker-row buttons all have `aria-label`.
- Open-analysis affordance is now an explicit `ArrowRight` button (was previously implicit on a `cursor-pointer` div).

## A real bug caught and fixed
While verifying the build, I noticed `border-subtle`, `border-strong`, `divide-subtle` references in my first cut compiled to no CSS. Reason: in this Tailwind config the colors are *named* `border-subtle` and `border-strong`. Tailwind utilities follow a `{prefix}-{color-name}` shape, so the working utilities are `border-border-subtle`, `border-border-strong`, `divide-border-subtle`. The unprefixed form silently no-ops because Tailwind doesn't have a color named `subtle` to match.

Compiled-CSS audit on the prior bundle confirmed:
- `.border-border-subtle`, `.border-border-strong`, `.divide-border-subtle` exist.
- `.border-subtle`, `.border-strong`, `.divide-subtle` do not.

Fixed in this run for Watchlist. **`Analysis.tsx` (shipped earlier today, commit `59ea5cb`) has the same issue** — needs a follow-up sweep. The `.panel` component class is unaffected because it sets `border: 1px solid var(--border-subtle)` directly via CSS custom properties at the `@layer components` level, so most panel-bordered surfaces still render the right border. The leak is in places that use raw `border border-subtle` utility classes on non-`.panel` elements.

## Verification
- `cd frontend && npm run build` passes — bundle `dist/assets/index-D73VHxFA.js 452.19 kB` / CSS `25.89 kB` (`+1.45 kB` js / `+0.16 kB` css from last run; bundle moved up because Watchlist now uses `lucide` `ArrowRight` and a few new utility classes).
- `cd backend && npm run build` (tsc) passes (no backend changes).
- `SUPABASE_URL=http://localhost:0 SUPABASE_SECRET_KEY=dev HUNT_USE_FIXTURES=1 npx tsx --test src/services/huntFixtureMode.test.ts` passes `3/3`.
- `grep -cE "framer-motion|motion\." frontend/src/pages/Watchlist.tsx` returns `0`.
- `grep -cE "emerald|dark-card|dark-bg|gray-800|gray-700|gray-400|gray-500|gray-600|text-green|text-red-400|text-yellow|text-white" frontend/src/pages/Watchlist.tsx` returns `0`.
- Compiled CSS contains `.border-border-subtle`, `.divide-border-subtle`, `.hover\:border-border-strong` — utilities now real CSS, not silent no-ops.

## What was deliberately not bundled
- Analysis.tsx `border-subtle` → `border-border-subtle` cleanup — separate run, separate file.
- Account.tsx, Scanner.tsx, SuccessRateIndicator.tsx, Layout.tsx framer-motion — those still import it. Earlier handoffs assumed Watchlist + Layout were the last two; that was wrong. Dropping framer-motion from `package.json` is not unlocked by this run.
- Luke pass on the Watchlist authenticated copy — short, internally consistent, can be folded into the deploy-prep Luke sweep when StrikeSight goes live.
- Public deploy / IndexNow — StrikeSight is on `autobox/strikesight-scanner-mvp` and not yet on a public URL. Deploy gate is its own run.

## Next autonomous step
Either (a) Analysis.tsx `border-subtle` → `border-border-subtle` correctness pass (small, surgical, fixes the same Tailwind-utility miss across the page that ships today's `Confirm on {ticker}` activation flow); or (b) Account.tsx / Scanner.tsx Cove pass (so framer-motion can be evaluated for removal — would also pull in SuccessRateIndicator.tsx and Layout.tsx); or (c) step #6 from the build queue (Ticker Analysis full delta × DTE matrix — requires backend `allStrategies` grid payload added to `AnalysisResult`, then a frontend matrix component); or (d) `DEPLOYMENT.md` / `HTTPS_DEPLOYMENT_GUIDE.md` Supabase rewrites before any production deploy. (a) is the smallest correctness win and the most direct customer-facing impact since Analysis is on the activation path. (c) is the highest product value but biggest scope.

## Open owner gates (unchanged)
- `ROTATED: STRIKESIGHT KEYS READY` — rotate the leaked Xata API key `xau_ncIRLvD0ac8cIczjxF0vZbHzW6nCArva4` in the Xata dashboard so it's invalidated (independent of removing the SDK).
- `APPROVED: SUBSCRIBE POLYGON STARTER, $29/MO` (or `APPROVED: SUBSCRIBE MARKETDATA.APP TRADER, $60/MO`) — real options chain data for final pre-launch testing.
- Supabase `spread_results` warehouse migration still needs Travis to apply SQL via the dashboard.
- PAF: AdSense impressions / eCPM, Smart Bidding strategy + spend report against the `$50` stop-loss, Google Ads verification clearance + the four-item post-verification queue.

## Spend
None. Current cash balance: `$162.45`.
