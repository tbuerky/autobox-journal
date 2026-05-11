# Shopify Review Pulse Prospect Prep

Date: 2026-05-11

## Outcome

Built the non-gated outbound prep for Shopify Review Pulse. No one was contacted.

The outreach gate is still the bottleneck:

`APPROVED: CONTACT 10 SHOPIFY APP DEVELOPERS WITH REVIEW PULSE SAMPLE`

## What Changed

- Tightened `workspace/shopify-review-pulse/review_pulse.mjs` so generic praise like "great support" no longer gets misclassified as a support risk.
- Generated prospect reports under `workspace/shopify-review-pulse/prospect-reports/`.
- Created a ranked 10-prospect target list below, using public Shopify App Store review pages and live search results.

## Prospect List

Ranked for likely response value: enough public review text, visible install-risk hook, and plausible pain around App Store conversion.

| Rank | App | Shopify reviews page | Public rating / count | Hook for outreach | Report |
|---:|---|---|---|---|---|
| 1 | SellerPic: Ads & Product Photos | https://apps.shopify.com/sellerpic/reviews | 4.5 / 101 | Clear pricing and annual-billing trust risk visible in recent reviews; concrete $49 report sample already exists. | `workspace/shopify-review-pulse/prospect-reports/sellerpic.md` |
| 2 | RecurrinGO! Subscriptions App | https://apps.shopify.com/recurring-invoices/reviews | 4.8 / 143 | Subscription apps are high-trust purchases; first-page signal includes pricing/billing trust. | `workspace/shopify-review-pulse/prospect-reports/recurring-invoices.md` |
| 3 | Trustpilot Reviews | https://apps.shopify.com/trustpilot-reviews/reviews | 1.9 / 171 from live search result | Severe public review pain: slow support, no reply, pricing/annual-plan complaints, integration failures. Large company, but the Shopify listing has urgent reputation damage. | `workspace/shopify-review-pulse/prospect-reports/trustpilot-reviews.md` |
| 4 | Tapcart - Mobile App Builder | https://apps.shopify.com/shopify-mobile-apps/reviews | 4.6 / 339 | Expensive app-builder category; even small App Store conversion gains matter. | `workspace/shopify-review-pulse/prospect-reports/shopify-mobile-apps.md` |
| 5 | Qikify Contact Form Builder | https://apps.shopify.com/contact-form-by-qikify/reviews | 4.9 / 420 | Mid-sized app with enough reviews for a useful language report and a clear workflow/customer-inquiry promise. | `workspace/shopify-review-pulse/prospect-reports/contact-form-by-qikify.md` |
| 6 | EasyReviews - Product Reviews | https://apps.shopify.com/easyreviews/reviews | 4.8 / 54 | Small enough that the developer may still care about scrappy conversion help; review text includes setup/widget friction. | `workspace/shopify-review-pulse/prospect-reports/easyreviews.md` |
| 7 | A2Reviews - Product Reviews | https://apps.shopify.com/a2reviews/reviews | 4.1 / 23 | Low review count but clear review-quality gap; cheap first validation target. | `workspace/shopify-review-pulse/prospect-reports/a2reviews.md` |
| 8 | Subi Subscriptions App | https://apps.shopify.com/subi-subscriptions-memberships/reviews | 4.9 / 863 | Just above the original 10-500 range, but subscription category has enough buyer value to justify a test. | `workspace/shopify-review-pulse/prospect-reports/subi-subscriptions-memberships.md` |
| 9 | Stamped Reviews & Loyalty | https://apps.shopify.com/product-reviews-addon/reviews | 4.7 / 3,632 | Very large incumbent; useful if the outreach angle is "sample report found export/support complaint clusters." Lower response odds. | `workspace/shopify-review-pulse/prospect-reports/product-reviews-addon.md` |
| 10 | Postscript SMS Marketing | https://apps.shopify.com/postscript-sms-marketing/reviews | 4.7 / 1,139 | High-ACV SMS category and visible billing complaint in live result; worth a lower-priority test. | `workspace/shopify-review-pulse/prospect-reports/postscript-sms-marketing.md` |

## Lower-Priority Reports Also Generated

- `workspace/shopify-review-pulse/prospect-reports/air-reviews.md`
- `workspace/shopify-review-pulse/prospect-reports/better-price-beat-any-price.md`
- `workspace/shopify-review-pulse/prospect-reports/chatty.md`
- `workspace/shopify-review-pulse/prospect-reports/judgeme.md`
- `workspace/shopify-review-pulse/prospect-reports/rivo-loyalty.md`
- `workspace/shopify-review-pulse/prospect-reports/rivyo-product-review.md`
- `workspace/shopify-review-pulse/prospect-reports/subscriptions-by-appstle.md`
- `workspace/shopify-review-pulse/prospect-reports/yotpo-social-reviews.md`

These are coherent reports, but they are weaker first outreach targets because they are either very large incumbents, have mostly positive first-page review text, or have lower obvious willingness-to-pay for a lightweight teardown.

## Live Evidence Used

- Shopify app review pages remain publicly fetchable and expose enough text for a lightweight report.
- Shopify's own developer docs say app ratings and positive reviews affect merchant install decisions and App Store placement: https://shopify.dev/docs/apps/launch/marketing/manage-app-reviews
- Search result evidence surfaced fresh review counts and pain hooks for EasyReviews, Qikify, Trustpilot Reviews, Subi, Tapcart, RecurrinGO, Postscript, and others.

Key public pages:

- https://apps.shopify.com/sellerpic/reviews
- https://apps.shopify.com/recurring-invoices/reviews
- https://apps.shopify.com/trustpilot-reviews/reviews
- https://apps.shopify.com/shopify-mobile-apps/reviews
- https://apps.shopify.com/contact-form-by-qikify/reviews
- https://apps.shopify.com/easyreviews/reviews
- https://apps.shopify.com/a2reviews/reviews
- https://apps.shopify.com/subi-subscriptions-memberships/reviews
- https://apps.shopify.com/product-reviews-addon/reviews
- https://apps.shopify.com/postscript-sms-marketing/reviews

## Outreach Copy Ready After Approval

Use one message per app. Do not send before approval.

```text
Subject: I made a public-review teardown for [APP NAME]

I am testing a tiny report for Shopify app teams: it reads public App Store reviews and turns them into install drivers, trust risks, and 3 fixes worth shipping this week.

I already made a sample from a Shopify app so you can see the shape: it is one page, not a dashboard.

For [APP NAME], the first thing I would look at is [SPECIFIC HOOK FROM PROSPECT LIST].

Would a $49 one-off report like this be useful, or is review-language analysis not painful enough to pay for?
```

## Next Step

If Travis approves the gate, send the first two messages to SellerPic and RecurrinGO using their tailored report hooks, then record replies/non-replies. If approval is still blocked, the next non-gated task should add pagination so reports can score all review pages rather than only the first public page.
