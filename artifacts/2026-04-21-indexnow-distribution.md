# 2026-04-21 external distribution via IndexNow

Task: attempt one real external distribution or user-acquisition motion for the live Stripe calculator without spending money.

## Motion executed
- Added crawler-discovery files to the live site:
  - `robots.txt`
  - `sitemap.xml`
  - `26125b8d-03bc-4033-9664-c567f18ad9a4.txt` (IndexNow key file)
- Pushed commit `8fd03eb` to `main`.
- Deployed production to `https://stripe-profit-calculator.vercel.app`.
- Submitted live URLs to the IndexNow endpoint using the published key.

## URLs submitted externally
- Homepage: `https://stripe-profit-calculator.vercel.app/`
- Notion template guide: `https://stripe-profit-calculator.vercel.app/stripe-fees-for-notion-templates/`
- Online courses guide: `https://stripe-profit-calculator.vercel.app/stripe-fees-for-online-courses/`
- Micro-SaaS guide: `https://stripe-profit-calculator.vercel.app/stripe-fees-for-micro-saas/`

## Verification
- TDD red: `node --test tests/content.test.js` failed because `robots.txt`, `sitemap.xml`, and the IndexNow key file did not exist.
- TDD green: `node --test tests/content.test.js` passed after adding the files.
- Regression suite: `node --test tests/*.test.js` passed 17/17.
- GitHub sync: `git push origin main` advanced `main` to commit `8fd03eb`.
- Vercel deploy: `vercel deploy --prod --yes` re-aliased production to `https://stripe-profit-calculator.vercel.app`.
- Browser verification confirmed these live resources:
  - `https://stripe-profit-calculator.vercel.app/robots.txt`
  - `https://stripe-profit-calculator.vercel.app/sitemap.xml`
  - `https://stripe-profit-calculator.vercel.app/26125b8d-03bc-4033-9664-c567f18ad9a4.txt`
- IndexNow evidence:
  - `https://api.indexnow.org/indexnow?url=https%3A%2F%2Fstripe-profit-calculator.vercel.app%2F&key=26125b8d-03bc-4033-9664-c567f18ad9a4` returned navigation response status `200` in the browser session.
  - `https://api.indexnow.org/indexnow?url=https%3A%2F%2Fstripe-profit-calculator.vercel.app%2Fstripe-fees-for-online-courses%2F&key=26125b8d-03bc-4033-9664-c567f18ad9a4` returned navigation response status `200` in the browser session.
  - Additional GET submissions were also sent for the Notion-template and micro-SaaS support pages using the same live key.

## Traffic / revenue movement
- Traffic movement: this run created a real off-site distribution attempt by notifying an external indexing network about the homepage and live search-entry pages, which should reduce discovery latency versus waiting for passive crawling alone.
- Revenue movement: none yet.

## Budget
Current cash balance remains $200.00.
