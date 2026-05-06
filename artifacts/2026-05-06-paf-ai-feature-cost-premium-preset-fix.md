# PAF — AI Feature Cost Calculator: Premium preset corrected from $15/$75 → $5/$25

**Date**: 2026-05-06 ~14:30 UTC
**Run**: 6th autonomous run of the day
**Type**: customer-facing credibility fix on a live AdSense-monetized utility
**Cash balance**: $162.45 (no spend; existing Vercel + AdSense + Render stack)

## What changed

`workspace/stripe-profit-calculator/app/ai-feature-cost.js:25-29` — the `premium` model preset on `/ai-feature-cost-calculator/` was projecting $15 / $75 per million tokens for input/output. No current frontier model from a tier-1 provider charges anywhere near that. The most expensive model on the just-verified AI Model Pricing Index (Anthropic Opus 4.7) is $5 / $25. Updated `premium` to $5 / $25 to match.

```diff
   premium: {
     label: 'Premium reasoning model',
-    inputPricePerMillion: 15,
-    outputPricePerMillion: 75,
+    inputPricePerMillion: 5,
+    outputPricePerMillion: 25,
   },
```

Also bumped a stale `Last verified May 4, 2026` assertion to `May 6, 2026` in `tests/content.test.js:982` — pre-existing breakage from run 1 of today's freshness bump on the AI Pricing Index page; same class of bug as run 5's `paf_smoke.mjs` fix.

## Why this matters

**Before**: A user picking "Premium reasoning model" projected per-call costs ~3x what any current frontier model actually charges. Someone running the math to decide whether to ship an AI feature would conclude "AI is too expensive, kill the feature" based on prices that haven't been current since 2023-era GPT-4 Turbo. That's a credibility leak on a live AdSense page that ranks for AI-pricing queries — and a quietly bad outcome for builders who trust the math.

**After**: Premium tier reflects Anthropic Opus 4.7 — the actual current premium frontier from a tier-1 provider. A user who picks Premium and projects a margin will see numbers that match what they'd actually pay if they shipped. The page's footer-note disclaimer that presets are illustrative still applies; the change is to make the "illustrative" example point at a real model.

This aligns with the wakeup-prompt directive to prefer **quality control** over endless on-site SEO page expansion. No new pages, no new sections — one number trio fixed, on a live customer-facing tool.

## Tests + deploy

- 110/110 tests pass after the change (`ai-feature-cost.test.js` 3/3, `scenarios.test.js`, `verdict.test.js`, `calc.test.js`, `content.test.js`).
- Deploy: `vercel deploy --prod --yes --token "$VERCEL_TOKEN_TSS"` from `workspace/stripe-profit-calculator/` → `dpl_41BjA4FAb7XAQPdvVXgzRBjaahUM` `READY production`. Aliased to `https://profitafterfees.com` (`vercel alias set ... profitafterfees.com`). Live `app/ai-feature-cost.js` confirms `inputPricePerMillion: 5` + `outputPricePerMillion: 25` under the `premium` key.

## What this does NOT change

- `low-cost` preset stays at $0.15 / $0.60 — still corresponds to a real OpenAI offering (GPT-4o-mini-class). Not stale.
- `mid-tier` preset stays at $3 / $15 — matches Anthropic Sonnet 4.6, the current verified mid-tier reasoning frontier.
- Default scenario values, copy, layout, FAQ, AI Pricing Index page — all untouched. Single bounded change.

## Considered and rejected

- **Renaming the dropdown options to specific model names** (e.g. "Anthropic Opus 4.7" instead of "Premium reasoning model"). Rejected — locks the preset to a single named model and creates a freshness debt every time pricing or model lineup shifts. The current generic labels with editable presets are the right pattern.
- **Updating low-cost from $0.15 / $0.60 to $0.10 / $0.40** to align with Gemini Flash-Lite (the cheapest model on the verified Pricing Index). Rejected — $0.15 / $0.60 still corresponds to a real model (GPT-4o-mini); changing it adds risk without obvious benefit.
- **Adding a "verified date" line to the calculator page itself**. Rejected — the existing footer-note explicitly warns that presets are illustrative defaults, which is the right posture; a verified date implies the presets ARE current pricing and would create the same freshness debt.
- **Routing through Cove or Luke**. Rejected — single-number numeric correction with no copy or layout judgment needed; not a creative-work task.

## Public-copy hygiene per RULES.md 14/15

- No internal labels, experiment language, or scaffolding copy added or changed. Only numeric preset values updated. Page copy continues to disclaim presets as illustrative.

## Next-run guidance

- Run 5's eligibility table from earlier today still holds for the rest of the day, with this run consuming the "find a real bounded improvement" slot:
  - **Now through 2026-05-06 20:17 UTC**: queue is now genuinely empty for this window. If owner replies on either StrikeRewind gate, resume launch-readiness work. Otherwise prefer no-action with a documented blocker over piling another move on top.
  - **2026-05-06 20:17 UTC onward**: StrikeRewind end-of-day smoke re-run via `workspace/strikerewind_smoke.mjs` (12h cadence since 08:17 UTC).
  - **2026-05-06 end of day after both smokes clean**: delete `config/TODO.md.bak-pre-cleanup` + `config/HANDOFF.md.bak-pre-relocate` rollback artifacts.
  - **2026-05-08 02:17 UTC onward**: AI Model Pricing Index re-verify (≥48h cadence).

## Suggested post copy

> Fixed a credibility leak on `/ai-feature-cost-calculator/`: the "Premium reasoning model" preset was projecting $15/$75 per million tokens — 3× higher than any current frontier model. Updated to $5/$25 (Anthropic Opus 4.7 — the most expensive entry in the just-verified pricing index). Tests 110/110 green. Deployed `dpl_41BjA4FAb7XAQPdvVXgzRBjaahUM`. Cash $162.45. Both StrikeRewind gates still on you.
