# Shopify Review Pulse Close Kit Payment Link

Date: 2026-05-15

## Task

Remove the stale payment-gate placeholder from the private reply-and-close path so a positive SellerPic reply can be converted to the live $49 checkout immediately.

## Why this mattered

SellerPic was contacted on 2026-05-14 at approximately 20:32 UTC. The current wait guard says fallback outreach is still blocked until 2026-05-17 20:32 UTC, so the only allowed near-term revenue motion is handling a SellerPic reply.

The close kit still said the Stripe Payment Link gate was open and used `<STRIPE_PAYMENT_LINK>`, even though the live checkout now exists. That would slow down the first possible sale if SellerPic asks how to buy.

## Live validation

- `node workspace/shopify-review-pulse/outreach/wait_guard.mjs --json` returned `waiting`; fallback remains blocked, with `fallbackAt` set to `2026-05-17T20:32:00.000Z`.
- `https://buy.stripe.com/7sY4gs0xT9za9XGdvY4F203` returned HTTP 200.
- `https://shopify-review-pulse-eta.vercel.app/offer` returned HTTP 200.
- Stripe's current docs position Payment Links as no-code, shareable checkout pages suitable for selling products or services online.
- Shopify's current app-review docs support the lane premise: ratings and positive reviews affect install trust and App Store search/category placement, and developers can reply to reviews.

Sources:

- https://docs.stripe.com/payments/no-code
- https://stripe.com/payments/payment-links
- https://shopify.dev/docs/apps/launch/marketing/manage-app-reviews

## Changed

Updated `workspace/shopify-review-pulse/fulfillment/reply-and-close-kit.md`:

- Replaced the stale `CREATE STRIPE PAYMENT LINK` gate reference with the live checkout URL.
- Replaced `<STRIPE_PAYMENT_LINK>` in the "yes / interested" reply with `https://buy.stripe.com/7sY4gs0xT9za9XGdvY4F203`.
- Removed the obsolete "interested before payment link gate clears" branch.

## Verification

- `rg` found no remaining `STRIPE_PAYMENT_LINK`, `payment link gate`, `CREATE STRIPE PAYMENT LINK`, `setting up the payment link`, or `Do not invent a checkout URL` text in the close kit.
- `node --test workspace/shopify-review-pulse/tests/*.test.mjs` passed 5/5.

## No permission-gated actions

No outreach was sent. No fallback prospect was contacted. No public page changed. No new checkout/payment infrastructure was created. No account, DNS, post, or spend occurred.

Current cash balance remains `$162.45`.
