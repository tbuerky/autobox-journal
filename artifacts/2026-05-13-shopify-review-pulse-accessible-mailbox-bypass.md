# Shopify Review Pulse Accessible Mailbox Bypass Recommendation

Date: 2026-05-13

## Outcome

Produced a concrete approval packet for the fastest non-spend path to get the first Shopify Review Pulse willingness-to-pay email sent while the branded `reviewpulse@theshepherdstack.com` mailbox remains blocked by Google sign-in verification.

No email was sent, no mailbox was accessed, no public page was changed, no checkout was created, and no spend occurred.

## Recommendation

Send the one already-approved SellerPic test from any owner-controlled mailbox Travis can access today, with a simple sender identity such as:

```text
From: Travis / The Shepherd Stack
To: support@sellerpic.ai
Subject: Locked public-review report preview for SellerPic
```

Use the existing body from:

```text
workspace/shopify-review-pulse/outreach/sellerpic-first-email.md
```

Keep the live links exactly as-is:

- `https://shopify-review-pulse-eta.vercel.app/sellerpic-teardown.html`
- `https://shopify-review-pulse-eta.vercel.app/offer.html`

After sending, record the timestamp in `config/RUNLOG.md` and wait 72 hours before using A2Reviews as the fallback.

## Why This Matters Now

The active Review Pulse lane has enough sales material for the first signal:

- live public offer page
- live locked SellerPic preview
- one-recipient SellerPic email draft and `.eml`
- A2Reviews fallback kit
- private fulfillment kit

The remaining blocker is not more collateral. It is reply-capable outbound access. If the branded mailbox stays blocked, waiting for perfect sender setup can delay the only signal that matters: whether a real Shopify app developer replies to the $49 report offer.

This bypass keeps the validation small and reversible: exactly one email, already approved as a one-email test, from an accessible owner-controlled inbox.

## Live Evidence Checked

- `https://shopify-review-pulse-eta.vercel.app/offer.html` returned HTTP 200 on 2026-05-13 10:18 UTC.
- `https://shopify-review-pulse-eta.vercel.app/sellerpic-teardown.html` returned HTTP 200 and `x-robots-tag: noindex, nofollow` on 2026-05-13 10:18 UTC.
- `workspace/shopify-review-pulse/outreach/sellerpic-first-email.eml` still parses to `support@sellerpic.ai`, subject `Locked public-review report preview for SellerPic`, and contains both current `shopify-review-pulse-eta.vercel.app` links.

## Live Research

- Google Workspace Admin docs say an admin can add up to 30 email aliases per user at no extra cost, and messages to the alias route to the user's primary inbox. Source: https://support.google.com/a/answer/33327?hl=en
- Google Workspace Admin docs also say the user must set up a custom From address in Gmail to send from an alias. Source: https://support.google.com/a/answer/33327?hl=en
- Gmail Help says Gmail can send from another owned address, but the address must be confirmed; work/school accounts may require SMTP server, username, and password. Source: https://support.google.com/mail/answer/22370?hl=en
- Gmail delegation docs say a Workspace user can grant access to another user in the same organization, and delegates can read/send email, but this is still Workspace configuration work. Source: https://developers.google.com/workspace/gmail/api/guides/delegate_settings

## Options Considered

1. **Keep waiting for `reviewpulse@theshepherdstack.com` verification.** Best branded path, but it has already stalled the only real validation signal.
2. **Send from an already-accessible owner-controlled mailbox.** Recommended for this one email. It avoids new spend, avoids new provider setup, preserves reply capture, and moves the validation forward now.
3. **Create an alias on an accessible Workspace user.** Good later, but still depends on admin setup and custom From configuration.
4. **Delegate the blocked mailbox to another user.** Potentially clean, but still requires Workspace administration and may not bypass the original security challenge quickly.
5. **Use Resend/Postmark/Brevo.** Rejected for this moment because provider setup solves sending but not reply capture as cleanly as an already-accessible inbox.

## Exact Approval Needed

```text
APPROVED: SEND SELLERPIC TEST FROM ACCESSIBLE OWNER MAILBOX
```

## What Happens Immediately After Approval

1. Travis identifies the accessible sender mailbox.
2. Send exactly one email to `support@sellerpic.ai` using the existing SellerPic draft.
3. Record the sender, send timestamp, and message subject in `RUNLOG.md`.
4. Keep `VERIFY GOOGLE SIGN-IN: reviewpulse@theshepherdstack.com OUTBOUND ACCESS` open until the branded mailbox is actually usable.
5. Wait 72 hours before sending the A2Reviews fallback.

## Current Budget

Cash remains `$162.45`. This recommendation requires no new spend.
