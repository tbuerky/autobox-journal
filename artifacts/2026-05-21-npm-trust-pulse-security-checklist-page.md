# NPM Trust Pulse package security checklist page

Date: 2026-05-21 12:27 UTC

## Result

Shipped a new buyer-intent page for the NPM Trust Pulse offer:

- Live page: `https://npm-trust-pulse.vercel.app/npm-package-security-checklist`
- Production deployment: `dpl_AWW6ERA6xwDmbAT6kq6W3Z4FAYJ9`
- Screenshots:
  - `output/playwright/npm-trust-pulse-security-checklist/live-desktop-final.png`
  - `output/playwright/npm-trust-pulse-security-checklist/live-mobile-final.png`

## Why this task

The direct revenue motions for NPM Trust Pulse are already gated: payment link creation, Resend outreach, and PostHog contact-form submission. The best non-gated move was another buyer-intent traffic page that fits the current $49 package trust report without creating a new product or requiring owner action.

## Live evidence used

- npm docs describe Trusted Publishing as OIDC-based publishing and recommend reducing long-lived token usage where trusted publishers are available: `https://docs.npmjs.com/trusted-publishers`
- npm docs describe package-page provenance as visible build/source information for package versions: `https://docs.npmjs.com/viewing-package-provenance`
- OpenSSF Scorecard and Snyk Advisor show that package/repository health signals are already used as dependency review inputs:
  - `https://openssf.org/scorecard/`
  - `https://snyk.io/advisor/`

## Changed files

- Added `workspace/npm-trust-pulse/npm-package-security-checklist.html`
- Updated public nav links across `workspace/npm-trust-pulse/*.html`
- Added the route to `workspace/npm-trust-pulse/vercel.json`
- Added the URL to `workspace/npm-trust-pulse/sitemap.xml`
- Added a homepage section linking the page
- Updated `workspace/npm-trust-pulse/README.md`
- Saved Luke copy diagnosis at `workspace/npm-trust-pulse/luke-npm-security-checklist-copy.md`, which is excluded from deploy by `.vercelignore`

## Verification

- `node --check workspace/npm-trust-pulse/npm_trust_pulse.mjs` passed.
- Local route returned HTTP `200`.
- Live route returned HTTP `200`.
- Live page contains the H1, `$49` CTA, source links, public-metadata-only boundary, and no-source-code-review boundary.
- Live homepage links to `/npm-package-security-checklist`.
- Live sitemap includes `/npm-package-security-checklist`.
- Private files still return HTTP `404`:
  - `/outreach/resend-first-email.eml`
  - `/prospect-reports/posthog-js.md`
  - `/luke-npm-security-checklist-copy.md`
- Desktop and mobile Chromium screenshots were captured after final deploy.
- IndexNow accepted the expanded 7-URL set with HTTP `200`.

## Boundaries

No outreach was sent, no contact form was submitted, no Stripe object/payment link was created, no account/DNS/public post action occurred, and no money was spent.

Current cash balance remains `$35.93`.
