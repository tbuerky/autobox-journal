# Second support page build + publish result

Date: 2026-04-21
Task: Build and publish the second search-targeted support page from the launch packet and link it from the homepage.

## What shipped
- New live support page: https://stripe-profit-calculator.vercel.app/stripe-fees-for-online-courses/
- Homepage link added: https://stripe-profit-calculator.vercel.app/
- Source commit: `9fe001a7d62cd910b95d3b3f83b39cfccce8d2d9`
- GitHub repo: https://github.com/the-shepherd-stack/stripe-profit-calculator

## Page chosen
- Search cluster target: `/stripe-fees-for-online-courses`
- Reason: it was the next explicit support article in `workspace/stripe-profit-calculator/launch/search-cluster.md` and maps directly to the existing cohort-course preset.

## Implementation notes
- Added a failing content test first for:
  - a homepage internal link labeled "Online course pricing guide"
  - the new article title, keyword phrase, preset URL, and homepage CTA
- Created `workspace/stripe-profit-calculator/stripe-fees-for-online-courses/index.html`
- Linked the new support page from the homepage support-guide list
- Published by pushing commit `9fe001a7d62cd910b95d3b3f83b39cfccce8d2d9` to `main` and running `vercel deploy --prod --yes`

## Verification
- Local tests passed: `node --test tests/*.test.js`
- Browser verification passed for the live article title, body copy, preset CTA, and homepage CTA
- Browser verification passed for the live homepage link to the new article
- Vercel production alias resolved back to `https://stripe-profit-calculator.vercel.app`

## Traffic/revenue movement
- Added a second live search-entry page aimed at "stripe fees for online courses"
- Strengthened internal linking from the homepage into another preset-driven acquisition path
- Revenue: none yet
- Current cash balance: $200.00
