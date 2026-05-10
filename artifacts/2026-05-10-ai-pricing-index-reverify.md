# AI Model Pricing Index — re-verify against provider sources (2026-05-10)

## Move
Eighth autonomous run of 2026-05-10. Re-verified all 6 model prices on `https://profitafterfees.com/ai-model-pricing-index/` against authoritative provider pricing pages. All match. Bumped freshness date "May 6, 2026" → "May 10, 2026", deployed, aliased to apex, live-verified.

## Comparison: page vs. authoritative source (2026-05-10)

| Model | Page (input / output per 1M) | Provider source | Match |
|---|---|---|---|
| Claude Sonnet 4.6 | $3.00 / $15.00 | platform.claude.com pricing table: $3 / $15 | ✓ |
| Claude Haiku 4.5 | $1.00 / $5.00 | platform.claude.com pricing table: $1 / $5 | ✓ |
| Claude Opus 4.7 | $5.00 / $25.00 | platform.claude.com pricing table: $5 / $25 | ✓ |
| Gemini 2.5 Flash | $0.30 (text/image/video) / $2.50 | ai.google.dev/gemini-api/docs/pricing: $0.30 / $2.50 | ✓ |
| Gemini 2.5 Flash-Lite | $0.10 (text/image/video) / $0.40 | ai.google.dev/gemini-api/docs/pricing: $0.10 / $0.40 | ✓ |
| Gemini 2.5 Pro | $1.25 (≤200k) / $10.00 (≤200k) | ai.google.dev/gemini-api/docs/pricing: $1.25 / $10 (≤200k) | ✓ |

Zero discrepancies vs. 2026-05-06 verify. Page accurate.

## Edit shipped
- `workspace/stripe-profit-calculator/ai-model-pricing-index/index.html:66` — date string in `.subhead`: `Last verified May 6, 2026.` → `Last verified May 10, 2026.`
- One-line change. No price edits, no model additions/removals, no layout change.

## Deploy
- `vercel deploy --prod --yes --token "$VERCEL_TOKEN_TSS"` from `workspace/stripe-profit-calculator/`.
- Deployment: `dpl_D1jABqzcn5uuQRqjBZxaD4puvjyd`, status `READY`, target `production`.
- Aliased: `https://profitafterfees.com`.
- Live verification: `curl -s https://profitafterfees.com/ai-model-pricing-index/` returns `Last verified May 10, 2026.`

## Why this move
- Customer-facing freshness check on a live AdSense-monetized passive page.
- Last verified 2026-05-06 — 4 days stale; cadence guidance was ≥48h, so well past.
- Both Travis-side gates (`ADS APPEAL`, `TESTING COMPLETE: STRIKEREWIND DATA-LIVE`) hold; piling on StrikeRewind during testing window was the wrong move. PAF EOD smoke ran two hours ago. Cron prune-verification window does not open until 2026-05-11 06:00 UTC. AI Pricing Index is the only bounded customer-facing slice not blocked.
- Direct trust signal — a "Last verified May 10, 2026" stamp outranks "May 6, 2026" on freshness signals for the page that earns AdSense.

## Considered and not done
- Did NOT add new models — Anthropic still tops out at Sonnet 4.6 / Opus 4.7 / Haiku 4.5; no Gemini additions warrant a row.
- Did NOT split Gemini 2.5 Pro into a >200k tier row — current ≤200k single-row is right-sized for the small-builder audience.
- Did NOT touch StrikeRewind (Travis-side testing window).
- Did NOT route through Cove/Luke — date bump on already-clean public copy; no design or copy judgment needed.
- Did NOT raise a new gate — autonomous and complete.

## Public-copy hygiene per RULES.md 14/15
The single edited line reads as customer-facing: "Per-million-token input and output prices for Claude and Gemini models builders actually ship with. One table, direct provider sources, and calculator links for modeling the price against your own usage. Last verified May 10, 2026." No internal labels, no experiment language, no notes-to-self.

## Cash impact
None. $162.45 unchanged. Deploy uses existing Vercel token.

## Suggested post copy

> AI Pricing Index re-verified against the provider docs — all 6 prices still match (Sonnet 4.6 $3/$15, Haiku 4.5 $1/$5, Opus 4.7 $5/$25, Gemini Flash $0.30/$2.50, Flash-Lite $0.10/$0.40, Pro $1.25/$10). Bumped the freshness date to May 10 and deployed. Live at https://profitafterfees.com/ai-model-pricing-index/. Cash $162.45. Both StrikeRewind/PAF Ads gates still on you.
