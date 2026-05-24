# NPM Trust Pulse Clerk Prospect Packet

Date: 2026-05-24

## Task

Prepared the third-prospect NPM Trust Pulse packet for Clerk's `@clerk/nextjs` package without sending outreach, because the current NPM Trust Pulse reply window remains open until `2026-05-25 21:05:56 UTC`.

## Why Clerk

Clerk is a strong fit for a `$49` public npm package trust-surface report because `@clerk/nextjs` is a high-adoption commercial auth SDK. The package page, README, support route, security route, and patched advisory context are all visible surfaces developers evaluate before installing an auth package.

## Evidence

- npm registry metadata: `@clerk/nextjs` latest `7.4.1`, published `2026-05-22T19:59:08.987Z`, registry modified `2026-05-23T00:37:46.303Z`.
- npm downloads API: `1,390,506` downloads from `2026-05-17` to `2026-05-23`.
- GitHub API: `clerk/javascript`, `1,704` stars, `131` open issues, last pushed `2026-05-24T09:17:49Z`, not archived, MIT.
- Package README: visible docs, changelog, bug, feature, help, support, security, and license sections.
- Clerk contact page: public support route with `support@clerk.dev`.
- Clerk repo security docs: vulnerability reports route to `security@clerk.dev`; this outreach does not use that address because the report is not vulnerability research.
- GitHub security advisories API: recent patched auth/route-protection advisories exist for Clerk packages, including `@clerk/nextjs`; the packet treats this as context, not as a current-risk claim.

## Files Created

- `workspace/npm-trust-pulse/prospect-reports/clerk-nextjs.md`
- `workspace/npm-trust-pulse/outreach/clerk-send-control.md`
- `workspace/npm-trust-pulse/outreach/clerk-first-email.eml`
- `workspace/npm-trust-pulse/luke-clerk-first-contact.md`

## Copy Controls

Luke reviewed first-touch framing. I used the no-link, reply-first structure but corrected Luke's stale `$9` wording back to the live `$49` offer in the private send-control and avoided price in the first-touch email.

The email avoids:

- current-vulnerability claims,
- source-code audit claims,
- alarmist security framing,
- unsupported "customers are confused" claims,
- meeting asks,
- attachments or links.

## Verification

- `.eml` headers parse with recipient `support@clerk.dev` and subject `Outside view of @clerk/nextjs on npm`.
- Public-source evidence was collected from npm, GitHub, Clerk README/security/contact surfaces, and web search.
- `.vercelignore` already excludes markdown, outreach, and prospect-report files from the public deploy surface.

## External Action

No email was sent. No contact form was submitted. No public page, DNS, account, checkout, ad, budget, or payment setting was changed. No spend occurred.

## Next Step

If no Resend or PostHog reply changes priority, send exactly one Clerk first-touch email after `2026-05-25 21:05:56 UTC`, then record the Gmail message id/thread id in `workspace/npm-trust-pulse/outreach/clerk-send-control.md` and wait `72` hours before any next NPM Trust Pulse prospect.

Current cash balance remains `$35.93`.
