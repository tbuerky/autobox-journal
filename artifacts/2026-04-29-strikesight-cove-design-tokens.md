# StrikeSight: Cove design tokens shipped

## What this is
Step #2 from the StrikeSight build queue locked into `HANDOFF.md` on 2026-04-28: **foundational design tokens** in `frontend/tailwind.config.js` and `frontend/src/index.css` so the upcoming Hunt-as-data-table rebuild and landing page copy rewrite reference one consistent system. Without this layer, every subsequent UI change would have to re-derive colors, type, and surface decisions ad hoc.

This is fully implementable in code — no Travis approval needed, no spend.

## Why this is the right run
Travis priority shift (interactive 2026-04-28) puts StrikeSight on ~90% bandwidth on a "build → polish → deploy → market" path. The HANDOFF locked the build order: (1) Supabase `spread_results` warehouse table, (2) **Cove design tokens**, (3) Hunt as dense data table, (4) routing restructure, (5) Luke landing copy.

Item #1 needs Travis to deploy SQL via the Supabase dashboard. Item #2 is fully autonomous. It is also a **prerequisite** for items #3 and #5 — the dense Hunt data table and the landing page need the new color/type system in place before either is built. Doing #2 first means #3 and #5 can both reference one anchor and don't drift apart.

The wakeup brief explicitly favors stronger design + product copy over more pages or more internal docs. This run is design-system foundation, not a page expansion or another SEO doc.

## Cove design direction this run lands
From the 2026-04-28 Cove design audit (recorded in `STATE.md` and `HANDOFF.md`):
- Institutional fintech aesthetic: `#0B0F14` background, layered near-black surfaces, `#111821` panels.
- JetBrains Mono or IBM Plex Mono for ALL numeric content.
- Replace Tailwind emerald everywhere with restrained `#22C55E` used sparingly.
- `rounded-md` not `rounded-2xl`.
- Remove emerald glow effects.

This run lands every one of those at the token layer. Subsequent passes apply them at the markup layer page by page.

## What changed

### `frontend/tailwind.config.js`
- `emerald` color value swapped from `#10b981` → `#22C55E`. Backwards-compat: existing references in 12 `.tsx` files (`Layout`, `SuccessRateIndicator`, `TickerInput`, `Home`, `Hunt`, `Analysis`, `Watchlist`, `Account`, `Scanner`, `Privacy`, `Terms`, plus `index.css`) now render restrained green without any markup change.
- New semantic tokens: `accent`, `accent-soft` (12% green wash for hover/active states), `pos`, `neg`, `warn`.
- Layered surfaces: `bg-base`, `bg-surface`, `bg-panel`, `bg-elevated`. `dark-bg` aliased to `#0B0F14`, `dark-card` aliased to `#111821` (backwards-compat).
- Border scale: `border-subtle` `#1C2430`, `border-strong` `#27313F`.
- Text scale: `fg-primary` `#E6EAF0`, `fg-secondary` `#A4ADBA`, `fg-muted` `#6C7685`.
- `fontFamily`: `mono` and `num` both map to `JetBrains Mono → IBM Plex Mono → ui-monospace → SFMono-Regular → Menlo → monospace`.
- `borderRadius.DEFAULT` reduced to `0.375rem` (`rounded-md`).

### `frontend/src/index.css`
- Added Google Fonts import for JetBrains Mono `400/500/600/700`.
- New `:root` CSS custom properties expose every token (`--bg-base`, `--bg-panel`, `--accent`, `--pos`, `--neg`, `--fg-primary`, etc.) so non-Tailwind components and inline `style={}` references can use the same anchors.
- `html, body` now resolve to `var(--bg-base)` / `var(--fg-primary)` — replaces the literal `#000000` background.
- New `.num` utility class: applies `font-num` plus `font-variant-numeric: tabular-nums` plus `font-feature-settings: "tnum" 1` so every numeric cell (win rate, EV%, strikes, credits) anchors on a single rule.
- New `.panel` and `.panel-elevated` component classes encapsulate the standard panel surface + subtle border at `rounded-md`. Subsequent Hunt-as-data-table pass can use `.panel` for the criteria rail and the results frame without re-deriving.
- Removed the emerald `box-shadow: 0 0 60px rgba(16, 185, 129, 0.05)` glow on the main container at `lg+` breakpoint (Cove explicit removal).
- Removed the emerald glow on `.slider:hover` thumb states (Cove explicit removal).
- Slider thumb border switched from hardcoded `#000` to `var(--bg-base)` so the thumb reads as cut out of the new institutional background, not floating on a different one.

### What did NOT change this run (deliberate scoping)
- No `.tsx` files were edited. Every existing `text-emerald` / `bg-emerald` / `border-emerald` / `bg-dark-bg` / `bg-dark-card` reference in 12 files now renders against the new tokens automatically. This is the correct scope for one autonomous run — markup-level passes are page-by-page work that belongs in the Hunt-data-table rebuild and landing page rewrite.
- The Tailwind keyframe animations `fade-in` and `slide-up` were preserved. Cove's "remove framer-motion page fades" is a separate markup-layer concern (framer-motion is its own library, unrelated to Tailwind's `animate-*` classes). When the routing restructure runs, the framer-motion `motion.div` page transitions can be removed in that pass.

## Verification
- `cd /home/autoproj/projects/StrikeSight/frontend && npm run build` → passes; bundle `dist/assets/index-lA3V66Oj.js 445.78 kB` (gzip 139.72 kB), CSS `dist/assets/index-CDrXkVds.css 24.33 kB`.
- `cd /home/autoproj/projects/StrikeSight/backend && npm run build` (tsc) → passes.
- Compiled CSS bundle:
  - `#22C55E` (new restrained accent): 10 occurrences (every `text-/bg-/border-/ring-emerald` rule and hover variant resolved correctly).
  - `#10b981` (old Tailwind emerald): 0 occurrences (token swap complete at the rendered level).
  - `#0B0F14` (institutional bg): present.
  - `#111821` (panel): present.
  - `JetBrains Mono`: present in `@font-face` rule.

Visual rendering review under a real browser is queued for the next session that has a browser; an autonomous run cannot perform a screenshot-grade design check.

## Git
- Commit: `e8b805d` on `autobox/strikesight-scanner-mvp`.
- Pushed to `https://github.com/tbuerky/StrikeSight`.
- Diff: `2 files changed, 85 insertions(+), 31 deletions(-)`.

## Recommendation
No new approval gate from this run. Owner-side gates open and unchanged: `ROTATED: STRIKESIGHT KEYS READY` (rotate the leaked Xata API key in Xata dashboard so it's invalidated), `APPROVED: SUBSCRIBE MARKETDATA.APP TRADER ...` or `APPROVED: SUBSCRIBE POLYGON STARTER ...` (paid options chain data; Polygon Starter `$29/mo` is the working assumption per `STATE.md`), `APPROVED PAF FIX CONVERSION` already shipped earlier.

The next autonomous run should pick up step #3 (rebuild Hunt results as a dense sortable data table — `Ticker | Strike | Exp | Win% | EV% | Credit | Action`) using the `.panel` / `.num` / `border-subtle` / `accent` tokens this run shipped, plus the framer-motion glow removal at the Layout/Hunt markup layer. Step #1 (Supabase `spread_results` warehouse table) becomes ready when Travis can run a SQL migration in the Supabase dashboard or replies with consent for AutoBox to author the migration file for him to apply.

Current cash balance: `$162.45`. No spend this run.
