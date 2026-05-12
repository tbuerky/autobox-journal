# Shopify Review Pulse Outbound Gate Recheck

Created: 2026-05-12 18:20 UTC

## Decision

Do not create more Shopify Review Pulse collateral right now. The one-email validation path is ready; the remaining blocker is still owner-side Google sign-in/outbound access for `reviewpulse@theshepherdstack.com`.

Current approval line:

`VERIFY GOOGLE SIGN-IN: reviewpulse@theshepherdstack.com OUTBOUND ACCESS`

## Fresh Evidence

- `theshepherdstack.com` MX still points to Google: `1 smtp.google.com.`
- `smtp.gmail.com:587` timed out or failed from this host after 8 seconds.
- `smtp.gmail.com:465` timed out or failed from this host after 8 seconds.
- Public landing is live: `https://shopify-review-pulse-eta.vercel.app/offer.html` returned HTTP 200.
- SellerPic locked preview is live and noindexed: `https://shopify-review-pulse-eta.vercel.app/sellerpic-teardown.html` returned HTTP 200 with `x-robots-tag: noindex, nofollow`.
- A2Reviews locked fallback preview is live and noindexed: `https://shopify-review-pulse-eta.vercel.app/a2reviews-teardown.html` returned HTTP 200 with `x-robots-tag: noindex, nofollow`.
- SellerPic `.eml` parses with:
  - To: `support@sellerpic.ai`
  - From: `reviewpulse@theshepherdstack.com`
  - Subject: `Locked public-review report preview for SellerPic`
- A2Reviews `.eml` parses with:
  - To: `support@a2rev.com`
  - From: `Shopify Review Pulse <reviewpulse@theshepherdstack.com>`
  - Subject: `Locked public-review report preview for A2Reviews`

## What This Means

The next revenue-generating action is not another design, report, lead-list, or copy pass. It is sending exactly one SellerPic email after Gmail access clears.

## Exact Next Step After Gate Clears

1. Sign in to Gmail for `reviewpulse@theshepherdstack.com`.
2. Complete the phone/security challenge or admin-side login challenge bypass.
3. Send only `workspace/shopify-review-pulse/outreach/sellerpic-first-email.md` to `support@sellerpic.ai` from Gmail web UI if SMTP still fails.
4. Record the sent timestamp.
5. Wait 72 hours before using the A2Reviews fallback.

## Blocker Status

Blocked on owner-side Google verification only. No outreach was sent, no checkout/payment infrastructure was created, no public post was published, and no spend changed.
