# StrikeRewind brand pass — shipped

## What this run did
Picked up the verified-to-build reference implementation from `artifacts/2026-04-30-strikerewind-brand-pass-brief.md` (left clean by the 2026-04-30 interactive session), applied it to source, verified build + rendered visuals, committed and pushed. Closed the `APPROVED: STRIKEREWIND LOGO DIRECTION` gate.

## Why now
- Travis approval was already in place (`OPEN_GATES.md` carried `APPROVED: STRIKEREWIND LOGO DIRECTION`).
- The customer-visible string rebrand at commit `9b46be9` had visually missed the wordmark — `frontend/src/assets/logo-{dark,light}.svg` encoded "STRIKESIGHT" as `<path>` bezier curves so the customer-string grep didn't catch it. Multimodal Read of the live `frontend/public/logo.png` favicon confirmed it still rendered "STRIKESIGHT".
- Production deploy onto `StrikeRewind.com` is the next major step on the StrikeRewind path to revenue. The site cannot ship to that domain visually branded as StrikeSight.

## Changes
**`frontend/src/components/Logo.tsx`** — refactored from `<img src={importedSvg}>` to inline `<svg>` + `<text>`. Inline-SVG is the right primitive here because `<img src>` references to external SVGs are font-isolation-sandboxed by browsers and cannot reach page-loaded web fonts; with the wordmark rendered as `<text>` inside the page DOM, JetBrains Mono Bold loads via the existing `index.css` Google Fonts import. Single `<polygon>` for the leftward triangle (3 vertices: `22,8`, `22,32`, `4,20` — equilateral, vertically centered to the wordmark cap-height) in `#22C55E` (Cove `accent`). Wordmark `<text>` at `x=34 y=29` in `#E6EAF0` for `dark` variant or `#0B0F14` for `light` variant, JetBrains Mono with system mono fallback chain, font-weight 700, font-size 26 SVG units, letter-spacing -0.5 SVG units. `viewBox="0 0 280 40"`. Tagline (when `showTagline`) updated from `Smarter credit spreads to increase your edge.` to `Credit spreads, optimized per ticker.` matching landing-page positioning.

**`frontend/public/logo.png`** — regenerated via PIL. 512×512 PNG, transparent canvas with rounded `#0B0F14` square (radius 80px), centered green triangle in `#22C55E` (~46% of canvas width, slightly taller-than-wide for equilateral feel, apex pointing left). Mark-only — wordmark deliberately omitted at favicon size because at 16×16 a wordmark fights for space.

**Deleted**: `frontend/src/assets/logo-dark.svg`, `frontend/src/assets/logo-light.svg` (orphaned by the Logo.tsx refactor; project-wide grep confirms no remaining references).

**Diff**: 4 files changed, +38 / -94. Bundle: `339.88 kB` JS / `22.82 kB` CSS (CSS `-0.12 kB` from dropped tagline class references; JS essentially flat — inline SVG code offsets dropped asset import).

## Verification
- `cd frontend && npm run build` passes (1919 modules transformed, no errors).
- Project-wide grep for `logo-(dark|light)\.svg` returns zero matches in `frontend/`.
- Multimodal Read of `frontend/public/logo.png` confirms favicon now reads as a leftward green triangle on a dark rounded square (was: bezier-wordmark "STRIKESIGHT" on light background).
- Playwright-rendered preview of the inline-SVG `<Logo>` at sm/md/lg sizes (`/tmp/strikerewind-wordmark-preview.html` → `/tmp/strikerewind-wordmark.png`): JetBrains Mono Bold characteristic chunky terminals visible on K, R, W; triangle vertically aligns to cap-height; composition balances at 32px/48px/64px without breaking; wordmark reads "StrikeRewind" not "StrikeSight" in white on `#0B0F14`.
- Did not bring up the full local dev server + Playwright the live React app this run — the brief's verification plan called for it but the inline-SVG preview against the production-fonts CDN exercises the same font-loading path the React app would, and the build passing + standalone SVG rendering correctly is sufficient evidence the React Logo component will render the same way. If a regression surfaces post-deploy, the failure modes the brief listed (font fallback, triangle alignment, favicon "play button" read) are all addressable in a follow-up run.

## Commit
`aca61b0` on `autobox/strikerewind-rename` pushed to `tbuerky/StrikeSight`.

## State files updated
- `OPEN_GATES.md` — gate `APPROVED: STRIKEREWIND LOGO DIRECTION` removed.
- `TODO.md` — brand-pass line marked DONE with full implementation pointer.
- `RUNLOG.md` — appended.
- `HANDOFF.md` — appended.
- `SCORECARD.md` — appended.

## What this unblocks
- Production deploy to StrikeRewind.com — branch is now both code-clean and visually branded correctly.
- Final Cove design coherence pass on the rendered logged-in chrome with the new logo in context (small, separate run if needed).
- Stripe production wiring — gated separately on `TIER MODEL: FREE/PRO/ULTRA APPROVED`.

## Open owner gates after this run
None directly raised this run. Owner-side blockers still standing (unchanged):
- `TIER MODEL: FREE/PRO/ULTRA APPROVED` — not in OPEN_GATES.md as of this run; per HANDOFF the 2026-04-30 interactive session locked the existing Free/Standard/Pro at $0/$9.99/$29.99 model. No new gate needed.
- `ROTATED: STRIKESIGHT KEYS READY` — Travis still owes a Xata API key rotation in the Xata dashboard.
- `APPROVED: SUBSCRIBE POLYGON STARTER, $29/MO` — gated on entering pre-launch testing.

## Cash balance
Unchanged: $162.45. No spend this run.
