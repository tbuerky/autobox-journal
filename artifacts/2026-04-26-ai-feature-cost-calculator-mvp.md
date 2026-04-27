# AI Feature Cost Calculator MVP shipped — 2026-04-26

## Operator decision

Profit After Fees remains live, polished, and blocked on owner-side acquisition actions. The highest-leverage non-owner move was to create a second shot on goal instead of adding another generic Profit After Fees support page.

Chosen task: ship a public MVP for **AI Feature Cost Calculator** at:

https://profitafterfees.com/ai-feature-cost-calculator/

## What shipped

- A calculator-first public page for SaaS builders pricing AI features.
- Editable model/token-price presets.
- Inputs for prompt tokens, output tokens, AI calls per user, monthly active users, subscription price, fixed monthly AI tooling cost, and target gross margin.
- Outputs for API cost per call, AI cost per user per month, total monthly AI cost, fixed cost per user, gross margin, break-even monthly price, and target-margin price.
- Shareable scenario URLs so a builder can send one exact pricing setup to a co-founder or teammate.
- Homepage link under calculators.
- Sitemap entry and IndexNow submission.

## Public-facing quality gate

Cove and Luke were used because this was public-facing design/copy work.

- Brief: `workspace/ai_feature_cost_calculator_brief.md`
- Cove/Luke output: `workspace/cove_luke_ai_feature_cost_calculator.md`

The shipped copy avoids internal labels, process language, experiment language, and unsupported traction claims. Token prices are described as illustrative defaults, not live provider pricing.

## Verification

- Focused tests passed for the new calculation logic and content checks.
- Full suite passed: `node --test tests/*.test.js` with `100/100` tests passing.
- Production deploy succeeded and re-aliased `https://profitafterfees.com/`.
- Live page verified at `https://profitafterfees.com/ai-feature-cost-calculator/`.
- Browser QA confirmed:
  - calculator renders above the fold,
  - changing subscription price updates gross margin and share URL live,
  - no JavaScript console errors,
  - visible copy is customer-facing and not internal/process-oriented.
- Live curl checks confirmed homepage link, AI calculator page, and sitemap all return HTTP 200 and include the AI calculator URL.
- IndexNow submission returned HTTP 200.

## Revenue or traffic movement

No direct revenue or measured traffic landed in this run. The project now has a public utility aimed at AI/SaaS builders, giving the next distribution move a concrete page to share instead of only a candidate packet.

## Permission gates

No spend was made and no permission gate was crossed.

Future gate still open: if Travis wants this as a standalone brand/domain, request explicit approval before checking or buying a domain:

`APPROVED: CHECK AND BUY ONE AI COST CALCULATOR DOMAIN, MAX $15`

## Budget

Current cash balance remains **$188.75**.

## Next step

Use the live AI Feature Cost Calculator URL in a distribution/feedback packet, or if owner-side Profit After Fees Google Ads/Indie Hackers evidence arrives first, inspect that evidence before doing more parallel-build work.
