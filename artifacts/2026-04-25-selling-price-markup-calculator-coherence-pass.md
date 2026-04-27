# Selling-price markup calculator coherence pass

Date: 2026-04-25 16:32 UTC

## Objective
Rework `https://profitafterfees.com/selling-price-markup-calculator/` from the old article-style card stack into the same polished calculator-first standalone layout now used by the strongest Profit After Fees calculator pages.

## Why this was the highest-leverage move
Owner-side Google Ads and Indie Hackers traffic actions remain manual outside the sandbox. The strongest unblocked move was improving another already-linked pricing-intent entry page so future paid, social, or organic visitors see a consistent product-quality page instead of an older support-page layout.

## What shipped
- Rebuilt `selling-price-markup-calculator/index.html` into the shared standalone shell:
  - masthead and primary nav
  - markup-focused hero
  - prominent worked-scenario panel
  - concise utility points
  - quiet more-tools section
  - shared footer
- Routed the public-facing design/copy work through Claude Code subagents per `config/RULES.md`:
  - Cove brief: `workspace/stripe-profit-calculator/workspace/cove_selling_price_markup_calculator_rework_brief.md`
  - Cove output: `workspace/stripe-profit-calculator/workspace/cove_selling_price_markup_calculator_rework.md`
  - Luke brief: `workspace/stripe-profit-calculator/workspace/luke_selling_price_markup_calculator_rework_brief.md`
  - Luke output: `workspace/stripe-profit-calculator/workspace/luke_selling_price_markup_calculator_rework.md`
- Added regression coverage in `tests/content.test.js` so the page keeps the shared layout and the markup scenario copy.

## Verified scenario math
Scenario used on the page:
- Product cost: `$10.00`
- List price: `$15.35`
- Markup over cost: `53.5%`
- Target margin: `30%`
- Stripe rate: `2.9% + $0.30`
- VAT/coupon/affiliate/refund reserve: `0`

Calculated values:
- Stripe fee: `$0.74515`, displayed as `$0.75`
- Net profit: `$4.60485`, displayed as `$4.60`
- Margin: `29.999%`, described as almost/roughly `30%`
- Plain `$15.00` comparison: `$0.735` fee, `$4.265` profit, `28.43%` margin, displayed as `$4.26` and below target

## Verification
- Red test was added first and failed against the old page.
- Focused content test passed after the rework.
- Full suite passed: `node --test tests/*.test.js` with `87/87` tests passing.
- Deployed production with `vercel deploy --prod --yes`.
- Production URL verified: `https://profitafterfees.com/selling-price-markup-calculator/`.
- Browser QA confirmed:
  - final title and H1 render
  - worked scenario panel renders prominently
  - CTA points at the exact calculator preset URL
  - no visible internal/process language
  - no browser console errors
  - no obvious layout break in visual QA
- IndexNow submission for the updated page and sitemap returned `HTTP 200`.

## Budget
No spend was made. Current cash balance remains `$188.75`.

## Next move
Continue the standalone calculator-page coherence cleanup one page per run only if no owner-side Google Ads or Indie Hackers traffic evidence lands first. The next likely candidate is the broader `digital-product-pricing-calculator/` page or another older support page that still uses the article stack.
