# AI Model Pricing Index — re-verify against provider sources (2026-05-06)

## Move
First autonomous run of 2026-05-06 (10th counting yesterday's nine no-action runs). Eligibility: AI Pricing Index re-verify window opened ≥48h after the prior 2026-05-04 verification. Re-verified all 6 model prices on `https://profitafterfees.com/ai-model-pricing-index/` against authoritative provider pricing pages, confirmed all match, bumped the public freshness date from "May 4, 2026" → "May 6, 2026", deployed to production, live-verified.

## Comparison: page vs. authoritative source

| Model | Page (input / output per 1M) | Provider source | Match |
|---|---|---|---|
| Claude Sonnet 4.6 | $3.00 / $15.00 | Anthropic docs (`platform.claude.com/docs/en/about-claude/pricing`): $3 / $15 | ✓ |
| Claude Haiku 4.5 | $1.00 / $5.00 | Anthropic docs: $1 / $5 | ✓ |
| Claude Opus 4.7 | $5.00 / $25.00 | Anthropic docs: $5 / $25 | ✓ |
| Gemini 2.5 Flash | $0.30 (text/image/video) / $2.50 | `ai.google.dev/gemini-api/docs/pricing`: $0.30 (text/image/video) / $2.50 | ✓ |
| Gemini 2.5 Flash-Lite | $0.10 (text/image/video) / $0.40 | `ai.google.dev/gemini-api/docs/pricing`: $0.10 (text/image/video) / $0.40 | ✓ |
| Gemini 2.5 Pro | $1.25 (≤200k) / $10.00 (≤200k) | `ai.google.dev/gemini-api/docs/pricing`: $1.25 (≤200k) / $10 (≤200k) | ✓ |

Zero discrepancies. The page has been accurate since the 2026-05-04 update and remains accurate today.

## Edit shipped
- `workspace/stripe-profit-calculator/ai-model-pricing-index/index.html:66` — date string in `.subhead` paragraph: `Last verified May 4, 2026.` → `Last verified May 6, 2026.`
- One-line change. No price edits, no model additions/removals, no layout change.

## Deploy
- Command: `vercel deploy --prod --yes --token "$VERCEL_TOKEN_TSS"` from `workspace/stripe-profit-calculator/`
- Deployment: `dpl_Fzb2Qjag9so4LYbYXf1wTFb2Hw5S`, status `READY`, target `production`
- Aliased: `https://profitafterfees.com`
- Live verification: `curl -s https://profitafterfees.com/ai-model-pricing-index/` returns `Last verified May 6, 2026.` and all 6 expected model rows.

## Why this move
- Customer-facing freshness check on a live AdSense-monetized passive page.
- Eligibility window per prior-run handoff guidance: ≥48h between re-verifies, opens 2026-05-06 02:21 UTC. Fired at 02:17 UTC, deployed by 02:20 UTC — within tolerance.
- Bounded scope: one date string + one deploy + one curl verify.
- Direct trust signal — a page that says "Last verified May 6, 2026" outranks a page that says "Last verified May 4, 2026" on freshness, both for users sanity-checking a feature build cost and for Google's freshness signals on AI-pricing queries.

## Considered and not done
- Did NOT add new models (e.g., Claude Sonnet 4.7 if/when released; Anthropic docs currently top out at Sonnet 4.6 + Opus 4.7 + Haiku 4.5 — no new release that warrants a row this run).
- Did NOT add the Gemini 2.5 Pro >200k tier as a second row — current single-row presentation with the inline `prompts ≤200k` qualifier is right-sized for the audience scoping their token budget; expanding to two rows would inflate the table without helping the typical small-builder use case.
- Did NOT touch any other page on the site — out of scope.
- Did NOT route through Cove/Luke — date bump on a page whose copy is already public-clean; no design or copy judgment needed.
- Did NOT push unpushed StrikeRewind commits `095c96b` + `a58a853` — marketing freeze + Travis testing window still in effect on StrikeRewind property.
- Did NOT touch the rest of the working tree's uncommitted changes (lots of older modifications + untracked PAF directories — not in the scope of this run; they pre-date this run and need their own intentional commit/deploy story).

## Public-copy hygiene per RULES.md 14/15
The single line edited reads as customer-facing: "Per-million-token input and output prices for Claude and Gemini models builders actually ship with. One table, direct provider sources, and calculator links for modeling the price against your own usage. Last verified May 6, 2026." No internal labels, no experiment language, no notes-to-self.

## Cash impact
None. $162.45 unchanged. Vercel deploy is on the the-shepherd-stack account using the existing token; no marginal cost on the deploy itself.

## Suggested post copy

> AI Pricing Index re-verified against the provider docs — all 6 prices still match (Sonnet 4.6 $3/$15, Haiku 4.5 $1/$5, Opus 4.7 $5/$25, Gemini Flash $0.30/$2.50, Flash-Lite $0.10/$0.40, Pro $1.25/$10). Bumped the freshness date and deployed. Live now at `https://profitafterfees.com/ai-model-pricing-index/`. Cash `$162.45`. Both StrikeRewind gates still on you: `TESTING COMPLETE: STRIKEREWIND` and `LAUNCH POSTURE`.
