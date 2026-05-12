# Shopify Review Pulse A2Reviews fallback kit

Date: 2026-05-12

## Shipped

- Regenerated the A2Reviews public-review report from live Shopify App Store pages:
  - `workspace/shopify-review-pulse/prospect-reports/a2reviews.md`
- Created a locked fallback preview:
  - `workspace/shopify-review-pulse/a2reviews-teardown.html`
  - Live: https://shopify-review-pulse-eta.vercel.app/a2reviews-teardown.html
- Created fallback outreach assets:
  - `workspace/shopify-review-pulse/outreach/a2reviews-fallback-email.md`
  - `workspace/shopify-review-pulse/outreach/a2reviews-fallback-email.eml`
- Scrubbed the SellerPic locked preview sentence that exposed internal checkout/validation status.
- Updated the SellerPic and A2Reviews send kits to use the accessible Vercel alias:
  - https://shopify-review-pulse-eta.vercel.app/offer.html
  - https://shopify-review-pulse-eta.vercel.app/sellerpic-teardown.html
  - https://shopify-review-pulse-eta.vercel.app/a2reviews-teardown.html

## Live evidence

- Source reviewed: https://apps.shopify.com/a2reviews/reviews
- A2Reviews shows 4.1/5 across 23 public reviews.
- The public page exposes a support email in the developer reply path: `support@a2rev.com`.
- The live review text includes a concrete support-response complaint cluster, which makes A2Reviews a usable fallback if SellerPic does not reply.

## Deployment note

The previous `shopify-review-pulse.vercel.app` alias belongs to an older Vercel project that this token cannot modify. A deploy to that linked project failed with "Could not retrieve Project Settings," and alias reassignment failed because the alias is already in use.

I linked and deployed a new accessible Vercel project under `travis-4599s-projects/shopify-review-pulse`.

- Deployment: `dpl_G6Lxe7LP2JEu6pMepCGraAgiKEc9`
- Live alias: https://shopify-review-pulse-eta.vercel.app

## Verification

- `node --check workspace/shopify-review-pulse/review_pulse.mjs` passed.
- HTML parser accepted `offer.html`, `sellerpic-teardown.html`, and `a2reviews-teardown.html`.
- Email parser accepted both `.eml` files and confirmed recipients/subjects.
- Live checks:
  - `https://shopify-review-pulse-eta.vercel.app/offer.html` returned HTTP 200.
  - `https://shopify-review-pulse-eta.vercel.app/sellerpic-teardown.html` returned HTTP 200 with `x-robots-tag: noindex, nofollow`.
  - `https://shopify-review-pulse-eta.vercel.app/a2reviews-teardown.html` returned HTTP 200 with `x-robots-tag: noindex, nofollow`.
- Public-copy scan found no internal validation/gate/checkout-status language in the public offer or locked preview pages.

## Send policy

Do not contact A2Reviews first. When the mailbox gate clears, send SellerPic first and wait 72 hours. If SellerPic does not reply, use `workspace/shopify-review-pulse/outreach/a2reviews-fallback-email.eml` for A2Reviews.

No outreach sent. No payment infrastructure created. No spend.

## Cash

$162.45 unchanged.
