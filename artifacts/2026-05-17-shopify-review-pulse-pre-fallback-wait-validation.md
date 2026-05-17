# Shopify Review Pulse pre-fallback wait validation - 2026-05-17

## Decision

Do not contact A2Reviews yet.

The SellerPic 72-hour wait is still active. At `2026-05-17T06:17:47.842Z`, the readiness checker returned `ready_waiting` with `14.24` hours remaining before fallback outreach is allowed. The approved fallback window opens at approximately `2026-05-17 20:32 UTC` unless SellerPic replies first or Travis gives fresh explicit instruction.

## Evidence

- Connected Gmail profile: `tbuerky@gmail.com`.
- Gmail search for SellerPic, `support@sellerpic.ai`, `reviewpulse@theshepherdstack.com`, and `SellerPic review notes` across the last 14 days returned no message IDs.
- This Gmail check does not prove the separate `reviewpulse@theshepherdstack.com` inbox has no reply unless forwarding exists.
- `node workspace/shopify-review-pulse/outreach/conversion_readiness.mjs --json` returned `ready_waiting`.
- Public offer: HTTP 200 at `https://shopify-review-pulse-eta.vercel.app/offer`.
- Public offer still includes the live Stripe checkout URL.
- Stripe checkout: HTTP 200 at `https://buy.stripe.com/7sY4gs0xT9za9XGdvY4F203`.
- SellerPic Shopify listing: HTTP 200; live parser reports `4.5/5` across `101` reviews.
- Shopify's live SellerPic page shows `Reviews (101)`, `Overall rating`, `4.5`, and `7` one-star reviews.
- Stripe's current Payment Links documentation still supports the low-touch checkout path: Payment Links are Stripe-hosted pages that can be shared by email or on a website with complexity `1/5`.

## Verification

```bash
node --test workspace/shopify-review-pulse/tests/*.test.mjs
```

Result: 10/10 tests passed.

## Sources

- SellerPic Shopify App Store listing: `https://apps.shopify.com/sellerpic`
- Stripe Payment Links docs: `https://docs.stripe.com/payment-links`
- Public Review Pulse offer: `https://shopify-review-pulse-eta.vercel.app/offer`

## Next action

At or after `2026-05-17 20:32 UTC`, rerun:

```bash
node workspace/shopify-review-pulse/outreach/conversion_readiness.mjs --json
```

If it returns `ready_for_fallback` and no SellerPic reply is visible, A2Reviews is the next target using `workspace/shopify-review-pulse/outreach/a2reviews-fallback-email.eml`. If SellerPic replies first, use `workspace/shopify-review-pulse/fulfillment/reply-and-close-kit.md`; if they pay, deliver `workspace/shopify-review-pulse/fulfillment/sellerpic-delivery-2026-05-15/`.

## Non-actions

No outreach, fallback contact, public page change, checkout/payment infrastructure creation, account creation, DNS change, public post, or spend.
