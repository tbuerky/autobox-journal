# StrikeRewind landing page — methodology block shipped

**Commit**: `8410703` on `autobox/strikerewind-rename`
**File**: `frontend/src/pages/LandingPage.tsx` (+18 / -0)
**Date**: 2026-05-01

## What shipped
A "How these numbers are calculated" panel inside the existing why-section ("The 30-delta rule is an average. You don't trade the average."), anchored directly below the example-output panel in the right column of the lg-grid. Three short paragraphs plus a not-a-forecast disclaimer line.

## Why
Pre-launch credibility gap. The example panel in that section showed three confident percentages (`82.4%`, `+3.1%`) with zero accounting for them. A skeptical retail trader reading the page would land on the example table, get to `EV%` with no definition, and bounce. The X launch post (queued in `artifacts/2026-04-30-strikerewind-x-launch-post.md`) targets exactly that audience — retail options sellers comparing this against a dozen X accounts making similar claims — so the credibility gap was the highest-conversion-leverage adjacent move while the three top-priority owner gates stay open.

## Process
1. Read the live `LandingPage.tsx` and confirmed the why-section had the credibility gap on the example panel.
2. Wrote a Luke brief at `workspace/luke_strikerewind_methodology_brief.md` with verified codebase facts (universe size, OTM grid, DTE windows, win definition, EV denominator, sample-size threshold, history windows).
3. Routed through `claude --print --permission-mode bypassPermissions` to the `luke` subagent (per `RULES.md` public-facing-copy rule). Output saved to `workspace/luke_strikerewind_methodology_output.md`.
4. Verified Luke's output against the actual engine code in `backend/src/services/newAnalysisEngine.ts` — found four factual issues, corrected them before applying.

## Factual corrections AutoBox made to Luke's draft
1. **OTM grid**: Luke wrote "1–9% OTM in 1% steps." Actual code (`newAnalysisEngine.ts:173`): `[-10, -5, 0, 5, 10, 15, 20, 25, 30]` — nine levels from 10% ITM through 30% OTM, mostly 5% steps. Reframed as "9 strike distances" without claiming the spacing pattern.
2. **DTE grid**: Luke wrote "1–8 weeks to expiration." Actual code: `[1, 4, 6, 8, 12, 24, 30, 52]` — eight windows spanning 1 week to 52 weeks. Reframed as "8 expirations, from 1 week out to 52 weeks."
3. **Data source claim**: Luke wrote "computed from end-of-day historical options chains." Current production data path uses synthetic premium estimation (`estimateCreditSpreadPremium`) with rolling historical volatility — real options chains only arrive once Polygon Starter is approved + wired. If StrikeRewind launches pre-Polygon and a sophisticated visitor fact-checks the chain claim, that's a credibility-killing overclaim. Replaced with provider-neutral "Backtest of historical price data" — accurate today, accurate post-Polygon.
4. **Win definition**: Luke wrote "expired profitable." Actual code (`newAnalysisEngine.ts:237`) for puts: `profitable = expirationPrice >= strikePrice` — i.e., short strike not breached at expiration. Tightened to "the stock closed at expiration without breaching the short strike" — same outcome in credit spread practice (premium kept = win, breach = loss) but lets a careful reader audit the claim against the code.

Luke's structure, voice, and pacing preserved exactly. The four edits are factual-accuracy corrections, not voice changes.

## Verification
- `cd frontend && npm run build` passes (1921 modules, JS `348.46 → 350.56 kB / +2.10 kB`, CSS `23.26 → 23.30 kB / +0.04 kB`).
- `cd backend && SUPABASE_URL=http://localhost:0 SUPABASE_SECRET_KEY=dev HUNT_USE_FIXTURES=1 npx tsx --test src/services/huntFixtureMode.test.ts src/services/spreadResultsService.test.ts` passes `12/12`.
- Cross-reference of every shipped numeric claim against `newAnalysisEngine.ts` and `data/sp500-tickers.ts`:
  - "full S&P 500" — `sp500-tickers.ts` has 515 entries (extra dual-class tickers) ✓
  - "144 spread setups per ticker" — 9 OTM × 8 DTE × 2 spread types = 144 ✓
  - "9 strike distances and 8 expirations" — matches arrays ✓
  - "1 week out to 52 weeks" — matches `[1,4,6,8,12,24,30,52]` ✓
  - "without breaching the short strike" — matches `expirationPrice >= strikePrice` ✓
  - "spread width minus net credit" — matches `maxLoss = NORMALIZED_SPREAD_WIDTH - normalizedPremium` ✓
  - "1, 2, 3, or 5 years" — matches Supabase migration `CHECK` clause ✓
  - "30 historical occurrences" — matches `totalTrades >= 30` filter ✓

## Public-copy hygiene per RULES.md rule 14/15
- No internal labels ✓
- No SEO scaffolding ✓
- No experiment / process language ✓
- No notes-to-self ✓
- No AI-smell phrases ✓
- No machine fingerprints (em-dash usage already established by Luke's prior April 29 landing copy) ✓
- Sentence-case headings ✓
- Reads as finished customer-facing asset ✓

## Layout note
The new panel is placed inside the same `lg:grid-cols-2 items-start` parent as the example panel, with `lg:col-start-2` to pin it to the right column on lg+ so it sits directly below the example output. On mobile it stacks naturally below.

## What this run deliberately did NOT do
- Did not address the three open owner gates (`APPROVED: DEPLOY ON VERCEL+RENDER STARTER, $7/MO`, `APPROVED: STRIKEREWIND TIER COPY + LIMITS PRE-DEPLOY`, `MIGRATION APPLIED: SPREAD_RESULTS WAREHOUSE`) — all owner-side, no autonomous action available.
- Did not touch `vercel.json` — the deploy run will rewrite it; doing it now would presume the Vercel+Render architecture choice that's still in the deploy gate.
- Did not add a pricing block — gated on `APPROVED: STRIKEREWIND TIER COPY + LIMITS PRE-DEPLOY`.
- Did not deploy — StrikeRewind is on `autobox/strikerewind-rename` and not yet on a public URL; deploy gate is open.

## State updates
- `TODO.md`: new `[DONE]` line under the dev-deps cleanup line.
- `RUNLOG.md`, `SCORECARD.md`, `HANDOFF.md`: appended.
- `OPEN_GATES.md`: unchanged (no new gate raised, no resolved gate to remove).
- `BUDGET.md`: unchanged. No spend; cash balance stays at `$162.45`.

## Next autonomous-runnable steps if approvals stay quiet
1. **On `APPROVED: STRIKEREWIND TIER COPY + LIMITS PRE-DEPLOY`** — execute the 7-step pre-baked plan from `artifacts/2026-04-30-strikerewind-tier-copy-and-limits-audit.md`.
2. **On `APPROVED: DEPLOY ON VERCEL+RENDER STARTER, $7/MO`** — execute the deploy run per `artifacts/2026-04-30-strikerewind-deploy-architecture-packet.md`. If both approvals arrive together, sequence: tier-copy fix first, then deploy, then Travis pastes the X post.
3. **On `MIGRATION APPLIED: SPREAD_RESULTS WAREHOUSE` + Polygon approval** — wire `schedulerService.ts` to the warehouse + Polygon data path.
4. **Adjacent no-approval items**: PAF AdSense impressions / eCPM passive check (needs Travis access); landing-page FAQ block routed through Luke (would address remaining objections like "Is this trading advice?", "Why historical and not real-time?", "What's required to start?").
