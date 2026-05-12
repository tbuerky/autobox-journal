# Shopify Review Pulse payment-link recommendation

Date: 2026-05-12

## Recommendation

Create one Stripe Payment Link for the Shopify Review Pulse one-off report after the outbound mailbox exists, then add that link to the public offer page and the SellerPic follow-up path.

Product:

- Name: Shopify Review Pulse report
- Price: $49 USD
- Type: one-off product, not subscription
- Description: One public-review teardown for one Shopify App Store listing, delivered within one business day when the review corpus is sufficient.

## Why Stripe Payment Links

- Stripe's docs describe Payment Links as no-code hosted payment pages that can be shared with customers. That is enough for a manual $49 first sale without building checkout.
- Stripe Payment Links support one-off products with flat-rate prices, which matches this report better than a subscription.
- Stripe lists Payment Links as included with Payments on standard pricing, so there is no extra monthly software cost beyond normal payment processing.
- PayPal links are also viable, but Stripe is the cleaner first choice because the broader project already has Stripe operational familiarity and the buyer experience is a hosted checkout rather than an email-money feel.

## Options considered

1. **Stripe Payment Link — recommended.** Fastest credible first-dollar path. No backend required. Easy to paste into email and the public page once Travis approves payment setup.
2. **PayPal Payment Link.** Also no-code and shareable, but less consistent with the existing project stack and more likely to feel like an ad hoc payment request.
3. **Manual invoice after a positive reply.** Lowest setup, but adds friction exactly when a prospect says yes.
4. **Full embedded checkout.** Overbuilt before the first paid report exists.

## Implementation after approval

1. Travis creates the one-off Stripe Payment Link in the Stripe Dashboard.
2. Add the live link to `workspace/shopify-review-pulse/offer.html` as the primary CTA.
3. Add the same link to `workspace/shopify-review-pulse/outreach/sellerpic-first-email.md` only if the mailbox is already connected and Travis wants the first email to accept payment directly.
4. Redeploy `workspace/shopify-review-pulse/` to Vercel.
5. Update the SellerPic send kit with the final payment URL and send policy.

## Approval line

`CREATE STRIPE PAYMENT LINK: SHOPIFY REVIEW PULSE $49 ONE-OFF REPORT`

## Sources

- Stripe Payment Links docs: https://docs.stripe.com/payment-links/create?pricing-model=standard
- Stripe pricing page: https://stripe.com/pricing
- PayPal Payment Links help: https://www.paypal.com/us/cshelp/article/how-do-i-create-a-pay-link-and-button-help262
- PayPal Payment Links product page: https://www.paypal.com/us/business/accept-payments/payment-links
