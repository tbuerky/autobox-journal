# Shopify Review Pulse Prospect Expansion

Date: 2026-05-13

## Outcome

Built a fresh next-target packet for Shopify Review Pulse without sending outreach, creating accounts, touching DNS, publishing publicly, or spending money.

The first-send plan is unchanged:

1. Send SellerPic only after `VERIFY GOOGLE SIGN-IN: reviewpulse@theshepherdstack.com OUTBOUND ACCESS`.
2. Wait 72 hours.
3. Use A2Reviews as the fallback second target if SellerPic does not reply.

This packet exists for the sequence after those two tests, not as permission to batch-send.

## Why This Was the Right Non-Gated Task

All current revenue motions are owner-gated:

- Google sign-in/outbound access is blocked.
- Stripe Payment Link creation is blocked.
- Founder-post publication is blocked.

The highest-value work still available inside the sandbox is improving target quality, because a better third/fourth prospect can raise the chance that the first approved email path produces a willingness-to-pay signal.

## Live Evidence Used

- Shopify says app ratings affect install likelihood and positive reviews can improve App Store search/category visibility: https://shopify.dev/docs/apps/launch/marketing/manage-app-reviews
- Shopify also says thoughtful replies to negative reviews can show other merchants that the app team is engaged: https://shopify.dev/docs/apps/launch/marketing/manage-app-reviews
- Kaching Subscriptions currently shows 623 reviews, 5.0 overall, and a visible 1-star bucket: https://apps.shopify.com/kaching-subscriptions/reviews
- Recharge Subscriptions currently shows 2,132 reviews, 4.8 overall, and a visible 1-star bucket: https://apps.shopify.com/subscription-payments/reviews
- Assortion currently shows 318 reviews and 4.9 overall: https://apps.shopify.com/assortion/reviews
- MAG Product Reviews currently shows 145 reviews and 4.6 overall: https://apps.shopify.com/product-review-myappgurus/reviews

## Reports Generated

New generated report files:

- `workspace/shopify-review-pulse/prospect-refresh-2026-05-13/kaching-subscriptions.md`
- `workspace/shopify-review-pulse/prospect-refresh-2026-05-13/subscription-payments.md`
- `workspace/shopify-review-pulse/prospect-refresh-2026-05-13/assortion.md`
- `workspace/shopify-review-pulse/prospect-refresh-2026-05-13/product-review-myappgurus.md`
- `workspace/shopify-review-pulse/prospect-refresh-2026-05-13/klaviyo-reviews.md`
- `workspace/shopify-review-pulse/prospect-refresh-2026-05-13/shopify-subscriptions.md`

Attempted but excluded:

- `rapid-reviews` returned Shopify HTTP 429 during fetch. I stopped instead of hammering the App Store.

## Ranked Expansion Targets

| Rank | App | Why It Belongs Next | Current Risk Hook | Action After First Two Tests |
|---:|---|---|---|---|
| 1 | Kaching Subscriptions | Subscription category has high merchant stakes; app is independent enough for founder/operator outreach; public page exposes strong positive language plus a visible negative edge. | The generated report found support as the strongest install driver and workflow/ease-of-use as the main visible risk; live page also exposes a 1-star bucket. | If SellerPic and A2Reviews do not reply, build a locked Kaching teaser and send one tailored email only after sender access exists. |
| 2 | MAG Product Reviews | Mid-sized app, 145 reviews, lower rating than the category leaders, and enough support complaints for a concrete $49 teardown. | Generated report found support experience as the strongest risk theme, including slow-support language. | Use as the fourth one-email test if Kaching does not reply. |
| 3 | Assortion | 318 reviews in upsell/bundles, a category where small listing improvements plausibly map to revenue. | Generated report found workflow/ease-of-use and performance/bug friction despite very strong support praise. | Keep as a later test; stronger than large incumbents but weaker than Kaching/MAG. |
| 4 | Recharge Subscriptions | Large review base and severe pricing/support themes, but lower odds of reaching a buyer through a cold lightweight report. | Public page includes 116 one-star reviews; generated report found support and workflow risk clusters. | Use only if we decide to test enterprise/large-incumbent response, not for the next one-email validation. |
| 5 | Klaviyo Reviews | Good category fit, but likely too large and process-heavy for a first-dollar cold report. | Generated report found install/import/reply-display friction, but the public page is mostly positive. | Deprioritize until after small independent apps are exhausted. |
| 6 | Shopify Subscriptions | Public pain is obvious, but Shopify is not a realistic buyer for a $49 cold teardown. | Public pages show low rating and high one-star share; generated report sampled too little text because of page shape/rate limits. | Do not contact; use only as market evidence for subscription-app pain. |

## Decision

Keep SellerPic as first send and A2Reviews as the 72-hour fallback. If both fail, the next best independent target is **Kaching Subscriptions**, not RecurrinGO, because Kaching has stronger category value, a fresher public review surface, and a sharper one-review hook around merchant loss/prevention.

No new gate is needed. The existing sender gate already controls whether any outreach can happen.

## Verification

- Ran `review_pulse.mjs` against seven live Shopify App Store candidates.
- Six report files were created under `workspace/shopify-review-pulse/prospect-refresh-2026-05-13/`.
- One candidate hit HTTP 429 and was excluded.
- No public files were changed.
- No outreach was sent.
- No spend.
