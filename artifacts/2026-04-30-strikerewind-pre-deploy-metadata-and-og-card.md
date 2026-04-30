# StrikeRewind — pre-deploy landing metadata + Open Graph card

**Date:** 2026-04-30
**Branch:** `autobox/strikerewind-rename`
**Commit:** `59c297a`
**Cash balance:** $162.45 (no spend)

## Why this run

Deploy gate `APPROVED: DEPLOY ON VERCEL+RENDER STARTER, $7/MO` is open and waiting on Travis. Until that approval lands, the production deploy itself can't run. The highest-leverage no-approval move is pre-deploy hygiene that's correct under any architecture choice and that the deploy run itself would otherwise have to bundle.

The current `frontend/index.html` ships only a `<title>` and a viewport tag. On a public credit-spread tool, that means:

- Search snippets render with no description
- Discord, Slack, X, iMessage previews render with no image and no description
- The first time a paying-prospect sees a StrikeRewind URL in a thread, it shows up as a bare text link

This is a real first-impression hit. Fixing it before deploy is cheaper than fixing it after the first share goes flat.

## What shipped

`frontend/index.html` (`+18 / -1`):
- `<meta name="description">` (155 chars) matching Luke's hero voice — `Find ticker-specific credit spreads that have historically beaten the 30-delta rule. Nightly scan of the S&P 500, ranked by win rate and expected value.`
- `<link rel="canonical" href="https://strikerewind.com/">` — sets the canonical for the public landing
- Open Graph block — `og:type`, `og:site_name`, `og:url`, `og:title`, `og:description`, `og:image` (with explicit `1200x630` dimensions), `og:image:alt`
- Twitter Card block — `twitter:card=summary_large_image`, `twitter:title`, `twitter:description`, `twitter:image`, `twitter:image:alt`
- `theme-color` corrected from `#000000` to Cove `#0B0F14` for mobile chrome consistency

`frontend/public/og-card.png` (new, 22.8 kB, 1200x630):
- Background `#0B0F14` (Cove `bg-base`)
- Leftward accent triangle `#22C55E` at left, vertically centered
- Wordmark `StrikeRewind` in `#E6EAF0`, JetBrains Mono Bold 110pt — fetched the actual TTF from the JetBrains GitHub repo into `/tmp` and rendered with PIL so the OG card matches the in-app wordmark exactly
- Tagline `Credit spreads, optimized per ticker.` in `#A4ADBA`, JetBrains Mono Regular 32pt, matching the Logo component's `showTagline` copy

Generated with `python3 /tmp/generate_og.py` (PIL `Image.new` + `ImageDraw.polygon` + `ImageDraw.text` with the downloaded JetBrains Mono Bold/Regular TTFs). Multimodal Read on the produced PNG verifies: leftward green triangle reads as the brand mark; "StrikeRewind" wordmark renders with JetBrains Mono Bold's distinctive K and R terminals; tagline sits below the wordmark in muted secondary; composition balances at 1200x630.

## What deliberately did NOT change

- `vercel.json` — broken serverless config (declares Express backend as Node-18 serverless with `app.listen` + `node-cron` inside) is left alone. Fixing it correctly depends on architecture choice (Option A frontend-only static vs Option B/D no-Vercel-at-all). The deploy run handles this when approval comes in.
- `frontend/.env.production` — file is `.gitignore`'d (line 24), so local edits don't propagate to deploy. Vercel env vars (`VITE_APP_NAME`, `VITE_API_URL`, `VITE_STRIPE_PUBLISHABLE_KEY`) are set at deploy time, not from a tracked file. Local edit made for dev-build parity only.
- `theme-color` already updated above; no other index.html scaffolding touched.
- No backend changes, no source-tree refactors, no bundle-size impact (HTML +1.43 kB, OG asset is a static public file not in the JS bundle).

## Verification

- `cd frontend && npm run build` passes (1920 modules transformed; `dist/index.html 2.29 kB / gzip 0.75 kB`; `dist/assets/index-eeRexftA.css 23.33 kB`; `dist/assets/index-D6t4qFBG.js 345.52 kB` — JS + CSS unchanged from prior build, only HTML and the new public asset shifted).
- `dist/og-card.png` present at `22 815` bytes; copied through Vite's public-asset pipeline correctly.
- `grep -c "og-card.png\|StrikeRewind\|og:image\|twitter:card\|description" dist/index.html` returns `14` — every metadata tag survives the build pipeline.
- `cd backend && npm run build` (tsc) passes; backend untouched.
- `SUPABASE_URL=http://localhost:0 SUPABASE_SECRET_KEY=dev HUNT_USE_FIXTURES=1 npx tsx --test src/services/huntFixtureMode.test.ts` passes 3/3.
- Multimodal Read of `frontend/public/og-card.png` confirms wordmark reads "StrikeRewind" (not "StrikeSight"), triangle is leftward green, no text rendering glitches.

Public-copy hygiene per `RULES.md` rule 14/15: every customer-visible string in the new metadata uses Luke's voice — no internal labels, no SEO scaffolding, no AI-smell, no machine fingerprints, no process language.

## What this unblocks

When Travis replies `APPROVED: DEPLOY ON VERCEL+RENDER STARTER, $7/MO`, the deploy run no longer has to bundle metadata polish. It's: fix `vercel.json`, set Vercel env vars (including `VITE_APP_NAME=StrikeRewind` and `VITE_API_URL=https://api.strikerewind.com`), `vercel deploy --prod`, configure DNS, smoke-test. The first social share of the live URL renders correctly out of the box.

## Cost / approval

No spend. No approval gate raised. Cash balance stays at `$162.45`.
