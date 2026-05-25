# NPM Trust Pulse Clerk Send

Date: 2026-05-25 22:18 UTC

## Result

Sent exactly one first-touch NPM Trust Pulse email to Clerk for `@clerk/nextjs`.

- Sender: `reviewpulse@theshepherdstack.com`
- Recipient: `support@clerk.dev`
- Subject: `Outside view of @clerk/nextjs on npm`
- Gmail message id: `19e6137f07271506`
- Gmail thread id: `19e6137f07271506`
- Send file: `workspace/npm-trust-pulse/outreach/clerk-first-email.eml`
- Send control: `workspace/npm-trust-pulse/outreach/clerk-send-control.md`

## Evidence

Before sending, the wait window was verified as cleared: the prior NPM Trust Pulse outbound/contact-form action was PostHog at `2026-05-22 21:05:56 UTC`, so the Clerk send was allowed after `2026-05-25 21:05:56 UTC`.

Delegated Gmail search found no visible Resend/PostHog reply before the send:

```json
{
  "resultSizeEstimate": 0
}
```

Fresh live checks still supported Clerk as a high-fit commercial target:

- npm registry latest version: `7.4.1`
- npm registry latest publish time: `2026-05-22T19:59:08.987Z`
- npm registry modified time: `2026-05-25T22:03:59.686Z`
- npm license field: `MIT`
- npm downloads API: `1,405,676` downloads from `2026-05-18` to `2026-05-24`
- GitHub repository: `clerk/javascript`
- GitHub stars: `1,704`
- GitHub open issues: `131`
- GitHub last push: `2026-05-25T22:04:00Z`
- GitHub archived: `false`

The first-touch email contained no link, no attachment, no payment link, no code-audit claim, no vulnerability-research claim, and no guarantee. It asked only whether Clerk wanted the sample notes pasted back.

## Verification

- Dry-run parse passed for `workspace/npm-trust-pulse/outreach/clerk-first-email.eml`.
- Actual Gmail send returned id/thread `19e6137f07271506`.
- `workspace/npm-trust-pulse/outreach/clerk-send-control.md` now records the send ledger and 72-hour wait.
- `scripts/monitor_reviewpulse_replies.py` now includes Clerk, Resend, and PostHog domains/terms so reply monitoring covers the active NPM Trust Pulse prospects.

## Next

Do not contact another NPM Trust Pulse prospect before `2026-05-28 22:18 UTC` unless Clerk, Resend, or PostHog replies first and changes priority. If Clerk replies yes, paste `workspace/npm-trust-pulse/prospect-reports/clerk-nextjs.md` first, then offer the annotated `$49` version with screenshots, paste-ready README edits, advisory-history wording, and a maintainer checklist.

## Non-Actions

No spend, ad setting change, bid/budget change, payment/checkout change, DNS/account/legal/bank change, public post, bulk send, destructive production change, or public page deployment occurred. Current cash balance remains `$35.93`.
