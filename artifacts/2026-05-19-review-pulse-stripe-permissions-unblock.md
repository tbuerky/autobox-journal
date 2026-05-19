# Review Pulse Stripe Permissions Unblock

Run: 2026-05-19 22:19 UTC

## Task

Turn the stale Review Pulse payment-link approval gates into the real executable blocker after the 2026-05-19 interactive gate-clearance session.

## Why This Matters Now

A2Reviews, SEOPress, and Strawberry have all been contacted from `reviewpulse@theshepherdstack.com`. If any prospect replies with purchase intent, Shopify Review Pulse already has a live `$49` checkout link, but WordPress Review Pulse and Extension Review Pulse still cannot collect payment.

The owner approval to create both `$49` links is already present. The blocker is not product approval anymore; it is Stripe write permission.

## Evidence

- Local Stripe CLI profile is authenticated to live account `acct_1TLwhK4BEFFaauKW` as The Shepherd Stack with a live restricted key.
- `stripe products list --live --limit 3` succeeds and shows existing live products, including `prod_UW9LUfuXiHK7es` for Shopify Review Pulse.
- `stripe prices list --live --limit 3` succeeds and shows `price_1TX72S4BEFFaauKWLdwRN7yv`, a live one-time `$49.00` Shopify Review Pulse price.
- `stripe payment_links list --live --limit 3` succeeds and shows live Shopify Review Pulse Payment Link `plink_1TX72a4BEFFaauKWQRhF47Ju` with checkout URL `https://buy.stripe.com/7sY4gs0xT9za9XGdvY4F203`.
- The latest handoff records that `stripe products create --live` and `stripe prices create --live` failed with `The provided key ... does not have the required permissions for this endpoint`.

Stripe documentation confirms this object chain: Payment Links use Products and Prices, then create a hosted payment page from line items. Stripe CLI docs also confirm CLI authentication uses restricted API keys and that restricted-key permissions can be viewed or replaced in the Dashboard.

Sources:

- https://docs.stripe.com/payment-links/create
- https://docs.stripe.com/stripe-cli/keys

## Gate Reconciled

Removed stale approval gates:

- `APPROVED: CREATE WORDPRESS REVIEW PULSE $49 STRIPE PAYMENT LINK`
- `APPROVED: CREATE EXTENSION REVIEW PULSE $49 STRIPE PAYMENT LINK`

Added the true blocker:

`STRIPE PERMISSIONS: REVIEW PULSE PRODUCT/PRICE/PAYMENT LINK WRITE ACCESS`

## Exact Permission Needed

Provide either:

1. A live Stripe restricted key with write access for Products, Prices, and Payment Links, plus read access for those same resources; or
2. A refreshed Stripe CLI login/session whose live restricted key has those write permissions.

Recommended restricted-key scope:

- Products: read/write
- Prices: read/write
- Payment Links: read/write
- Checkout Sessions: read-only is acceptable if available for verification, but not required for creating these links

Do not provide a full unrestricted secret key unless there is no practical restricted-key option.

## Immediately After Permission Clears

1. Create `WordPress Review Pulse - one plugin report` at `$49.00` one-time.
2. Create `Extension Review Pulse - one extension report` at `$49.00` one-time.
3. Create one Payment Link for each product with quantity fixed to 1.
4. Record product, price, Payment Link, and checkout URL IDs in the appropriate private READMEs/fulfillment scripts.
5. Do not add public buy buttons unless Travis separately approves public checkout CTAs.

## Changes Made This Run

- Updated `config/OPEN_GATES.md` to show the true Stripe-permissions gate.
- Updated `workspace/wordpress-review-pulse/README.md` to reflect the SEOPress send and the payment blocker.
- Updated `workspace/extension-review-pulse/README.md` to reflect the Strawberry send and the payment blocker.
- Updated `config/TODO.md`, `config/STATE.md`, and `config/ACTIVE_BETS.md`.

## Boundary

No Stripe product, price, Payment Link, checkout URL, public CTA, outreach, account setting, DNS change, public post, deploy, or spend happened in this run.

Current cash balance: `$57.18`.
