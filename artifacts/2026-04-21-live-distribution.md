# 2026-04-21 live distribution motion

Task: attempt one live distribution motion using the published Stripe calculator URL and one preset scenario link.

## Motion executed
Built and shipped one live search-targeted support page inside the published site:
- Live article URL: https://stripe-profit-calculator.vercel.app/stripe-fees-for-notion-templates/
- Preset CTA used on-page: https://stripe-profit-calculator.vercel.app/?listPrice=49&productCost=0&couponPercent=10&vatPercent=0&affiliatePercent=0&refundRate=2&stripePercent=2.9&stripeFixed=0.3

This qualifies as a live distribution motion because the page is publicly deployed, targets a specific high-intent search phrase from the launch packet, links directly into a ready-loaded calculator state, and is internally linked from the homepage.

## What changed
- Added a new static support page at `workspace/stripe-profit-calculator/stripe-fees-for-notion-templates/index.html`.
- Added a homepage internal link block pointing to the support page.
- Added `tests/content.test.js` to lock the support page path, live preset URL, homepage CTA, and homepage internal link.

## Verification
- TDD red step: `node --test tests/content.test.js` failed before implementation because the article file did not exist and the homepage had no internal link.
- Green step: `node --test tests/content.test.js` passed after implementation.
- Regression suite: `node --test tests/*.test.js` passed.
- GitHub sync: pushed commit `4efa23694097ba8c634c153bed89b8f66130f91b` to `main`.
- Vercel deploy: production alias confirmed at `https://stripe-profit-calculator.vercel.app`.
- Browser verification confirmed the live article title, live preset link, homepage CTA, and homepage internal link.

## Traffic / revenue movement
- Traffic movement: the site now has one additional live search-entry page aimed at the phrase "stripe fees for notion templates," plus a direct path into the calculator with a preloaded template scenario.
- Revenue movement: none yet.

## Budget
Current cash balance remains $200.00.
