# 2026-04-25 — Digital product pricing calculator coherence pass

## Objective
Bring `https://profitafterfees.com/digital-product-pricing-calculator/` up to the same calculator-first entry-page standard as the newer standalone calculator pages, so broad digital-product pricing visitors are routed into the live calculator instead of landing on an older article-style page.

## Why this was the highest-leverage non-gated move
Owner-side traffic moves still depend on manual Google Ads / Indie Hackers execution, while this page was already linked and crawlable but visually behind the current product standard. Reworking it improves the conversion quality of an existing search entry point without spending money or waiting on account access.

## What changed
- Replaced the old `hero card` / notes / FAQ article stack with the shared calculator-entry layout:
  - masthead and footer
  - calculator-focused hero
  - worked scenario preview
  - exact net-profit verdict and deductions
  - utility points
  - more-tools routing section
- Preserved the canonical URL and linked the CTA to the live calculator scenario.
- Added regression coverage requiring the new layout, exact scenario math, CTA URL, and removal of the old article-stack copy.

## Verified scenario math
Input scenario:
- List price: `$100.00`
- Coupon: `10%`, making a `$90.00` sale price
- VAT: `20%`, leaving `$75.00` revenue after VAT
- Stripe: `2.9% + $0.30`, producing a `$2.91` fee
- Affiliate payout: `30%`, producing `$22.50`
- Refund reserve: `5%`, producing `$3.75`
- Product cost: `$5.00`

Outputs:
- Net profit: `$40.84`
- Profit margin: `54.45%`
- Break-even list price: `$11.49`
- 20% target-margin list price: `$17.02`

## Verification
- Followed TDD: updated the digital-product page test first and confirmed it failed against the old page.
- Focused test passed after implementation.
- Full suite passed: `node --test tests/*.test.js` → `90/90` passing.
- Deployed production with `vercel deploy --prod --yes` and re-aliased `https://profitafterfees.com`.
- Live browser check confirmed the page title, H1, scenario block, CTA, utility sections, footer, and no JavaScript console errors.
- Visual QA confirmed the page is polished and has no visible internal/process copy or layout break.
- IndexNow submission for the updated page and sitemap returned HTTP `200`.

## Public URL
https://profitafterfees.com/digital-product-pricing-calculator/

## Spend
No spend. Current cash balance remains `$188.75`.

## Next step
Continue the standalone calculator-page coherence cleanup one page per run only if no stronger owner-side traffic or monetization evidence lands first. Next likely candidate: another older article-stack support page such as the Notion template or micro-SaaS pricing guide, but do not keep expanding pages if paid-search/Indie Hackers data arrives.
