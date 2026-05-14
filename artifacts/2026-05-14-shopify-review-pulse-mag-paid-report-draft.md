# Shopify Review Pulse MAG Paid-Report Draft

Date: 2026-05-14

## Outcome

Created a private paid-report draft for **MAG: Product Reviews** as the fourth independent Shopify Review Pulse target after SellerPic, A2Reviews, and Kaching.

This does not change the current first-send sequence:

1. SellerPic first after one send gate clears.
2. Wait 72 hours.
3. A2Reviews if SellerPic does not reply.
4. Kaching only after the first two tests complete or fail.
5. MAG Product Reviews only after the earlier independent tests complete or fail.

## Why This Was the Right Task

All immediate external revenue actions remain owner-gated:

- `APPROVED: SEND SELLERPIC TEST FROM ACCESSIBLE OWNER MAILBOX`
- `VERIFY GOOGLE SIGN-IN: reviewpulse@theshepherdstack.com OUTBOUND ACCESS`
- `APPROVED: CREATE FREE TALLY INTAKE FORM FOR SHOPIFY REVIEW PULSE`
- `CREATE STRIPE PAYMENT LINK: SHOPIFY REVIEW PULSE $49 ONE-OFF REPORT`
- `APPROVED: PUBLISH SHOPIFY REVIEW PULSE FOUNDER POST`

The useful non-gated revenue work was to improve fulfillment readiness for a real follow-on prospect, not to create more public collateral or batch-send outreach.

## Live Evidence Used

- MAG Product Reviews App Store listing remains live and public: https://apps.shopify.com/product-review-myappgurus
- MAG public review page remains live and shows the review surface used for the local pull: https://apps.shopify.com/product-review-myappgurus/reviews
- Shopify says ratings and reviews can affect merchant install likelihood and App Store search/category visibility: https://shopify.dev/docs/apps/launch/marketing/manage-app-reviews
- Shopify partner guidance supports focused, useful public replies rather than defensive replies: https://www.shopify.com/partners/blog/reply-to-reviews/
- MyAppGurus publishes help content for MAG Product Reviews, supporting a self-serve setup/docs angle: https://www.myappgurus.com/blogs/mag-product-reviews

## Files Created

- `workspace/shopify-review-pulse/prospect-refresh-2026-05-14/product-review-myappgurus-latest.md`
- `workspace/shopify-review-pulse/fulfillment/mag-product-reviews-paid-report-scaffold.md`
- `workspace/shopify-review-pulse/fulfillment/mag-product-reviews-paid-report-draft.md`

## Report Angle

MAG's best public-review asset is support plus easy setup: the fresh local pull sampled 169 public review texts and found 80 positive support hits, 25 workflow/ease-of-use hits, and 17 Shopify-fit hits.

The paid-report draft frames the install risk narrowly: a few public reviews complain about slow or missing support, difficult-to-find controls, and paid-app reliability. The recommended fixes are not generic reputation advice; they focus on App Store copy, onboarding, help docs, and Shopify-safe public reply drafts.

## Verification

- Re-ran `review_pulse.mjs` against live public MAG reviews.
- Generated the paid-report scaffold from the fresh MAG pull.
- Wrote the final private paid-report draft manually from the scaffold.
- `node --check workspace/shopify-review-pulse/review_pulse.mjs` passed.
- `node --check workspace/shopify-review-pulse/fulfillment/build_paid_report_scaffold.mjs` passed.
- Confirmed `workspace/shopify-review-pulse/.vercelignore` still excludes `fulfillment/`.

## Boundaries

No outreach was sent. No public page was changed. No checkout or payment infrastructure was created. No account was created. No DNS change was made. No public post was published. No money was spent.
