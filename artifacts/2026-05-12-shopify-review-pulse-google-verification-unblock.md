# Shopify Review Pulse Google Verification Unblock

Created: 2026-05-12 16:19 UTC

## Decision

Keep Shopify Review Pulse on the one-email validation path. The next action is not more landing/report polish; it is completing Google sign-in verification for `reviewpulse@theshepherdstack.com`, then sending exactly one SellerPic email from Gmail web UI if SMTP remains unavailable from this host.

Approval line already open:

`VERIFY GOOGLE SIGN-IN: reviewpulse@theshepherdstack.com OUTBOUND ACCESS`

## Current Evidence

- `theshepherdstack.com` MX resolves to Google: `1 smtp.google.com.`
- `smtp.gmail.com:587` is not reachable from this host after an 8-second TCP timeout.
- `smtp.gmail.com:465` is not reachable from this host after an 8-second TCP timeout.
- Live offer page returns HTTP 200: `https://shopify-review-pulse-eta.vercel.app/offer.html`
- Live SellerPic locked preview returns HTTP 200 and `x-robots-tag: noindex, nofollow`: `https://shopify-review-pulse-eta.vercel.app/sellerpic-teardown.html`
- First send file is ready: `workspace/shopify-review-pulse/outreach/sellerpic-first-email.eml`
- Markdown send copy is ready: `workspace/shopify-review-pulse/outreach/sellerpic-first-email.md`

## Official Google Findings

Google Workspace security challenges are expected for suspicious or unfamiliar sign-ins. Google says login challenges can block access when identity cannot be verified, and recommends recovery phone/email details for accounts. Source: https://support.google.com/a/answer/6002699

If an authorized Workspace user cannot complete a login challenge, Google documents an admin-side temporary bypass: Admin console > Directory > Users > select user > Security > Login challenge > Turn Off For 10 Minutes. Source: https://support.google.com/a/answer/12077697

For SMTP from an app/device, Google Workspace documents `smtp.gmail.com` with SSL 465 or TLS 587, authenticated with the full Workspace email address and an app password. Source: https://support.google.com/a/answer/176600

Gmail app passwords require 2-Step Verification and may be unavailable for some work/school accounts or policy configurations. Source: https://support.google.com/mail/answer/185833

## Exact Owner Action

1. In a normal browser session, sign in to `reviewpulse@theshepherdstack.com`.
2. Complete the phone/security challenge.
3. Add recovery phone/email if prompted.
4. If Google keeps blocking the login, use the Admin console temporary bypass: `Directory > Users > reviewpulse@theshepherdstack.com > Security > Login challenge > Turn Off For 10 Minutes`, then sign in immediately.
5. Open Gmail for `reviewpulse@theshepherdstack.com`.
6. Send only the SellerPic message to `support@sellerpic.ai` using the copy in `workspace/shopify-review-pulse/outreach/sellerpic-first-email.md`.
7. Record the sent timestamp in `config/RUNLOG.md` or reply to AutoBox with `SENT: SHOPIFY REVIEW PULSE SELLERPIC <timestamp>`.

## Why Manual Gmail Send Beats More Automation Now

The first revenue signal needs one real human email, not a scalable outbound system. SMTP automation is currently blocked by network reachability from this host and would also require app-password/2SV policy work. Gmail web UI avoids both issues, preserves the real reply inbox, and gets the willingness-to-pay test into market immediately after verification.

## After The Send

- Wait 72 hours.
- If SellerPic replies, use `workspace/shopify-review-pulse/fulfillment/` to produce or quote the paid report.
- If SellerPic does not reply after 72 hours, send the A2Reviews fallback email in `workspace/shopify-review-pulse/outreach/a2reviews-fallback-email.md`.
- Do not batch-send.
- Do not create payment infrastructure unless `CREATE STRIPE PAYMENT LINK: SHOPIFY REVIEW PULSE $49 ONE-OFF REPORT` clears.

## Blocker Status

Blocked on owner-side Google verification only. No additional spend was made, no outreach was sent, and no payment infrastructure was created.
