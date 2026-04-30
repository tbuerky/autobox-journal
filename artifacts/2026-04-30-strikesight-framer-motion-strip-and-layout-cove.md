# StrikeSight — framer-motion strip, Layout.tsx Cove pass, dead-code delete

## What shipped
- Removed `framer-motion` from `frontend/package.json` and lockfile (the last two consumers were either rewritten or deleted in this run).
- Rewrote `frontend/src/components/Layout.tsx` end-to-end. Replaced `motion.div` nav indicator (`layoutId="navIndicator"` spring transition) with a static 0.5px accent strip on the active item; tokenized every legacy class to Cove (`bg-dark-bg`/`bg-dark-card` → `bg-bg-base`/`bg-bg-panel`, `border-gray-800` → `border-border-subtle`, `text-emerald` → `text-accent`, `text-gray-400` → `text-fg-muted`, `bg-emerald/10` → `bg-accent`, PRO badge `bg-yellow-400/20 text-yellow-400` → `bg-warn/15 text-warn border-warn/30`); added `aria-label` + `aria-current="page"` on every nav link and `aria-label` on the logo home link.
- Deleted `frontend/src/components/SuccessRateIndicator.tsx` — 68 lines of dead code, no imports anywhere in the project.

## Why this run
HANDOFF/TODO both flagged Layout + SuccessRateIndicator as the last `framer-motion` consumers. Stripping them unlocks dropping the package itself, which:
1. Cuts the production JS bundle (the public landing page is the same React app — every visitor downloads this).
2. Closes the Cove migration: every authenticated screen + the public landing page now reads from one consistent token set, no legacy emerald/dark-card/gray references in any user-facing code.
3. Removes the only remaining bundle-size regression that would land on a public StrikeRewind.com deploy.

## Verification
- `frontend npm run build` passes. **Bundle: `dist/assets/index-NF6aLeFL.js 339.67 kB │ gzip: 103.17 kB` and `dist/assets/index-DpaCTw0S.css 22.94 kB │ gzip: 5.11 kB`. Down from `452.35 kB` JS / `24.11 kB` CSS in the prior run — `-112.68 kB` (~47 kB gzipped wire savings).**
- `backend npm run build` (tsc) passes.
- `huntFixtureMode.test.js` passes 3/3.
- `npm uninstall framer-motion` removed 4 packages cleanly (4 transitive deps).
- `grep -E 'framer-motion|from ["'\'']framer'` across `frontend/src` returns 0 matches.
- `grep -E 'bg-dark-|emerald|gray-[0-9]+|text-white|yellow-'` against `Layout.tsx` returns 0 matches.

## What did not change
- Bottom-nav route list (`/dashboard`, `/hunt`, `/watchlist`, `/account`) preserved exactly.
- Tier badge logic preserved exactly (PRO/STANDARD/free fallback).
- `Logo` component import preserved.
- No backend changes.
- No content/copy changes that affect the user-facing buyer story.

## Public-copy hygiene
Layout is shared chrome for authenticated routes, not customer-facing in the SEO sense, but applies the same Cove tokens that the public landing page uses. No internal labels or process language anywhere. PRO/STANDARD/free badge labels come from `useUser()` context, not changed here.

## Commit
`21a9963` on `autobox/strikesight-scanner-mvp` — pushed to GitHub.

## Owner-side gates open and unchanged
- `TIER MODEL: FREE/PRO/ULTRA APPROVED` — Travis Discord reply needed; deploy-blocking for Stripe production wiring.
- `ROTATED: STRIKESIGHT KEYS READY` — rotate leaked Xata API key in Xata dashboard.
- `APPROVED: SUBSCRIBE POLYGON STARTER, $29/MO` — gated on entering pre-launch testing.
- Supabase `spread_results` warehouse SQL — apply via Supabase dashboard.

## Next autonomous-runnable steps
1. Step #6 from build queue — full delta × DTE matrix on `/analysis/:ticker`. Requires backend `allStrategies` payload (engine truncates to `topStrategies.slice(0, 5)` at `newAnalysisEngine.ts:462`). Frontend renders a sortable heat-map cell grid keyed by delta band × DTE bucket.
2. On `TIER MODEL: FREE/PRO/ULTRA APPROVED` reply — repoint env vars (`STRIPE_STANDARD_PRICE_ID` → `STRIPE_PRO_PRICE_ID`, `STRIPE_PRO_PRICE_ID` → `STRIPE_ULTRA_PRICE_ID`), update `Account.tsx` tier cards to match HANDOFF spec, add 3-card pricing block to `LandingPage.tsx`.
3. Production deploy to StrikeRewind.com on Vercel (domain already purchased; build is clean; Stripe stays in test mode until tier-model approved).

## Cash balance
`$162.45`. No spend this run.
