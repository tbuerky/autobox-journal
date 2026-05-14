# Shopify Review Pulse Gate-Deadlock Escalation

Date: 2026-05-14 12:18 UTC

## Outcome

Stopped on the same owner-side revenue gate and tightened the next-run policy: do not build more Shopify Review Pulse collateral by default while the first SellerPic send is blocked.

The current lane has enough proof, first-send copy, fallback targets, and private fulfillment material to test willingness to pay. The bottleneck is not another report draft. It is getting exactly one message to SellerPic from a mailbox Travis can access.

## Current Best Approval Line

`APPROVED: SEND SELLERPIC TEST FROM ACCESSIBLE OWNER MAILBOX`

Why this stays first:

- It costs `$0`.
- It avoids waiting on Google's sign-in challenge.
- It uses the existing one-recipient send packet at `workspace/shopify-review-pulse/outreach/sellerpic-send-control.md`.
- It creates the first real willingness-to-pay signal faster than a founder post, payment-link setup, Tally intake form, or more prospect prep.

## Fresh Evidence

- Public offer is live: `https://shopify-review-pulse-eta.vercel.app/offer.html` returned HTTP `200`.
- SellerPic locked preview is live and noindexed: `https://shopify-review-pulse-eta.vercel.app/sellerpic-teardown.html` returned HTTP `200` with `x-robots-tag: noindex, nofollow`.
- `theshepherdstack.com` MX still points to Google: `1 smtp.google.com.`
- SMTP from this host still cannot be used: `smtp.gmail.com:587` and `smtp.gmail.com:465` both failed or timed out.
- Public request CTAs still point at `mailto:reviewpulse@theshepherdstack.com`, which remains commercially risky until the mailbox can receive replies or the Tally gate clears.
- The SellerPic send files still point to the current `shopify-review-pulse-eta.vercel.app` links and `support@sellerpic.ai`.

## Live Market / Tool Validation

- Shopify's current app-review docs still support the commercial premise: reviews influence merchant install trust and positive reviews can improve Shopify App Store search/category placement.
- Shopify's same guidance reinforces the compliance boundary: review manipulation and incentive-based review requests are prohibited. Review Pulse should stay positioned as analysis, reply drafting, and listing improvement, not review solicitation.
- Tally still advertises a free plan with unlimited forms and responses, so the Tally intake gate remains a good no-spend fallback if Travis wants inbound requests before the branded mailbox works.
- Google's account help still supports that phone/text verification can be required during sign-in, so this is plausibly an owner-side access challenge rather than a code problem.

## Decision

No new gate was added. The existing first gate remains the correct one.

Future autonomous runs should not create more Review Pulse target reports, previews, send kits, or fulfillment drafts unless one of these happens:

1. Travis clears a send/intake/payment/post gate.
2. A live state check shows a hard change, such as mailbox access working, a new inbound request, a reply, or a broken public asset.
3. Travis gives a fresh owner instruction that changes the priority.

If none of those happen, the honest output is the same blocker: `APPROVED: SEND SELLERPIC TEST FROM ACCESSIBLE OWNER MAILBOX`.

## Exact Next Action After Approval

1. Open `workspace/shopify-review-pulse/outreach/sellerpic-send-control.md`.
2. Send exactly one email to `support@sellerpic.ai` from the approved accessible mailbox.
3. Record sender and UTC timestamp in the send-control packet.
4. Wait 72 hours.
5. Use A2Reviews only if SellerPic does not reply.

## Boundaries

No outreach was sent. No public page was changed. No checkout or payment infrastructure was created. No account was created. No DNS change was made. No public post was published. No money was spent.

## Sources

- Shopify app-review guidance: https://shopify.dev/docs/apps/launch/marketing/manage-app-reviews
- Tally free plan/features: https://tally.so/help/tally-a-free-typeform-alternative
- Google account verification help: https://support.google.com/accounts/answer/114129
