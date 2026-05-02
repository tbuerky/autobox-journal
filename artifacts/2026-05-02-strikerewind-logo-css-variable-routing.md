# StrikeRewind Logo CSS-variable routing — 2026-05-02

## Why this run

One open gate (`CARD ADDED: RENDER WORKSPACE`) — owner-only, blocks the StrikeRewind deploy pipeline. Last 5 runs alternated between PAF meta hygiene audits and pre-deploy hygiene on StrikeRewind customer-facing surfaces (options-risk disclosure 2026-05-02 commit `711abe8`, Footer Cove-token alignment 2026-05-02 commit `508d453`). Prior handoff explicitly named "Logo.tsx review pass (last component with hardcoded color values, not tokens)" as the next-adjacent autonomous-runnable option. Continuing the pre-deploy quality-control pattern on the customer-facing conversion chain.

## Diagnosis

`frontend/src/components/Logo.tsx` rendered a SVG wordmark with three fill values written as raw hex literals:
- `#22C55E` — accent triangle
- `#E6EAF0` — wordmark text on dark variant
- `#0B0F14` — wordmark text on light variant

These hex values match the canonical Cove tokens defined in `frontend/src/index.css:9-21` (`--accent`, `--fg-primary`, `--bg-base`), but the Logo component was not routing through those tokens — it duplicated the hex values inline. Concrete failure mode: the last token rotation (emerald `#10b981` → `#22C55E`, 2026-04-29 commit `e8b805d`) updated `tailwind.config.js` and `index.css`, but a Logo rendered as raw hex would not have followed automatically. Any future Cove-token shift would silently drift Logo.tsx from the rest of the surface.

## Edit

```tsx
// before
const wordmarkFill = variant === 'light' ? '#0B0F14' : '#E6EAF0';
const accent = '#22C55E';
...
<polygon points="22,8 22,32 4,20" fill={accent} />
<text fill={wordmarkFill} ...>StrikeRewind</text>

// after
const wordmarkFill = variant === 'light' ? 'var(--bg-base)' : 'var(--fg-primary)';
const accentFill = 'var(--accent)';
...
<polygon points="22,8 22,32 4,20" style={{ fill: accentFill }} />
<text style={{ fill: wordmarkFill }} ...>StrikeRewind</text>
```

Two non-obvious notes:
1. The SVG `fill` *attribute* does not parse CSS `var()` — only the CSS `fill` *property* does. Switched both `fill` attributes to `style={{ fill: 'var(--name)' }}` so the variable resolves at render time.
2. `index.css:8-22` already declares all three tokens at `:root`, so the variables are guaranteed to be in scope wherever Logo renders (every public + authenticated surface).

## Verification

- `cd frontend && npm run build` passes (1921 modules, JS `353.70 → 353.74 kB / +0.04 kB` flat, CSS `22.83 kB` unchanged).
- `cd backend && npx tsx --test src/services/huntFixtureMode.test.ts src/services/spreadResultsService.test.ts` passes `12/12`.
- Compiled bundle `dist/assets/index-C6i4LMo2.js` contains `var(--accent)` ×1, `var(--fg-primary)` ×1, `var(--bg-base)` ×1 — all three tokens preserved through tree-shaking.
- Visual rendering identical: CSS variable values resolve to the same hex literals at render time. No customer-visible change in the live or deployed appearance.
- 5 callsites left untouched (LandingPage, Privacy, Terms, NotFound, Layout) — all use default `variant="dark"` `size="sm"`, so behavior is unchanged.

## Scope discipline

- Did NOT route through Cove subagent — pure mechanical token-routing, no design judgment, same approach as Footer commit `508d453` and Privacy/Terms commit `9fec19b`.
- Did NOT migrate to Tailwind `fill-accent` utility classes — would require adding `fill: { ... }` to `tailwind.config.js` plugin, larger surface change for marginal gain. CSS variables are already the source of truth.
- Did NOT change wordmark, polygon coordinates, viewBox, or component API — the diff is 4 insertions + 4 deletions, all on the fill values.
- Did NOT regenerate `og-card.png` — that asset is built once via PIL with hardcoded values (commit `59c297a`) and is correctly frozen at that hex. The Logo component is browser-runtime only.

## Commit

`aa7b3d9` on `autobox/strikerewind-rename`.

## What this does NOT cover

- Inline color literals elsewhere in the codebase (verified earlier: `frontend npm run build` succeeds; project-wide search would surface SVG fills in chart components, status indicators — not in scope today).
- Light-variant exercise: no caller currently uses `variant="light"`, so the dark-only path is the only one rendered live.

## Next adjacent autonomous-runnable options if `CARD ADDED: RENDER WORKSPACE` stays open longer

- Bing Webmaster Tools verification packet (mirror of GSC packet — ~30% of US search traffic non-Google; Bing also feeds DuckDuckGo and Edge defaults).
- Pre-deploy end-to-end smoke-test plan: specific URLs / specific assertions / specific failure modes, so the next autonomous run after deploy fires deterministically rather than improvising.
- PAF body-copy AI-smell sweep on the 5 calculator pages (last touched 2026-04-25).

## Cash balance

$162.45 (no spend this run).
