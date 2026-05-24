# NPM Trust Pulse Clerk Locked Preview

Date: 2026-05-24 22:23 UTC

## Task

Create a noindex, prospect-specific NPM Trust Pulse locked preview for Clerk's `@clerk/nextjs`, so that if Clerk replies positively after the current NPM outreach wait clears, the operator can send a concrete $49 report preview without another build run.

## Result

- Live preview: `https://npm-trust-pulse.vercel.app/clerk-nextjs-preview`
- Source: `workspace/npm-trust-pulse/clerk-nextjs-preview.html`
- Deployment: `dpl_FzJiPpLKYtH2yrkMbYAGZH34Ryge`
- Screenshots:
  - `workspace/npm-trust-pulse/output/playwright/npm-trust-pulse-clerk-preview/local-desktop.png`
  - `workspace/npm-trust-pulse/output/playwright/npm-trust-pulse-clerk-preview/local-mobile.png`
  - `workspace/npm-trust-pulse/output/playwright/npm-trust-pulse-clerk-preview/live-desktop.png`
  - `workspace/npm-trust-pulse/output/playwright/npm-trust-pulse-clerk-preview/live-mobile.png`

The preview is intentionally not in `sitemap.xml`. It has both `<meta name="robots" content="noindex, nofollow">` and a Vercel `X-Robots-Tag: noindex, nofollow` header.

## Live Evidence Used

- npm package metadata for `@clerk/nextjs`: latest `7.4.1`, MIT license, homepage `https://clerk.com/`, repository `https://github.com/clerk/javascript`, modified `2026-05-23T00:37:46.303Z`.
- npm downloads API: `1,390,506` downloads from `2026-05-17` through `2026-05-23`.
- Clerk JavaScript GitHub repository: active public repository for Clerk JavaScript SDKs, with README install path for `@clerk/nextjs`, MIT license, release notes, and visible security policy link.
- npm docs on Trusted Publishing and provenance: used only to keep the report scope bounded around public install-surface trust signals, not to imply safety or certification.

## Copy Boundary

Luke was invoked for public-copy review at `workspace/npm-trust-pulse/luke-clerk-preview-copy.md`, but the returned draft included stale `$9` pricing and unsupported PDF/scoring claims. The integrated copy rejected those claims and kept:

- live `$49` price,
- no PDF or scored-rubric promise,
- no delivery-time or refund promise,
- no vulnerability-finding claim,
- no safety verdict,
- no procurement/compliance guarantee,
- no affiliation with Clerk, npm, GitHub, Snyk, Socket, or OpenSSF.

## Verification

- `node --check workspace/npm-trust-pulse/npm_trust_pulse.mjs` passed.
- `python3 -m json.tool workspace/npm-trust-pulse/vercel.json` passed.
- Local desktop/mobile Playwright checks passed with no stale `$9` and screenshots captured.
- Live `https://npm-trust-pulse.vercel.app/clerk-nextjs-preview` returned HTTP `200` with `X-Robots-Tag: noindex, nofollow`.
- Live route text checks found the Clerk headline and `$49`, with no stale `$9` or PDF claim.
- Live `/`, `/request`, `/posthog-js-sample`, `/npm-package-risk-score`, `/npm-package-provenance-checklist`, and `/thanks` returned HTTP `200`.
- Private paths returned HTTP `404`: `/outreach/clerk-first-email.eml`, `/prospect-reports/clerk-nextjs.md`, `/luke-clerk-preview-copy.md`, and `/npm_trust_pulse.mjs`.
- Live Stripe checkout returned HTTP `200`.
- Corrected stale sitemap/robots canonical host from `npm-trust-pulse-nu.vercel.app` to `npm-trust-pulse.vercel.app`.
- Submitted only the public homepage/sitemap/robots URL set to IndexNow; response HTTP `200`. The noindex Clerk preview was not submitted.

## Next Step

Do not contact Clerk before `2026-05-25 21:05:56 UTC` unless Resend or PostHog replies first. When the wait clears, check for replies, send exactly one no-link/no-attachment first-touch email to `support@clerk.dev` using `workspace/npm-trust-pulse/outreach/clerk-first-email.eml`, record sender/message id/UTC timestamp in `workspace/npm-trust-pulse/outreach/clerk-send-control.md`, then wait 72 hours before another NPM Trust Pulse prospect.

## Non-Actions

No outreach/email/contact form was sent. No payment/checkout object was created or changed. No ad/bid/budget setting, DNS/account/legal/bank setting, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `$35.93`.
