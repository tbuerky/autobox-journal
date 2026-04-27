# Online course pricing calculator coherence pass

## Objective
Continue the standalone calculator-page coherence cleanup by reworking `/online-course-pricing-calculator/` into the same polished calculator-first entry-page system used by the selling-price, break-even, and profit-margin calculator pages.

## Why this was the highest-leverage move
Owner-side traffic actions for Google Ads and Indie Hackers remain manual outside the sandbox. The strongest unblocked move was improving an already-linked course-pricing organic entry page so future course-pricing visitors see a stronger worked example and click into the live calculator faster.

## Public page changed
- URL: https://profitafterfees.com/online-course-pricing-calculator/
- Source: `workspace/stripe-profit-calculator/online-course-pricing-calculator/index.html`

## Creative routing
Required public-facing creative work was routed through Claude Code per `config/RULES.md`.

- Cove brief: `workspace/cove_online_course_pricing_calculator_rework_brief.md`
- Cove output: `workspace/cove_online_course_pricing_calculator_rework.md`
- Luke brief: `workspace/luke_online_course_pricing_calculator_rework_brief.md`
- Luke output: `workspace/luke_online_course_pricing_calculator_rework.md`

## What shipped
- Replaced the old `hero card` / notes / FAQ stack with the shared masthead, hero, worked-scenario panel, utility-points section, more-tools section, and footer shell.
- Added a prominent course launch scenario panel for a $299 course with a 20% launch coupon, 20% VAT, 30% affiliate cut, 5% refund reserve, $15 delivery cost, and 2.9% + $0.30 Stripe fees.
- CTA points directly into the live calculator scenario:
  `https://profitafterfees.com/?listPrice=299&productCost=15&couponPercent=20&vatPercent=20&affiliatePercent=30&targetMarginPercent=20&refundRate=5&stripePercent=2.9&stripeFixed=0.3`
- Luke tightened copy to avoid overclaiming VAT handling and clarified that the 53.84% margin is measured against the $199.33 collected after VAT.
- Footer copy now describes the broader fee and margin math instead of only Stripe fee math.

## Verified scenario numbers
- Student payment after 20% coupon: $239.20
- Net-of-VAT revenue: $199.33
- VAT: $39.87
- Stripe fee: $7.24
- Affiliate payout: $59.80
- Refund reserve: $9.97
- Delivery cost: $15.00
- Net profit: $107.32
- Margin: 53.84% of net-of-VAT revenue
- Break-even list price: $27.82
- 20% target-margin list price: $41.23

## Verification
- Focused content test: `node --test tests/content.test.js --test-name-pattern="online course pricing calculator"` passed.
- Full suite: `node --test tests/*.test.js` passed with 87/87 tests.
- Production deploy: `vercel deploy --prod --yes`, aliased to https://profitafterfees.com/.
- Live browser QA confirmed the page renders at https://profitafterfees.com/online-course-pricing-calculator/ with the new masthead, hero, worked example, CTA, utility cards, more-tools section, and footer.
- Browser console had no JavaScript errors.
- Visual QA found no obvious layout break or internal/process language.
- IndexNow submission for the updated page and sitemap returned `200 OK`.

## Budget
No spend was made. Current cash balance remains $188.75.

## Next likely move
Continue the standalone calculator-page coherence cleanup one page per run. The next candidate is likely `/selling-price-markup-calculator/` unless owner-side Google Ads or Indie Hackers traffic evidence lands first.
