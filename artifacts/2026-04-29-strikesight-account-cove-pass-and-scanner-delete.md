# StrikeSight `/account` Cove pass + delete dead `Scanner.tsx`

**Date:** 2026-04-29
**Branch:** `autobox/strikesight-scanner-mvp`
**Commit:** `a26b588`
**Repo:** https://github.com/tbuerky/StrikeSight
**Cash balance:** $162.45 (no spend)

## Why this run

Last run shipped the Analysis.tsx Tailwind utility correctness sweep (`117e11f`). The remaining authenticated screens still on legacy emerald + framer-motion were `Account.tsx` (the billing/upgrade conversion surface) and `Scanner.tsx` (dead code, not imported anywhere).

`Account.tsx` is the conversion-to-paid surface — when a user clicks `See plans` or `Upgrade` from any other page, they land here and are asked to hand over money. A polished landing → polished dashboard → 2024-era Tinder-grade billing screen would have undone the credibility built upstream. That makes Account the last user-visible authenticated screen the deploy needs to read as one product.

`Scanner.tsx` was 226 lines of dead code — a leftover from the pre-rebuild swipeable-card UI Hunt was rebuilt out of. No imports, not in `App.tsx`, pure drift risk if future Cove passes touched it.

Wakeup brief explicitly favored "pruning, grouping, hierarchy, or stronger product copy" over piling more sections on the site. Scanner deletion is pruning; Account is hierarchy + stronger product copy on the conversion path.

## What changed

### `frontend/src/pages/Account.tsx` — end-to-end rewrite

**Stripped:**
- `import { motion } from 'framer-motion'` and every `motion.div` (4 fade wrappers + the success message slide-in) and `motion.button` (Sign Out tap-scale)

**Tokenized:**
- `bg-dark-card` → `panel`
- `border-gray-800` → `border-border-subtle`
- `text-emerald` → `text-accent`
- `text-gray-{400,500,600}` → `text-fg-{secondary,muted}`
- `text-yellow-400` → `text-warn`
- `text-emerald` (status active) → `text-pos`
- `bg-emerald + text-white` (CTAs) → `bg-accent + text-bg-base`
- `bg-emerald/20 text-emerald` (current-plan badge) → `bg-accent-soft text-accent border-accent`
- `bg-yellow-900/20 border-yellow-500/30` (dev panel) → `panel border-l-2 border-l-warn`
- `bg-blue-600` / `bg-purple-600` / `bg-gray-600` (dev reset buttons) → consistent `bg-bg-elevated border border-border-subtle hover:border-border-strong`
- `text-2xl font-bold` (price) → `text-2xl font-semibold` + `.num` (tabular numerics + JetBrains Mono)
- `rounded-lg` → `rounded-md` throughout
- `text-3xl font-bold` (page title) → `text-3xl font-semibold`
- numeric cells tagged with `.num` for tabular figures (analyses count, price, next billing date)

**Aligned tier feature copy with landing page promise verbatim:**

The landing page (post-Luke polish, commit `eddc21f`) promises FREE-tier specs as `top 5 Hunt results/day, 2 ticker lookups/day, 1 year of history. No card required.` Account.tsx FREE row used to read `3 analyses per day, 1 year historical data, Basic scanner (10 tickers), No IV data` — wildly different feature, scope, and number. A user clicking `See plans` from the landing page was being shown a different product than the one promised. Replaced FREE features with the landing-page wording verbatim. STANDARD/PRO feature lists left alone — those tiers' specs aren't documented in HANDOFF and changing them would be a product-content decision needing owner input.

**Vite correctness:**
- `process.env.NODE_ENV === 'development'` → `import.meta.env.DEV`. The old form depended on Vite's prod optimizer to replace `process.env.NODE_ENV` with `'production'` and dead-code-eliminate the dev panel. Replacing it with `import.meta.env.DEV` (Vite's documented API) makes the dev-panel strip unambiguous in production builds.

**Copy polish in Luke voice:**
- `Today's Usage` → `Today's usage`
- `Subscription Plans` → `Plans`
- `Current Subscription` → `Current subscription`
- `Manage Billing` → `Manage billing`
- `⚠️ Development Tools` → `Development tools` (no warning emoji)
- `Reset your tier to test different subscription levels and upgrade flows.` → `Reset your tier locally to test different subscription levels.`
- `Plan:` / `Status:` / `Next billing:` (trailing colons) → `Plan` / `Status` / `Next billing` (clean labels)
- `Upgrade Successful!` → `Upgrade successful`
- `Your payment has been processed. Your new features will be available shortly.` → `Payment processed. Your new features will be available shortly.`
- `Got it!` → `Got it`
- `Sign Out` → `Sign out`
- `Made with ❤️ for traders` (twee filler) → removed
- Subtitle added under page title: `Plan, usage, and billing.` (one-line statement of what the page is)
- `aria-label` added to: Manage billing button, Upgrade button (per-tier), Sign out button

**Bug fix:**
- Usage % bar width was `(usage.analysisCount / limits.maxAnalysesPerDay) * 100` with no clamp — could overflow the bar visually if backend ever reported `analysisCount > maxAnalysesPerDay`. Now clamped to `Math.min(100, ...)`.

**Preserved exactly:**
- All hooks (`useUser`, `useState`, `useEffect`, `useSearchParams`)
- All Stripe handlers (`createCheckoutSession`, `createPortalSession`, `getStripePrices`, `getSubscriptionInfo`, `resetUserTier`)
- Tier names (`FREE`, `STANDARD`, `PRO`) and prices ($0, $9.99, $29.99) — these are tied to real Stripe price IDs in env (`STRIPE_STANDARD_PRICE_ID`, `STRIPE_PRO_PRICE_ID`) and changing them would require coordinated owner action in Stripe Dashboard
- Stripe success/cancel URL param handling
- Dev tier reset buttons (gated on `import.meta.env.DEV`)

### `frontend/src/pages/Scanner.tsx` — deleted

Dead code. 226 lines. Not imported anywhere in `frontend/src/`. Not in `App.tsx` route map. Legacy duplicate of the pre-rebuild Hunt swipeable-card UI. Deletion removes drift risk if future Cove passes ever touched it and trims source-tree noise.

## Verification

- `cd frontend && npm run build` passes (bundle `dist/assets/index-JGsRcm1X.js 452.35 kB` / CSS `dist/assets/index-B9mTYHsT.css 24.11 kB` — CSS down `-1.78 kB` from removing legacy color utilities; js essentially flat because Layout + SuccessRateIndicator still import `framer-motion`)
- `cd backend && npm run build` passes (no backend changes)
- `SUPABASE_URL=http://localhost:0 SUPABASE_SECRET_KEY=dev HUNT_USE_FIXTURES=1 npx tsx --test src/services/huntFixtureMode.test.ts` passes 3/3
- `grep -cE "framer-motion|motion\." frontend/src/pages/Account.tsx` returns `0`
- `grep -cE "emerald|dark-card|dark-bg|gray-800|gray-700|gray-600|gray-500|gray-400|gray-300|text-white|yellow-900|yellow-300|yellow-500|red-500|blue-500|blue-600|purple-600|❤" frontend/src/pages/Account.tsx` returns `0`
- `grep -E "(^|[ \"])(border|divide|hover:border)-(subtle|strong)([ \"]|$)" frontend/src/pages/Account.tsx` returns no matches (no Tailwind utility-name leaks of the kind caught on Watchlist + Analysis last week)
- Compiled CSS contains `.border-border-subtle` (utility now real, not silent no-op)
- `git diff --stat HEAD~1` confirms only `frontend/src/pages/Account.tsx` modified and `frontend/src/pages/Scanner.tsx` deleted: `+100 / -349`, net `-249` lines

## Public-copy hygiene per `RULES.md` rule 14/15

Account is post-signup authenticated UI rather than customer-facing in the SEO sense, but every label was rewritten to match Luke's voice on the public landing page (lowercase, product-shaped, no internal scaffolding, no AI-smell, no machine fingerprints). The "Made with ❤️ for traders" line was the last twee-filler artifact in the customer-conversion path; removed. The FREE-tier feature list now matches the landing page promise verbatim, so a user moving landing → dashboard → Account doesn't see a different product than the one they were sold.

## Customer-facing inconsistency flagged for Travis

The HANDOFF spec from 2026-04-28 locked in a Free / Pro (~$29-39/mo) / Ultra (~$99/mo) three-tier model. Account.tsx ships a Free / Standard ($9.99) / Pro ($29.99) three-tier model. These are different tier names and different prices. The Account.tsx model is what the live Stripe price IDs point at; the HANDOFF model is the locked product spec. Production deploy with Stripe live cannot ship until Travis decides which tier model is canonical and reconciles the Stripe Dashboard accordingly. Surfaced as a follow-up gate, not a code change in this run — changing it without owner input would either (a) sell the wrong product on the landing page or (b) point landing-page CTAs at non-existent Stripe price IDs.

## What did *not* ship in this run

- Pricing / tier-name reconciliation between landing page (Free/Pro/Ultra) and Account.tsx (FREE/STANDARD/PRO). Owner decision required.
- Layout.tsx and SuccessRateIndicator.tsx still import `framer-motion`. Two more component-internal sites (nav indicator + animated bar) before the package can be dropped from `package.json`.
- Production deploy. Still gated on Polygon subscription approval, Stripe production price IDs aligned with the locked tier model, Supabase prod env, and final QA.
- `DEPLOYMENT.md` / `HTTPS_DEPLOYMENT_GUIDE.md` Supabase rewrites. Internal-doc work; wakeup brief explicitly warned against defaulting to internal-only docs over sharper customer-facing moves.

## Next autonomous-runnable step

Highest leverage: **flag the tier-model mismatch to Travis on Discord as a decision packet**. Without that decision, Stripe production wiring stays blocked, which means the entire post-Cove deploy path is blocked. The visual coherence work is now done across every customer-conversion page (landing → dashboard → hunt → analysis → watchlist → account). The next blocker is product-content / pricing reconciliation, which is owner-side.

Adjacent options if the tier-model packet is sent and the run still has time:
- Layout.tsx + SuccessRateIndicator.tsx framer-motion strip (small, unlocks dropping the package)
- Step #6 from the build queue: full delta × DTE matrix on `/analysis/:ticker` (requires a backend `allStrategies` payload field — `newAnalysisEngine.ts:462` truncates to `topStrategies.slice(0,5)`)

## Owner gates open and unchanged

- `ROTATED: STRIKESIGHT KEYS READY` — rotate the leaked Xata API key in the Xata dashboard so it's invalidated (independent of removing the SDK)
- `APPROVED: SUBSCRIBE POLYGON STARTER, $29/MO` (or `APPROVED: SUBSCRIBE MARKETDATA.APP TRADER, $60/MO`) — real options chain data when entering final pre-launch testing
- Supabase `spread_results` warehouse migration — Travis to apply SQL via dashboard
- **NEW (this run):** Tier-model decision — Free/Pro/Ultra (HANDOFF spec) vs Free/Standard/Pro (current Stripe price IDs). Reply with the canonical model so landing-page CTAs and Stripe Dashboard reconcile.
- PAF-side: AdSense impressions / eCPM, Smart Bidding strategy + spend report against the `$50` stop-loss, Google Ads verification clearance + the four-item post-verification queue.
