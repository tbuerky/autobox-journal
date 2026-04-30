# StrikeSight Hunt rebuild — dense sortable data table

Date: 2026-04-29
Branch: `autobox/strikesight-scanner-mvp`
Commit: `e8a3572`
File: `frontend/src/pages/Hunt.tsx` (`+247 / -285`, net `-38`)

## What changed

### Killed
- `framer-motion` `<motion.div>` swipeable card per opportunity
- `AnimatePresence` directional card transitions (`x: 300 → x: -300`)
- `currentCardIndex`, `nextCard`, `prevCard`, dot-pagination row
- 600px tall single-card hero with `text-8xl` EV display
- Setup form's `motion.div` fade/translate wrapper
- All emerald-glow markup-layer styling on cards (panels now use `.panel`)
- The `framer-motion` import is gone from this file (still in `package.json` for other pages)

### Built
Desktop (`md:` and up): a single sortable table with 7 columns —
| Column | Type | Sortable |
|---|---|---|
| Ticker | with company subtitle | yes (asc default) |
| Strategy | `formatStrategyDisplay` output | no |
| Exp | weeks, right-aligned, `.num` | yes (desc default) |
| Win% | right-aligned, `.num` | yes (desc default) |
| EV% | right-aligned, `.num text-pos`, signed | yes (desc default — initial sort) |
| Credit | `$xx.xx`, right-aligned, `.num` | yes (desc default) |
| Action | `Analyze` button → `/analysis/:ticker` | no |

Mobile (`<md`): same data as a stacked list of `.panel` cards with a sort-chip row above them (`EV% / Win% / Credit / Exp`); each card shows ticker, signed EV%, strategy line, three-up Exp/Win/Credit grid in `.num`, and a full-width `Analyze {ticker}` button.

Empty state: simple panel with `Target` icon, "No matches found", "Adjust criteria" button. Cache state: `Cached Nm ago` chip + `RefreshCw` icon. Header still has `New hunt` link.

Setup form: same controls (5 sliders + strategy-type tri-button + index list), now wrapped in `.panel p-6` instead of `bg-dark-card border-gray-800 rounded-xl`; range tracks switched to `bg-bg-elevated`; selected buttons use `border-accent bg-accent-soft text-accent`; unselected `border-border-subtle text-fg-secondary hover:border-border-strong`. CTA `bg-accent text-bg-base rounded` instead of `rounded-xl`; loading state shows the same cycling scan messages but in plain `<span>` instead of `motion.div`.

### Sort behavior
Default: `evPercent` desc. Click a sortable header (`Ticker`, `Exp`, `Win%`, `EV%`, `Credit`):
- if not currently sorted by it → switch to that key, default direction (asc for `ticker`, desc for the rest)
- if already sorted by it → toggle direction
Sort indicator: `ArrowUp` / `ArrowDown` lucide icon next to the active column header in `text-accent`. Mobile chips show `↑` / `↓` glyphs.

## Why this run

HANDOFF locked the Cove design direction on 2026-04-28 ("Hunt results: dense sortable data table … not swipeable cards") and the design tokens were shipped on the prior run (commit `e8b805d`). That made step #3 of the locked build queue the right autonomous next move:
- step #1 (Supabase `spread_results` warehouse table) is gated on Travis applying SQL via the dashboard
- step #2 (Cove design tokens) shipped last run
- step #3 (Hunt rebuild as data table) is unblocked and uses the just-shipped tokens
- step #4 (routing restructure) and step #5 (Luke landing copy) downstream of #3

Doing #3 now also makes #5 (Luke pass on landing copy) and step #6 (Ticker Analysis as a similar dense matrix) reference the same table-grade visual language instead of two disconnected anchors.

## Verification

- `cd frontend && npm run build` → passes; bundle `446.16 kB` js / `25.94 kB` css
- `cd backend && npm run build` → passes
- `npx tsx --test src/services/huntFixtureMode.test.ts` (with `HUNT_USE_FIXTURES=1`, only `SUPABASE_URL` + `SUPABASE_SECRET_KEY` set) → `3/3 pass`
- `grep framer-motion frontend/src/pages/Hunt.tsx` → zero matches
- `grep "currentCardIndex\|swipeable" frontend/src/pages/Hunt.tsx` → zero matches
- 54 occurrences of design tokens (`panel|num|border-subtle|accent`) in the new file

## Public-facing copy review

Per RULES.md rule 14/15: the new strings on this page are short, customer-facing, and stay product-shaped. No internal labels, experiment language, SEO scaffolding, or process notes. The phrases used are:
- `Run a hunt`
- `Set your criteria. The scanner returns ticker-specific credit spreads that have historically beaten generic delta/DTE rules.`
- `Hunt results` / `Sort by:`
- `Hunting...` / scan-message rotation (existing strings)
- `No matches found` / `Try loosening your criteria.` / `Adjust criteria`

These are tighter than the prior copy ("Hunt Your Setup", "Define your criteria and find matching opportunities") and match the product positioning locked in HANDOFF: "scans the whole S&P, returns exact strikes and expirations that have been consistently profitable over time."

The Hunt page is not yet on a public URL — it's behind auth on the `autobox/strikesight-scanner-mvp` branch. Once routing restructure (step #4) and the Luke landing-copy pass (step #5) ship and the app deploys to StrikeRewind.com, this Hunt UI is what an authenticated user sees after running a scan.

## Next step

Step #4 from the build queue: restructure routing — `/` becomes the unauthenticated landing shell, `/dashboard` becomes the authenticated home (today's top signal + watchlist quick-view + Run Hunt CTA), `/hunt` stays as the scanner. This is autonomous-runnable; no Travis approval required. After that, step #5 (Luke landing copy pass) is route-able to Luke per RULES.md as the first public-facing copy work on StrikeRewind.

Open owner gates unchanged:
- `ROTATED: STRIKESIGHT KEYS READY` (rotate the leaked Xata API key in Xata dashboard)
- `APPROVED: SUBSCRIBE POLYGON STARTER, $29/MO` — wait until pre-launch testing per Travis direction
- Apply `spread_results` Supabase migration via dashboard, or grant explicit consent for AutoBox to author the migration file

Current cash balance: `$162.45`. No spend.
