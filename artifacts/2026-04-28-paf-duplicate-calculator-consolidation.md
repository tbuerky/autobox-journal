# PAF duplicate calculator-pair consolidation (301 redirects)

## Why now
The remaining live PAF revenue gates are owner-side (AdSense status, StrikeSight rotation/provider/domain approvals, AI Feature Margin Check post URL). The wakeup brief was explicit that pruning, grouping, and hierarchy beats more pages or another internal doc. Three pairs of overlapping calculator pages were still cannibalizing each other in Google's index, all three pairs targeting the same calculator product with slightly different keyword framings. The TODO had this cued as the next pruning pass.

## Decisions
| Pair | Canonical (kept) | 301'd (deleted) | Rationale |
|------|------------------|-----------------|-----------|
| Course pricing | `/online-course-pricing-calculator/` | `/course-pricing/` | Calculator-first slug aligns with the actual product; matches the long-tail buyer intent "online course pricing calculator". |
| Software/SaaS pricing | `/saas-pricing-calculator/` | `/software-pricing-calculator/` | Already linked from the homepage; SaaS is the narrower, higher-intent buyer audience for this brand. |
| Transaction fee | `/transaction-fee-calculator/` | `/stripe-fee-per-transaction/` | Already linked from the homepage; broader slug can rank for both the generic and Stripe-specific queries while `/stripe-processing-fee-calculator/` keeps the Stripe-specific lane. |

## Changes
- Created `vercel.json` with six permanent redirects (with and without trailing slash) for the three loser slugs.
- Deleted `course-pricing/`, `software-pricing-calculator/`, and `stripe-fee-per-transaction/` from the deployed tree.
- Removed the three loser URLs from `sitemap.xml`.
- Removed internal links to the loser slugs from `saas-pricing-calculator/index.html`, `stripe-processing-fee-calculator/index.html`, `transaction-fee-calculator/index.html`, and `online-course-pricing-calculator/index.html`.
- Removed loser-slug-specific tests in `tests/content.test.js` (three page-content tests, three sitemap-includes tests, the three share-metadata entries, and the LLM/transaction social-card test reference).
- Added a regression in `tests/content.test.js` asserting the three loser directories do NOT exist in the source tree AND that `vercel.json` contains the three permanent redirects to the correct destinations.

## Verification
- `node --test tests/*.test.js` — `110/110` passed.
- `vercel deploy --prod --yes` — `dpl_HoTw4AFM5bkgfNhYfNhd6N9rBCJn` deployed successfully under team `travis-4599s-projects`.
- `vercel alias set ... profitafterfees.com` and `... www.profitafterfees.com` — both succeeded.
- Live HTTP checks (Vercel's `permanent: true` issues 308, which Google treats as a permanent canonicalization signal equivalent to 301):
  - `/course-pricing/` → `308` → `https://profitafterfees.com/online-course-pricing-calculator/`
  - `/software-pricing-calculator/` → `308` → `https://profitafterfees.com/saas-pricing-calculator/`
  - `/stripe-fee-per-transaction/` → `308` → `https://profitafterfees.com/transaction-fee-calculator/`
  - `/online-course-pricing-calculator/` → `200`
  - `/saas-pricing-calculator/` → `200`
  - `/transaction-fee-calculator/` → `200`
  - `/` → `200`, `/privacy/` → `200`, `/ads.txt` → `200`
- IndexNow POST for the three canonical URLs returned `HTTP 200`.

## What this changes
- Search engines see one canonical page per buyer intent for these three intent clusters. No more competing duplicates inside the same domain.
- Existing inbound link equity to the three loser URLs is preserved via the 308/301 redirect (Google passes ranking signals through permanent redirects).
- The site footer/related-page lists no longer point readers at pages that immediately bounce them through a redirect.

## Out of scope
- The `break-even-price-calculator.bak/` directory remains in source (sandbox `sudo` is password-gated). Already 404 on production and excluded from the test walker; no public exposure.
- `/stripe-processing-fee-calculator/` was kept untouched. The TODO only flagged the three pairs above; this third Stripe-specific page targets a distinct query pattern ("processing fee" vs. "transaction fee" vs. "fee per transaction") and is not duplicate content.

## Next operator move (if no fresh owner evidence lands)
Capture AdSense status / Auto Ads / impressions / eCPM once Travis provides them; integrate StrikeSight real options data on `APPROVED:`; secure `getstrikesight.com` on approval; or buy `aifeaturecost.com` on approval. If continuing the prune theme, audit `/digital-product-pricing-calculator/` for overlap with `/profit-margin-calculator/` and `/selling-price-calculator/` — but only after a fresh content read.

## Approval
None required. No spend. Current cash balance: `$188.75`.
