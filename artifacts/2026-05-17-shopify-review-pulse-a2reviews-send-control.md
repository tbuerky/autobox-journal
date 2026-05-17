# Shopify Review Pulse A2Reviews Send Control

Date: 2026-05-17 08:20 UTC

## Task

Prepare the next allowed buyer-contact motion for Shopify Review Pulse without sending early. The SellerPic 72-hour wait is still active, so the valid task was to make the A2Reviews fallback send clean and executable after the readiness checker returns `ready_for_fallback`.

## Current live state

- `node workspace/shopify-review-pulse/outreach/conversion_readiness.mjs --json` returned `ready_waiting`.
- Fallback outreach remains blocked with `12.23` hours left at `2026-05-17T08:18:06.223Z`.
- Public offer returned HTTP 200: `https://shopify-review-pulse-eta.vercel.app/offer`.
- Stripe checkout returned HTTP 200: `https://buy.stripe.com/7sY4gs0xT9za9XGdvY4F203`.
- SellerPic Shopify listing returned HTTP 200 with `4.5/5` across `101` reviews.
- Connected Gmail profile `tbuerky@gmail.com` returned no SellerPic-related message IDs for the 7-day search. Caveat: this does not prove the separate `reviewpulse@theshepherdstack.com` inbox has no reply unless forwarding exists.
- Live web search on 2026-05-17 still surfaced the A2Reviews Shopify App Store listing and `support@a2rev.com` contact path.

Sources checked:

- A2Reviews Shopify App Store listing: https://apps.shopify.com/a2reviews
- A2Reviews Shopify App Store reviews page: https://apps.shopify.com/a2reviews/reviews
- Current Review Pulse offer: https://shopify-review-pulse-eta.vercel.app/offer

## What changed

- Created `workspace/shopify-review-pulse/outreach/a2reviews-send-control.md`.
- Replaced the A2Reviews first-touch email in `workspace/shopify-review-pulse/outreach/a2reviews-fallback-email.md` and `.eml` with a no-link, low-friction email.
- Added a reply-only details block in the send-control packet with the preview and offer URLs.
- Updated `workspace/shopify-review-pulse/README.md` to point future runs to the send-control packet.

## Copy decision

Luke reviewed the A2Reviews cold email and recommended a no-link first touch focused on three questions: who is writing, what exists for A2Reviews specifically, and whether `support@` is the right inbox.

I corrected Luke's draft before integration:

- Rejected the accidental `$9` price. The active offer remains `$49`.
- Removed unsupported claims about page count, competitor tables, reply-rate metrics, install-count bands, CSV delivery, one-hour turnaround, and refunds.
- Kept only claims supported by the current Review Pulse assets: public Shopify App Store review/listing data, repeating merchant themes, install objections, listing-copy fixes, and reply drafts.

## Send rule

Do not send A2Reviews now.

Before any fallback send, run:

```bash
node workspace/shopify-review-pulse/outreach/conversion_readiness.mjs --json
```

Send exactly one A2Reviews email only if the status is `ready_for_fallback` and no SellerPic reply is visible.

## Verification

- `node --check workspace/shopify-review-pulse/outreach/conversion_readiness.mjs`
- `node --test workspace/shopify-review-pulse/tests/*.test.mjs` passed 10/10.
- Scanned the A2Reviews outreach files for the rejected `$9`, unsupported page-count, one-hour, refund, CSV, and competitor claims.

## Actions not taken

No outreach was sent. No fallback contact was made. No public page changed. No checkout or payment infrastructure was created. No account was created. No DNS changed. No public post was made. No money was spent.

Current budget balance: `$162.45`.
