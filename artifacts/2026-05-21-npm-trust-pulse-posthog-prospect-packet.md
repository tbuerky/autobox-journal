# NPM Trust Pulse PostHog Prospect Packet

Date: 2026-05-21 08:23 UTC

## Task

Move NPM Trust Pulse forward while existing spend, outreach, and payment-link gates remain uncleared by creating a second target-specific prospect packet.

## Current State

- Live offer: `https://npm-trust-pulse.vercel.app/`
- Live request page: `https://npm-trust-pulse.vercel.app/request`
- Live public sample: `https://npm-trust-pulse.vercel.app/posthog-js-sample`
- Current price shown publicly: `$49` one-off for one npm package report.
- Existing gates before this run:
  - `APPROVED: LAUNCH WRITE MY FORMULA GOOGLE SEARCH TEST, MAX $15`
  - `APPROVED: CONTACT RESEND WITH NPM TRUST PULSE SAMPLE`
  - `APPROVED: CREATE NPM TRUST PULSE STRIPE PAYMENT LINK, $49`

## Target Selected

PostHog's `posthog-js` package.

## Live Evidence

- npm downloads API returned `6,826,367` weekly downloads for `posthog-js` for `2026-05-13` to `2026-05-19`.
- npm registry metadata showed latest `posthog-js` version `1.374.3`, published `2026-05-20T13:33:41.563Z`.
- npm registry metadata showed license field `SEE LICENSE IN LICENSE`.
- GitHub API for `PostHog/posthog-js` showed `544` stars, `200` open issues, last push `2026-05-21T08:16:54Z`, and `archived: false`.
- The registry README text did not include `security`, `support`, `privacy`, or `vulnerability` before the first install/code section.
- GitHub advisory API shows the public advisory `GHSA-8775-5hwv-wr6v` was patched in `posthog-js` `1.57.2`; this packet does not claim any current vulnerability.
- Snyk's current `posthog-js` page describes the package as healthy/maintained and confirms the category demand for public package trust/security information.
- PostHog's Trust Center exists separately, so the issue is not absence of trust material; it is that key trust routes are not visible from the npm README fold.

## Files Created

- `workspace/npm-trust-pulse/prospect-reports/posthog-js.md`
- `workspace/npm-trust-pulse/outreach/posthog-send-control.md`
- `workspace/npm-trust-pulse/outreach/posthog-first-contact.md`
- `workspace/npm-trust-pulse/luke-posthog-first-contact.md`

## Recommendation

After the Resend gate either clears or is intentionally skipped, submit exactly one PostHog contact-form message using `workspace/npm-trust-pulse/outreach/posthog-first-contact.md`.

Exact approval line:

`APPROVED: SUBMIT POSTHOG CONTACT FORM WITH NPM TRUST PULSE SAMPLE`

## Boundaries

No outreach was sent. No contact form was submitted. No Stripe object/payment link/checkout URL was created. No public page, account, DNS, or post changed. No money was spent. Current budget balance remains `$35.93`.

## Sources

- npm registry and downloads APIs for `posthog-js`
- GitHub API for `PostHog/posthog-js`
- GitHub security advisory API for `PostHog/posthog-js`
- Snyk package page: `https://security.snyk.io/package/npm/posthog-js`
- PostHog Trust Center: `https://trust.posthog.com/`
- PostHog public site: `https://posthog.com/`
