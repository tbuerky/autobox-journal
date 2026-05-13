# Shopify Review Pulse Outbound Fallback Audit

Created: 2026-05-13

## Task

Check whether a free or low-cost email provider should replace the stalled Google Workspace mailbox path for the first Shopify Review Pulse willingness-to-pay email.

No email was sent, no account was created, no DNS was changed, no payment infrastructure was created, and no money was spent.

## Recommendation

Do not switch providers yet. Keep the first-send path on the existing Google Workspace mailbox.

Approval line already open:

`VERIFY GOOGLE SIGN-IN: reviewpulse@theshepherdstack.com OUTBOUND ACCESS`

## Why

The problem is not only sending. The first revenue test needs a credible reply path for SellerPic. A send-only provider can push the email out, but if replies still land at an inaccessible `reviewpulse@theshepherdstack.com` inbox, the test can create demand that AutoBox cannot receive or fulfill.

The lowest-friction path is still:

1. Travis completes or bypasses the Google security challenge for `reviewpulse@theshepherdstack.com`.
2. Send exactly one SellerPic email from Gmail web UI using `workspace/shopify-review-pulse/outreach/sellerpic-first-email.md` or `.eml`.
3. Record the sent timestamp.
4. Wait 72 hours before A2Reviews.

## Provider Findings

| Provider | Current useful fact | Cost signal | Why it does not beat Google now |
|---|---:|---:|---|
| Resend | Free accounts allow 100 transactional emails/day and 3,000/month; verified domain then permits sending from any address at that domain. | $0 free tier | Requires account, domain verification, API key, and reply handling. Sending is not the only blocker. |
| Postmark | Free Developer tier includes 100 emails/month and does not expire. | $0 developer tier | Strong deliverability, but still requires account/domain setup and is shaped for transactional streams, not the first manual sales reply loop. |
| Brevo | Free plan includes 300 daily email sends, 1 user, transactional email, and custom templates. | $0 free tier | Still requires sender/domain authentication for a professional sender and does not solve the inaccessible reply inbox. |

## Sources

- Resend account quotas: https://resend.com/docs/knowledge-base/account-quotas-and-limits
- Resend sender/domain behavior: https://resend.com/docs/knowledge-base/how-do-I-create-an-email-address-or-sender-in-resend
- Postmark pricing/free Developer tier: https://postmarkapp.com/pricing/
- Brevo free plan: https://help.brevo.com/hc/en-us/articles/208589409-About-Brevo-s-pricing-plans
- Brevo transactional email options: https://help.brevo.com/hc/en-us/articles/7924148470546-How-can-I-send-transactional-emails-with-Brevo
- Brevo sender/domain authentication guidance: https://help.brevo.com/hc/en/articles/208836149-

## If Google Remains Blocked

Only after Travis decides the Workspace mailbox cannot be recovered should AutoBox open a new outbound-provider gate. The least bad fallback would be Resend because it is developer-oriented, has a usable free quota, and permits any sender at a verified domain after domain verification.

That fallback would still require a new owner approval and setup sequence:

1. Approve a Resend free account for Shopify Review Pulse.
2. Add/verify `theshepherdstack.com` or a sending subdomain in Resend.
3. Provide an API key through a private channel.
4. Configure a reply-capture path before sending SellerPic.

Do not do this while the Google sign-in challenge is the smaller blocker.

## Current Blocker

Blocked on owner-side Google verification only. The current open gates remain correct:

- `VERIFY GOOGLE SIGN-IN: reviewpulse@theshepherdstack.com OUTBOUND ACCESS`
- `CREATE STRIPE PAYMENT LINK: SHOPIFY REVIEW PULSE $49 ONE-OFF REPORT`
- `APPROVED: PUBLISH SHOPIFY REVIEW PULSE FOUNDER POST`

Cash balance: $162.45. Spend: $0.
