# Shopify Review Pulse Owner-Gate Hard Stop

Date: 2026-05-14 10:18 UTC

## Outcome

Stopped on the current owner gate instead of building more Review Pulse collateral.

The lane has enough assets for the first real signal. The next revenue-moving action is still the one-recipient SellerPic send, and it cannot be done from this run without either Google mailbox access or explicit approval to use an owner-accessible mailbox.

## Current Best Approval Line

`APPROVED: SEND SELLERPIC TEST FROM ACCESSIBLE OWNER MAILBOX`

Why this line first: it avoids waiting indefinitely on Google's sign-in challenge, uses the already-approved one-recipient test, costs `$0`, and creates the first willingness-to-pay signal faster than more prospect reports, more previews, a founder post, or payment setup.

## Evidence Checked

- Public offer is live: `https://shopify-review-pulse-eta.vercel.app/offer.html` returned HTTP `200`.
- SellerPic locked preview is live and noindexed: `https://shopify-review-pulse-eta.vercel.app/sellerpic-teardown.html` returned HTTP `200` with `x-robots-tag: noindex, nofollow`.
- `theshepherdstack.com` MX still points to Google: `1 smtp.google.com.`
- SMTP from this host still cannot be used as a send path: `smtp.gmail.com:587` and `smtp.gmail.com:465` both timed out.
- Google's current help material confirms phone/text challenges can be required during account sign-in and must be completed with a phone-capable path.
- Tally remains a viable free intake fallback because its current docs advertise unlimited forms and submissions on the free plan, but creating that form is already gated.
- Shopify's current app-review docs continue to support the lane premise: merchant reviews affect install trust and positive reviews can influence Shopify App Store search/category placement.

## Options Considered

1. **Send SellerPic from an owner-accessible mailbox after approval.**
   - Best move.
   - Cost: `$0`.
   - Uses existing packet: `workspace/shopify-review-pulse/outreach/sellerpic-send-control.md`.
   - Creates direct market signal now.

2. **Wait for branded Google Workspace sign-in verification.**
   - Still valid, but slower.
   - Google sign-in verification remains owner-side.
   - SMTP is still not a working path from this host, so Gmail web UI may still be required after verification.

3. **Create the free Tally intake form.**
   - Useful because public CTAs currently point to the inaccessible `reviewpulse@theshepherdstack.com` mailbox.
   - Still requires account/form creation approval.
   - Less immediate than the SellerPic send because there is no active public traffic motion yet.

4. **Build more reports or send kits.**
   - Rejected.
   - SellerPic, A2Reviews, Kaching, and MAG now have enough private fulfillment depth for the validation sequence.
   - More collateral does not create willingness-to-pay evidence.

## Exact Next Action After Approval

If Travis replies with `APPROVED: SEND SELLERPIC TEST FROM ACCESSIBLE OWNER MAILBOX`:

1. Open `workspace/shopify-review-pulse/outreach/sellerpic-send-control.md`.
2. Send exactly one email to `support@sellerpic.ai` from the accessible owner mailbox.
3. Record sender and UTC timestamp in the send-control packet.
4. Wait 72 hours.
5. Use A2Reviews only if SellerPic does not reply.

## Boundaries

No outreach was sent. No public page was changed. No checkout or payment infrastructure was created. No account was created. No DNS change was made. No public post was published. No money was spent.

## Sources

- Google Account Help, phone/text verification: https://support.google.com/accounts/answer/114129
- Google Workspace Admin Help, sign-in issues: https://support.google.com/a/answer/6335621
- Tally free plan/features: https://tally.so/help/tally-a-free-typeform-alternative and https://tally.so/help/features
- Shopify app-review guidance: https://shopify.dev/docs/apps/launch/marketing/manage-app-reviews
