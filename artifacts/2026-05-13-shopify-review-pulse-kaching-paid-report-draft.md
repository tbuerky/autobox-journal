# Shopify Review Pulse Kaching Paid Report Draft

Date: 2026-05-13

## Outcome

Created a private paid-report draft for **Kaching Subscriptions App**, the highest-ranked expansion target after SellerPic and A2Reviews.

Primary output:

- `workspace/shopify-review-pulse/fulfillment/kaching-paid-report-draft.md`

Supporting refreshed local pull:

- `workspace/shopify-review-pulse/prospect-refresh-2026-05-13/kaching-subscriptions-latest.md`

No outreach was sent. No public page was changed. No checkout, account, DNS, or payment infrastructure was created. No spend.

## Why This Was the Right One Task

All active Review Pulse revenue motions remain owner-gated:

- `VERIFY GOOGLE SIGN-IN: reviewpulse@theshepherdstack.com OUTBOUND ACCESS`
- `CREATE STRIPE PAYMENT LINK: SHOPIFY REVIEW PULSE $49 ONE-OFF REPORT`
- `APPROVED: PUBLISH SHOPIFY REVIEW PULSE FOUNDER POST`
- `APPROVED: CREATE FREE TALLY INTAKE FORM FOR SHOPIFY REVIEW PULSE`
- `APPROVED: SEND SELLERPIC TEST FROM ACCESSIBLE OWNER MAILBOX`

The best non-gated move was to make a sellable artifact for the next independent target, not create more public collateral or run another broad market scan.

## Live Evidence Used

- Kaching's public Shopify listing showed 623 reviews, 5.0 overall, Built for Shopify status, and a visible 1-star bucket.
- The refreshed local pull sampled 559 public review text items from Kaching review pages.
- The one-star filter exposed five low-star reviews with charge amount, setup safeguard, support timing, and feature-expectation risks.
- Shopify's review-management docs say good ratings affect install likelihood, positive reviews can affect App Store search/category visibility, and app teams can reply publicly to reviews.

Sources:

- https://apps.shopify.com/kaching-subscriptions/reviews
- https://apps.shopify.com/kaching-subscriptions/reviews?ratings%5B%5D=1
- https://shopify.dev/docs/apps/launch/marketing/manage-app-reviews

## Report Positioning

The report does not pitch Kaching as a damaged app. The stronger angle is:

- Their review base is excellent.
- Support praise is the install-conversion asset.
- A small low-star bucket raises high-trust subscription-app concerns around charge amounts, setup checks, and support response.
- The practical fix is a pre-launch setup-safety message, review-reply macros, and tighter feature-expectation copy.

## Verification

- Ran `node workspace/shopify-review-pulse/review_pulse.mjs kaching-subscriptions --pages 50 --out workspace/shopify-review-pulse/prospect-refresh-2026-05-13/kaching-subscriptions-latest.md`.
- Live-opened the Shopify review page and Shopify review-management docs.
- Live-checked the one-star filtered review page.
- Confirmed the private report stays under `workspace/shopify-review-pulse/fulfillment/`, which is already excluded by `.vercelignore`.

## Next Step

Do not contact Kaching yet. First-send order remains unchanged:

1. Send SellerPic only after one of the send gates clears.
2. Wait 72 hours.
3. Use A2Reviews as fallback if SellerPic does not reply.
4. Use Kaching as the next independent target only after those first two tests fail or complete.

No new gate is needed. Existing outreach and payment gates already control the next real-world action.
