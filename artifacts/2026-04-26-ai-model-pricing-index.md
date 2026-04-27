# AI model pricing index companion asset

## Objective
Build the no-spend AI model pricing index recommended by the directory-video review so the live AI Feature Cost Calculator has a source-linked data companion instead of another generic page.

## Shipped URL
https://profitafterfees.com/ai-model-pricing-index/

## What changed
- Added a public AI Model Pricing Index page with six source-linked rows:
  - Anthropic Claude Sonnet 4.6 — $3.00 input / $15.00 output per 1M tokens.
  - Anthropic Claude Haiku 4.5 — $1.00 input / $5.00 output per 1M tokens.
  - Anthropic Claude Opus 4.7 — $5.00 input / $25.00 output per 1M tokens.
  - Google Gemini 2.5 Flash — $0.30 input / $2.50 output per 1M tokens.
  - Google Gemini 2.5 Flash-Lite — $0.10 input / $0.40 output per 1M tokens.
  - Google Gemini 2.5 Pro — $1.25 input / $10.00 output per 1M tokens for prompts up to 200k tokens.
- Added direct scenario links from each model row into the AI Feature Cost Calculator with that model's input/output token price prefilled.
- Linked the index from the homepage calculator list and the AI Feature Cost Calculator nav.
- Added the new URL to `sitemap.xml` and submitted the new page, AI calculator, and sitemap to IndexNow.

## Source checks
- Anthropic API pricing was checked in browser at `https://claude.com/pricing` on 2026-04-26 UTC.
- Google Gemini API pricing was checked in browser at `https://ai.google.dev/gemini-api/docs/pricing` on 2026-04-26 UTC.
- OpenAI's official pricing pages were challenge-gated in the sandbox, so OpenAI rows were intentionally not included instead of publishing unsourced numbers.

## Customer-facing quality review
- Cove/Luke were routed through Claude Code for public-facing copy/layout guidance; output stored at `workspace/stripe-profit-calculator/workspace/cove_luke_ai_model_pricing_index.md`.
- Live browser review confirmed the page renders at the production URL.
- Browser copy scan found no internal/process language matching `experiment|artifact|SEO page|operator|sandbox|blocker|validation`.

## Verification
- RED: content tests failed before the page and sitemap entry existed.
- GREEN: `node --test tests/content.test.js --test-name-pattern="AI model pricing index|sitemap.xml includes the AI model pricing index|share metadata"` passed.
- Full suite: `node --test tests/*.test.js` passed `106/106`.
- Production deploy: `vercel deploy --prod --yes`, aliased to `https://profitafterfees.com/`.
- Live checks: `https://profitafterfees.com/ai-model-pricing-index/` returns HTTP 200; sitemap includes the new URL; IndexNow returned `200`.

## Revenue / traffic relevance
This gives the AI calculator a citeable data asset with source links and scenario links. It should make the parallel utility easier to share with AI/SaaS builders because the page answers the first question — "what do these models cost?" — and immediately routes readers into the calculator to test their own usage.

## Budget
No spend. Current cash balance remains `$188.75`.

## Next step
If Travis posts or shares the AI calculator/index and returns a public URL or reactions, capture that evidence first. If no owner-side evidence arrives, the next non-owner move should be a sharper distribution packet for the pricing index/AI calculator bundle or a small approval-gated standalone-domain recommendation if the index makes the AI utility feel worth separating from Profit After Fees.
