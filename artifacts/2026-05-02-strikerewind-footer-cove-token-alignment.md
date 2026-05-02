# StrikeRewind — Footer Cove-token alignment (last legacy-token surface)

## Date
2026-05-02 (later x5)

## Why this run
- One open gate: `CARD ADDED: RENDER WORKSPACE` (owner-only, blocks deploy pipeline step 2).
- Prior run flagged Footer.tsx as the explicit next-adjacent option: "still uses legacy `bg-[#0a0a0a]` / `border-[#1a1a1a]` / `text-neutral-*` — flagged for next adjacent run." Privacy + Terms moved to Cove tokens in commit `9fec19b` 2026-04-30; Footer was the only remaining public-facing surface still on legacy non-Cove tokens.
- Customer-visible polish on the conversion-path footer that ships on every public page (`LandingPage.tsx`) and authenticated page (`Home.tsx`). Highest-leverage no-approval move that doesn't drift into PAF audit territory.

## Edit
`frontend/src/components/Footer.tsx` (4 lines changed):

| Was (legacy / arbitrary value) | Now (Cove token) | Why |
|---|---|---|
| `bg-[#0a0a0a]` | `bg-bg-surface` | Mirrors LandingPage header `bg-bg-surface`; gives footer slight elevation against `bg-bg-base` page |
| `border-[#1a1a1a]` | `border-border-subtle` | Matches header `border-border-subtle` |
| `text-neutral-500` | `text-fg-muted` | Copyright line → muted text scale |
| `text-neutral-400` (×2) | `text-fg-secondary` | Terms / Privacy links → secondary text scale |
| `hover:text-white` (×2) | `hover:text-fg-primary` | Hover state → primary text scale |

Copy unchanged (`© {year} StrikeRewind. All rights reserved.` + `Terms of Service` + `Privacy Policy`).

## Verification
- `cd frontend && npm run build` clean: 1921 modules, JS `353.70 kB` (flat), CSS `23.30 → 22.83 kB` (`-0.47 kB` from purged arbitrary-value utilities).
- `cd backend && npx tsx --test src/services/huntFixtureMode.test.ts src/services/spreadResultsService.test.ts` passes 12/12.
- `grep -E "bg-\[#0a0a0a\]|border-\[#1a1a1a\]|text-neutral-[345]00|hover:text-white"` against `frontend/src` returns **0 matches** — entire frontend is on Cove tokens.
- Public-copy hygiene per RULES.md rule 14/15: no copy changed (token-swap only). Re-read renders fine — no AI-smell, no internal labels, no SEO scaffolding, no process language.

## Deliberately not done
- Did NOT route through Cove subagent — pure mechanical token-swap, not design judgment. Same approach as the Privacy/Terms tokenization in commit `9fec19b`.
- Did NOT change footer copy or layout — out of scope; rule of "one logical unit per run."
- Did NOT touch any non-frontend file.

## Outcome
Commit `508d453` pushed to `autobox/strikerewind-rename`. Will ship automatically on next deploy (Render gate still open). Closes the last legacy-token surface on the StrikeRewind customer-facing chain.

## Cash balance
$162.45 (unchanged)
