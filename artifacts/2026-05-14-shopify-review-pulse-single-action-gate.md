# Shopify Review Pulse Single-Action Gate

Date: 2026-05-14 14:18 UTC

## Decision

Do not build more Shopify Review Pulse collateral by default. The highest-leverage revenue move is still the one-recipient SellerPic willingness-to-pay email.

Use this approval line:

`APPROVED: SEND SELLERPIC TEST FROM ACCESSIBLE OWNER MAILBOX`

## Why This Is Still The Right Move

The buyer target remains credible. Live Shopify App Store review data for SellerPic still shows 102 public reviews, 4.5 overall rating, 7 one-star reviews, and recent visible complaints about pricing, billing, credits, and support follow-up. That is enough pain to justify testing the $49 report offer with one direct email.

The sales assets are already ready. The public offer page is live, the SellerPic locked preview is live and noindexed, the importable email and copy-paste send packet already exist, and the private fulfillment files already cover a paid report.

The blocker is not research, copy, lead quality, or fulfillment. It is permission to send from a mailbox that can receive replies.

## Live Evidence

- Public offer: `https://shopify-review-pulse-eta.vercel.app/offer.html` returned HTTP 200.
- SellerPic locked preview: `https://shopify-review-pulse-eta.vercel.app/sellerpic-teardown.html` returned HTTP 200 and `x-robots-tag: noindex, nofollow`.
- SellerPic App Store review page: `https://apps.shopify.com/sellerpic/reviews` showed 102 reviews, 4.5 average, 7 one-star reviews, and visible pricing/support complaints.
- Domain mail routing: `theshepherdstack.com` MX still resolves to `1 smtp.google.com.`.
- Direct SMTP from this host still failed on `smtp.gmail.com:587` and `smtp.gmail.com:465`.
- Current executable send packet: `workspace/shopify-review-pulse/outreach/sellerpic-send-control.md`.

## Options Considered

- **Send from branded Review Pulse mailbox:** best brand fit, but still blocked by Google sign-in verification and host SMTP failures.
- **Create Tally intake:** useful later, but it does not test willingness to pay by itself and still needs owner approval/account work.
- **Create Stripe Payment Link:** useful after interest, but a checkout link without first-send traffic does not create demand.
- **Publish founder post:** possible traffic motion, but replies may still route into the blocked Review Pulse mailbox unless Travis agrees to collect them manually.
- **Build more reports or pages:** lower leverage now. The first target, fallback target, fulfillment kit, and reply kit already exist.

## Next Action After Approval

1. Send exactly one email to `support@sellerpic.ai` using `workspace/shopify-review-pulse/outreach/sellerpic-send-control.md`.
2. Record the sender, UTC timestamp, and message id if available.
3. Wait 72 hours before contacting A2Reviews.
4. If SellerPic replies positively before the Stripe link exists, use `workspace/shopify-review-pulse/fulfillment/reply-and-close-kit.md` and restate the existing Stripe Payment Link gate.

## Guardrails

- No email was sent.
- No public page was changed.
- No checkout or payment infrastructure was created.
- No account was created.
- No DNS was changed.
- No public post was published.
- No spend occurred.
