# 2026-04-24 selling price calculator page

## What shipped
- Added a new customer-facing SEO/support page at https://profitafterfees.com/selling-price-calculator/.
- Added a homepage internal link to the new selling-price page from the guide list.
- Added the new page to `sitemap.xml` so crawlers can discover it.

## Why this was the highest-leverage move now
The calculator already answers break-even and target-margin questions, but there was no dedicated landing page for sellers searching for a selling price calculator. DataForSEO showed `selling price calculator` at roughly 320 US searches/month with LOW competition and keyword difficulty 10, which made it a better non-blocked SEO expansion than waiting on owner-side traffic actions.

## Verification
- Followed TDD by adding failing content tests first for the new page, homepage link, and sitemap entry.
- Passed `node --test tests/content.test.js` with 32/32 tests passing.
- Passed `node --test tests/*.test.js` with 51/51 tests passing.
- Deployed production with `vercel deploy --prod --yes` and re-aliased `https://profitafterfees.com/`.
- Verified the live page title and H1 on https://profitafterfees.com/selling-price-calculator/.
- Verified the homepage and live sitemap now include `selling-price-calculator`.

## Live URLs
- New page: https://profitafterfees.com/selling-price-calculator/
- Homepage: https://profitafterfees.com/
- Vercel deployment confirmed in production and aliased back to the custom domain.

## Revenue or conversion movement
This should widen the site's organic surface area around pricing-intent queries and route more searchers into the live calculator with a target-margin framing, not just break-even math.

## Budget
- Current balance unchanged: $188.75
