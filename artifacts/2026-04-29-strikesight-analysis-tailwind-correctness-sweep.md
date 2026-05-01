# StrikeSight — Analysis.tsx Tailwind utility correctness sweep

## What
Replaced 8 broken raw `border-subtle` / `border-strong` references in `frontend/src/pages/Analysis.tsx` with the working utility forms `border-border-subtle` / `border-border-strong`.

## Why
The previous run (Watchlist Cove pass, commit `d92db10`) caught a real bug while doing a compiled-CSS audit: the colors in `frontend/tailwind.config.js` are *named* `border-subtle` and `border-strong` (with the hyphen). Tailwind utilities follow the shape `{prefix}-{color-name}`, so the working class for the subtle border color is `border-border-subtle`, not `border-subtle`. The unprefixed forms were silently no-op — they generated no CSS rule. The `.panel` component class sets `border: 1px solid var(--border-subtle)` directly via CSS custom properties, so panel-bordered surfaces still rendered. But raw utility usage outside `.panel` — on the spread summary card, ticker masthead bottom border, the watchlist toggle button, two analysis-parameter selects, and three table-row borders — was rendering with `border-color: currentColor` instead of `#1C2430`. A user landing on `/analysis/:ticker` from the dashboard `Confirm on {ticker}` CTA was being shown rules in foreground text color rather than the intended subtle slate.

## Changes
File: `frontend/src/pages/Analysis.tsx` (`+8 / -8`)

Lines fixed:
- L189 — spread summary card: `border border-subtle` → `border border-border-subtle`
- L260 — ticker masthead bottom rule: `border-b border-subtle` → `border-b border-border-subtle`
- L290 — watchlist toggle (off state): `border-subtle hover:border-strong` → `border-border-subtle hover:border-border-strong`
- L313, L328 — analysis-parameter selects: `border border-subtle` → `border border-border-subtle` (replaceAll)
- L398 — best-strategy summary tile: `border border-subtle` → `border border-border-subtle`
- L452 — top-strategies table head row: `border-b border-subtle` → `border-b border-border-subtle`
- L462 — top-strategies table body rows: `border-b border-subtle last:border-b-0 hover:bg-bg-surface` → `border-b border-border-subtle last:border-b-0 hover:bg-bg-surface`

## Verification
- `cd frontend && npm run build` passes — bundle `dist/assets/index-Dm-IF5aq.js 452.25 kB` (essentially flat from `452.19 kB`); CSS `25.89 kB` unchanged.
- `cd backend && npm run build` (tsc) passes.
- `SUPABASE_URL=http://localhost:0 SUPABASE_SECRET_KEY=dev HUNT_USE_FIXTURES=1 npx tsx --test src/services/huntFixtureMode.test.ts` passes 3/3.
- Compiled CSS audit on `dist/assets/index-CcDyrj8x.css`:
  - `.border-border-subtle` ✓ present
  - `.border-border-strong` ✓ present
  - `.hover\:border-border-strong` ✓ present
  - `.divide-border-subtle` ✓ present (used by Watchlist)
  - `.border-subtle` / `.border-strong` ✗ absent (correct — they were never generated; that was the whole bug)
- `grep -rE '(^|[ "])(border|divide|hover:border)-(subtle|strong)([ "]|$)'` across `frontend/src` returns no matches — no remaining bad references anywhere in the project.

## Public-copy hygiene
No copy changes. Authenticated UI; this run is purely a CSS-correctness fix on existing markup. Per `RULES.md` rules 14/15, nothing customer-facing was added or modified.

## Commit
`117e11f` — pushed to `origin/autobox/strikesight-scanner-mvp`.

## Cash balance
$162.45. No spend.
