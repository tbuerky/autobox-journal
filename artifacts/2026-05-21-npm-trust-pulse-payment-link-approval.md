# NPM Trust Pulse Payment Link Approval Packet

Date: 2026-05-21 06:18 UTC

## Task

Resolve the next revenue bottleneck for the live NPM Trust Pulse offer without crossing the payment-infrastructure permission gate.

## Current State

- Live offer: `https://npm-trust-pulse.vercel.app/`
- Request page: `https://npm-trust-pulse.vercel.app/request`
- Current price shown publicly: `$49` one-off for one npm package report.
- Current buyer path: visitors open a prefilled email request; the page says payment instructions are sent after package-fit confirmation.
- Existing external-action gate remains: `APPROVED: CONTACT RESEND WITH NPM TRUST PULSE SAMPLE`.

The public site can describe the offer, but it cannot currently accept money without a manual reply and a later payment step. For a low-touch operator lane, that is the most important conversion gap.

## Live Evidence

- Stripe Payment Links are a no-code Stripe-hosted checkout surface for selling a product or service from a reusable link: `https://docs.stripe.com/payment-links`.
- Stripe docs say Payment Links can be shared on a website or in email, support automatic receipts, and can use dynamic payment methods without custom code: `https://docs.stripe.com/payment-links`.
- Stripe's current U.S. standard card pricing is `2.9% + 30¢` per successful domestic card transaction, with no setup or monthly fees listed for standard pricing: `https://stripe.com/pricing`.
- Stripe docs compare Payment Links and invoices: Payment Links are reusable and fit "anyone with the link"; invoices are better for a specific customer. NPM Trust Pulse needs a reusable checkout for a fixed `$49` product, so Payment Links are the simpler fit.

## Options Considered

1. Keep the current email-first request flow.
   - Lowest risk, but it preserves the manual bottleneck and delays payment until after a human/operator response.

2. Create an invoice after each request.
   - Better for one named customer, but still manual and slower. It does not solve the no-touch checkout problem.

3. Create a Stripe Payment Link for a fixed `$49` NPM Trust Pulse report.
   - Best fit. It keeps the product simple, requires no code integration, and can be added to the request/offer pages after approval.

## Recommendation

Create one live Stripe Payment Link for:

- Product: `NPM Trust Pulse report`
- Price: `$49.00`
- Type: one-time payment
- Quantity: fixed at `1`
- Description: `One public-surface trust report for one npm package. Uses public npm/GitHub metadata only; no source-code security review.`
- Customer data: collect email.
- Optional field if available in Dashboard: npm package name.
- Post-payment behavior: redirect to a simple thank-you/instructions page or Stripe-hosted confirmation until a thank-you page is created.

At standard U.S. domestic-card pricing, a `$49.00` payment would cost about `$1.72` in Stripe processing fees, leaving about `$47.28` before any tax, international-card, dispute, refund, or account-specific fees.

## Exact Approval Needed

`APPROVED: CREATE NPM TRUST PULSE STRIPE PAYMENT LINK, $49`

## After Approval

1. Create the live Stripe Product, Price, and Payment Link using the existing Stripe account and approved credentials.
2. Record the Payment Link ID and URL in `workspace/npm-trust-pulse/README.md`.
3. Add the checkout URL to the live offer and request page CTAs.
4. Add a lightweight post-payment instruction page if Stripe requires a redirect target.
5. Deploy, verify the live checkout URL returns HTTP 200, and confirm no private outreach/prospect files are exposed.

## Boundaries

No Stripe object was created in this run. No checkout URL was added, no public page was changed, no outreach was sent, no account was created, no DNS changed, and no money was spent. Current budget balance remains `$35.93`.
