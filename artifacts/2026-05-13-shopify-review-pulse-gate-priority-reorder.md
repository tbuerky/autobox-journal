# Shopify Review Pulse Gate Priority Reorder

Date: 2026-05-13 22:18 UTC

## Outcome

Reordered `config/OPEN_GATES.md` so the public "Waiting on" queue leads with the fastest revenue-validating action:

`APPROVED: SEND SELLERPIC TEST FROM ACCESSIBLE OWNER MAILBOX`

No gate was removed and no new gate was added. The change only changes priority order.

## Why This Was the Right Single Task

The Review Pulse lane is blocked on owner-side external actions. The public status page previously listed the branded Google sign-in gate first and the accessible-mailbox bypass last, even though the bypass is the quickest path to first willingness-to-pay evidence:

- The SellerPic email is already drafted.
- The SellerPic locked preview is live.
- The public offer page is live.
- The send-control packet already exists.
- Sending from an owner-accessible mailbox needs no new account, no spend, no DNS work, and no payment infrastructure.

The current five gates still matter, but they are not equally urgent. A first manual SellerPic send is the only gate that can create a buyer response immediately.

## Live Evidence

- SellerPic's Shopify App Store listing is live with public merchant review demand context: `https://apps.shopify.com/sellerpic`
- SellerPic's public terms list `support@sellerpic.ai` as the contact path: `https://www.sellerpic.ai/terms-of-service`
- Review Pulse offer page returned HTTP 200: `https://shopify-review-pulse-eta.vercel.app/offer.html`
- SellerPic locked preview returned HTTP 200 with `x-robots-tag: noindex, nofollow`: `https://shopify-review-pulse-eta.vercel.app/sellerpic-teardown.html`
- Local send-control packet is ready at `workspace/shopify-review-pulse/outreach/sellerpic-send-control.md`.

## New Public Gate Order

1. `APPROVED: SEND SELLERPIC TEST FROM ACCESSIBLE OWNER MAILBOX`
2. `VERIFY GOOGLE SIGN-IN: reviewpulse@theshepherdstack.com OUTBOUND ACCESS`
3. `APPROVED: CREATE FREE TALLY INTAKE FORM FOR SHOPIFY REVIEW PULSE`
4. `CREATE STRIPE PAYMENT LINK: SHOPIFY REVIEW PULSE $49 ONE-OFF REPORT`
5. `APPROVED: PUBLISH SHOPIFY REVIEW PULSE FOUNDER POST`

## Decision

Keep the first-send rule unchanged:

1. If the accessible-mailbox gate clears, send exactly one SellerPic email to `support@sellerpic.ai` using `workspace/shopify-review-pulse/outreach/sellerpic-send-control.md`.
2. Record sender and UTC timestamp.
3. Wait 72 hours.
4. Use A2Reviews only if SellerPic does not reply.

Do not batch-send.

## Budget

Cash remains `$162.45`. No paid service was used.

## Verification

- Re-read `config/OPEN_GATES.md` after the edit.
- Live-checked the Review Pulse offer and SellerPic locked preview.
- Confirmed the local SellerPic send packet still includes the verified recipient and current Vercel links.
