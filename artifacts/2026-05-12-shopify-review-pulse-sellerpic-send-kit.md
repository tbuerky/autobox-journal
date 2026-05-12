# Shopify Review Pulse SellerPic send kit

Date: 2026-05-12

## Task

Actual outreach is still blocked on `CREATE/CONNECT MAILBOX: reviewpulse@theshepherdstack.com FOR SHOPIFY REVIEW PULSE OUTBOUND`.

This run reduced the next owner step to one mailbox action plus one one-recipient email send. No email was sent and no new credential was used.

## Live checks

- SellerPic Shopify review page is still live: `https://apps.shopify.com/sellerpic/reviews`
- Opened Shopify page showed 4.5/5 across 102 reviews, with visible low-star pricing/billing and support complaints still supporting the first-send hook.
- Public landing is live: `https://shopify-review-pulse.vercel.app/offer.html` returned HTTP 200.
- Locked SellerPic preview is live: `https://shopify-review-pulse.vercel.app/sellerpic-teardown.html` returned HTTP 200 with `X-Robots-Tag: noindex, nofollow`.

## Built

- Ready-to-import email file: `workspace/shopify-review-pulse/outreach/sellerpic-first-email.eml`
- Existing Markdown draft remains canonical for editing: `workspace/shopify-review-pulse/outreach/sellerpic-first-email.md`

## Send procedure after mailbox clears

1. Create or connect `reviewpulse@theshepherdstack.com`.
2. Send exactly one email to `support@sellerpic.ai`.
3. Use subject: `Locked public-review report preview for SellerPic`.
4. Use the body in `workspace/shopify-review-pulse/outreach/sellerpic-first-email.md` or import `workspace/shopify-review-pulse/outreach/sellerpic-first-email.eml`.
5. Record the send timestamp in `config/HANDOFF.md`.
6. Wait 72 hours.
7. If no reply, use A2Reviews as the second target. Do not batch-send.

## Approval line

`CREATE/CONNECT MAILBOX: reviewpulse@theshepherdstack.com FOR SHOPIFY REVIEW PULSE OUTBOUND`

## Discord-ready update

Did: converted the SellerPic first-send into a ready `.eml` file and rechecked the live target/preview pages.
See: `workspace/shopify-review-pulse/outreach/sellerpic-first-email.eml` and `artifacts/2026-05-12-shopify-review-pulse-sellerpic-send-kit.md`
Next: create/connect `reviewpulse@theshepherdstack.com`, then send one SellerPic email and wait 72h.
Blocked on you: `CREATE/CONNECT MAILBOX: reviewpulse@theshepherdstack.com FOR SHOPIFY REVIEW PULSE OUTBOUND`

## Cash

$162.45 unchanged. No spend.
