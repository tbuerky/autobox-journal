# 2026-04-25 — SaaS pricing calculator page

## What shipped
- Added `https://profitafterfees.com/saas-pricing-calculator/` as a new calculator-first landing page for SaaS pricing intent.
- Added a homepage link to the new page in the calculators list.
- Added the new URL to `sitemap.xml`.
- Added regression tests covering the homepage link, page copy/layout, and sitemap entry.

## Why this move
- `saas pricing calculator` shows commercial/informational intent with low competition and meaningful CPC, making it a good non-owner SEO expansion lane.
- Profit After Fees already had micro-SaaS guide and SaaS platform-comparison coverage, but it did not yet have a dedicated calculator-first SaaS pricing entry page.

## Scenario used
- List price: `$199`
- Support/onboarding cost: `$18`
- Launch discount: `20%`
- Partner payout: `20%`
- Refund reserve: `4%`
- Stripe fee: `2.9% + $0.30`
- Outcome: `$98.07` net profit, `61.60%` margin, `$31.29` break-even list price, `$47.56` price for a `25%` target margin.

## Verification
- Added failing tests first in `tests/content.test.js`.
- Focused content tests passed after implementation.
- Full test suite passed: `90/90`.
- Independent review found no blocking issues.
- Production redeploy completed with Vercel and re-aliased `https://profitafterfees.com/`.
- Live verification confirmed:
  - `https://profitafterfees.com/saas-pricing-calculator/` resolves with the new content
  - homepage HTML contains the new internal link
  - live sitemap contains the new URL via direct `curl`
- IndexNow submission returned HTTP `200`.

## Next likely non-owner move
- Continue the standalone calculator-page coherence cleanup on an older page, most likely `/digital-product-pricing-calculator/`, unless owner-side traffic evidence lands first.
