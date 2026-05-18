# WordPress Review Pulse Stripe Link Approval Packet

Run: 2026-05-18 20:19 UTC

## Task

Remove the next payment blocker for WordPress Review Pulse without crossing the payment-infrastructure permission gate.

## Recommendation

Create one Stripe Payment Link for `WordPress Review Pulse - one plugin report` at `$49.00` one-time, then wire the live WordPress Review Pulse request CTA and the SEOPress reply/delivery scripts to that link.

Approval line:

`APPROVED: CREATE WORDPRESS REVIEW PULSE $49 STRIPE PAYMENT LINK`

## Why this matters now

The WordPress offer is public and the SEOPress preview, send-control packet, and paid-delivery package are ready. The current CTA asks prospects to email for the report, and the fulfillment notes correctly say to deliver only after payment, explicit sample approval, or a positive reply asking for the full report.

That leaves a closing gap: if SEOPress or another approved one-contact prospect replies "yes, send it" or "how do we buy?", the system currently needs another owner/payment step before it can collect the $49. A live Payment Link would make the first positive reply immediately closeable.

## Options considered

1. **Keep email-only until a buyer asks.** Lowest setup friction, but it creates a delay at the highest-intent moment.
2. **Create a Stripe Invoice per prospect.** Useful for a named customer, but slower and less reusable for the public offer.
3. **Create one reusable Stripe Payment Link.** Best fit for this stage: no-code, reusable, Stripe-hosted checkout, can be shared by email and linked from the site.

## Live evidence

- Stripe docs describe Payment Links as a Stripe-hosted no-code payment page that can be shared in emails or on a website.
- Stripe docs say Payment Links can sell products or subscriptions at a fixed price, can be shared multiple times, and can be embedded as a buy button.
- Stripe pricing says Payment Links are included with Payments at no additional charge for standard payments pricing. Payment processing fees still apply.

Sources:

- https://docs.stripe.com/payment-links
- https://docs.stripe.com/no-code/payment-links
- https://stripe.com/pricing

## Exact setup

- Product name: `WordPress Review Pulse - one plugin report`
- Price: `$49.00`
- Type: one-time
- Quantity: fixed at `1`
- Success message: `Thanks - reply to the delivery email with your WordPress.org plugin URL and the decision you want the report to support.`
- Required customer fields: email
- Optional metadata if available: `lane=wordpress_review_pulse`, `offer=one_plugin_report`
- Do not enable a custom Stripe-hosted payment domain; Stripe pricing lists that as `$10/mo`, and it is not needed for this validation stage.
- Do not create subscriptions, coupons, upsells, invoices, or a customer portal for this first test.

## Immediately after approval

1. Create the Stripe Payment Link in the existing Stripe account.
2. Update `workspace/wordpress-review-pulse/index.html` so the request CTA points to the live payment link, while preserving an email fallback for preflight questions.
3. Update `workspace/wordpress-review-pulse/fulfillment/seopress-delivery-2026-05-18/reply-drafts.txt` and `delivery-email.md` to include the payment link in "how do we buy?" and paid-delivery flows.
4. Deploy the WordPress Review Pulse site and verify the live CTA, sample page, sitemap, and locked preview.
5. Record the Payment Link URL, Stripe object IDs, and any payment receipt handling instructions in the private fulfillment docs.

## Permission boundary

No Stripe product, price, Payment Link, checkout URL, invoice, coupon, account setting, or public CTA was created or changed in this run. No outreach, contact-form submission, public post, DNS change, account creation, or spend happened.

Current cash balance: `$57.18`.
