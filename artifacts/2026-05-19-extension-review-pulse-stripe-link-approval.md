# Extension Review Pulse Stripe Link Approval

Date: 2026-05-19 08:17 UTC

## Task

Document the payment-closing blocker for Extension Review Pulse and raise the exact approval needed for one reusable `$49` Stripe Payment Link.

## Why This Was The Right One-Task Move

All direct revenue motions are still gated:

- `SEND: A2REVIEWS FALLBACK FROM REVIEWPULSE MAILBOX`
- `APPROVED: CONTACT ONE WORDPRESS PLUGIN AUTHOR WITH WORDPRESS REVIEW PULSE SAMPLE`
- `APPROVED: PUBLISH WORDPRESS REVIEW PULSE X POST`
- `APPROVED: CREATE WORDPRESS REVIEW PULSE $49 STRIPE PAYMENT LINK`
- `APPROVED: CONTACT ONE CHROME EXTENSION DEVELOPER WITH EXTENSION REVIEW PULSE SAMPLE`

The Extension Review Pulse public offer, locked Strawberry preview, send-control packet, prospect queue, and Strawberry paid-delivery package are already ready. If Strawberry replies yes after an approved send, the current blocker becomes payment collection. The non-gated move is to define the smallest Stripe setup before the reply arrives.

## Live Evidence Used

- Stripe's current Payment Links docs say a Payment Link creates a Stripe-hosted payment page that can be shared with customers and supports fixed-price products.
- Stripe's pricing page lists Payment Links as included with Payments for businesses on standard pricing, with the normal successful-transaction fee applying.
- Stripe's Payment Links product page says links can be shared over email and support one-time payments.

Sources:

- https://docs.stripe.com/payment-links/create
- https://stripe.com/pricing
- https://stripe.com/payments/payment-links

## Recommendation

Create one reusable Stripe Payment Link:

- Product name: `Extension Review Pulse - one extension report`
- Price: `$49.00`
- Currency: `USD`
- Type: one-time flat-rate product
- Quantity: fixed at `1`
- Customer information: collect email
- Tax/shipping: no shipping; no physical goods
- Custom domain: do not enable for this validation stage
- Post-payment invoice: do not enable unless Travis wants the optional extra Stripe invoice fee
- Coupon/discount: none
- Subscription, retainer, upsell, and customer portal: none

## Exact Approval Needed

`APPROVED: CREATE EXTENSION REVIEW PULSE $49 STRIPE PAYMENT LINK`

## What Happens Immediately After Approval

1. Create the Payment Link in the existing Stripe account.
2. Update `workspace/extension-review-pulse/fulfillment/strawberry-delivery-2026-05-19/reply-drafts.txt` so the "Interest before payment link exists" script contains the live link.
3. Update `workspace/extension-review-pulse/fulfillment/strawberry-delivery-2026-05-19/delivery-email.md` if it references payment flow language.
4. Add the link to `workspace/extension-review-pulse/README.md` as the approved payment path.
5. Do not put the live payment link on the public offer page until there is a reason to accept anonymous buyers or Travis explicitly approves a public buy button.

## Options Considered

- Reuse the WordPress Review Pulse Payment Link: rejected. Same price, but separate product naming keeps buyer receipts and manual fulfillment clean.
- Create a full public checkout CTA now: rejected. There is no approved traffic/public-sale motion yet, and the current validation is one-contact.
- Invoice manually after positive reply: acceptable fallback, but slower than a reusable link and requires more owner/manual handling.
- Wait until Strawberry replies: rejected. The report is already staged; a positive reply should move to payment without another planning run.

## Permission Boundaries

No Stripe product, price, Payment Link, checkout URL, invoice, coupon, public CTA, outreach, contact form, account, DNS change, deploy, public post, or spend was created in this run.

## Budget

Current cash balance remains `$57.18`. Creating the recommended Payment Link should add no fixed monthly charge under standard Stripe Payments pricing, but each successful payment will incur Stripe's normal transaction fee.
