# Shopify Review Pulse Gate Recheck and Inbound Risk

Date: 2026-05-13 14:18 UTC

## Outcome

Rechecked the active Shopify Review Pulse validation path and confirmed no owner gate has cleared.

The strongest current blocker is now explicit: the public request CTAs and both locked report previews still send buyers to `reviewpulse@theshepherdstack.com`, but that mailbox is not confirmed accessible. Until either the Google sign-in gate or the free Tally intake gate clears, inbound demand could be lost even if a prospect clicks "Request the full report."

No email was sent. No public page was changed. No checkout, account, DNS, or payment infrastructure was created. No spend.

## Live Checks

- `https://shopify-review-pulse-eta.vercel.app/offer.html` returned HTTP 200.
- `https://shopify-review-pulse-eta.vercel.app/sellerpic-teardown.html` returned HTTP 200 and `x-robots-tag: noindex, nofollow`.
- `https://shopify-review-pulse-eta.vercel.app/a2reviews-teardown.html` returned HTTP 200 and `x-robots-tag: noindex, nofollow`.
- `theshepherdstack.com` MX still resolves to Google: `1 smtp.google.com.`
- TCP checks from this host to `smtp.gmail.com:587` and `smtp.gmail.com:465` still timed out or failed.
- The SellerPic `.eml` still points to `support@sellerpic.ai` and uses current `shopify-review-pulse-eta.vercel.app` links.
- The A2Reviews `.eml` still points to `support@a2rev.com` and uses current `shopify-review-pulse-eta.vercel.app` links.

## Inbound Risk Found

`rg` confirmed the live public pages still use `mailto:` CTAs to the blocked mailbox:

- `workspace/shopify-review-pulse/offer.html` -> `mailto:reviewpulse@theshepherdstack.com`
- `workspace/shopify-review-pulse/sellerpic-teardown.html` -> `mailto:reviewpulse@theshepherdstack.com`
- `workspace/shopify-review-pulse/a2reviews-teardown.html` -> `mailto:reviewpulse@theshepherdstack.com`

This is not a new defect; it is exactly why the existing Tally gate matters. The current public surface is reachable, but the response path is fragile until Travis either verifies the mailbox or approves a free intake form.

## Gate Reconciliation

No active gate has resolution evidence in `OWNER_MESSAGES.md`, `HANDOFF.md`, `BUDGET.md`, or live checks. Keep all five Review Pulse gates open:

- `VERIFY GOOGLE SIGN-IN: reviewpulse@theshepherdstack.com OUTBOUND ACCESS`
- `CREATE STRIPE PAYMENT LINK: SHOPIFY REVIEW PULSE $49 ONE-OFF REPORT`
- `APPROVED: PUBLISH SHOPIFY REVIEW PULSE FOUNDER POST`
- `APPROVED: CREATE FREE TALLY INTAKE FORM FOR SHOPIFY REVIEW PULSE`
- `APPROVED: SEND SELLERPIC TEST FROM ACCESSIBLE OWNER MAILBOX`

## Next Real Move

Do not build more Review Pulse collateral by default.

Fastest unblock remains one of:

1. `APPROVED: SEND SELLERPIC TEST FROM ACCESSIBLE OWNER MAILBOX` — send exactly one SellerPic email from an owner-controlled reply-capable inbox.
2. `VERIFY GOOGLE SIGN-IN: reviewpulse@theshepherdstack.com OUTBOUND ACCESS` — send exactly one SellerPic email from Gmail web UI if SMTP still fails.
3. `APPROVED: CREATE FREE TALLY INTAKE FORM FOR SHOPIFY REVIEW PULSE` — replace public `mailto:` CTAs so inbound requests are capturable before outreach or public posting.

## Budget

Cash remains `$162.45`. This run used no paid services and created no new recurring spend.
