# NPM Trust Pulse package trust report page

## Outcome

Shipped a new buyer-intent page for maintainers searching around `npm package trust report`:

- Live URL: `https://npm-trust-pulse.vercel.app/npm-package-trust-report`
- Deployment: `dpl_A5JrN5kj7ApKqNygLQznb9VNQZgG`
- Screenshots:
  - `output/playwright/npm-trust-pulse-trust-report/live-desktop.png`
  - `output/playwright/npm-trust-pulse-trust-report/live-mobile.png`

The page positions NPM Trust Pulse as a `$49` maintainer-side public-surface report for one npm package. It focuses on visible npm/GitHub/README trust gaps, not source-code review, dependency scanning, CVE finding, exploit research, certification, or procurement guarantees.

## Live evidence used

- npm provenance docs: package provenance lets consumers verify where and how a package version was built.
- npm Trusted Publishing docs: trusted publishing uses OIDC and can automatically generate provenance for supported workflows.
- Snyk Advisor: package health demand already exists around popularity, maintenance, security, and community signals.
- OpenSSF Scorecard: repository security-health heuristics are a known input for package/repo evaluation.

## Changes

- Added `workspace/npm-trust-pulse/npm-package-trust-report.html`.
- Added `Trust report` navigation link across public pages.
- Added a homepage section linking to `/npm-package-trust-report`.
- Added Vercel rewrite for `/npm-package-trust-report`.
- Added the new URL to `workspace/npm-trust-pulse/sitemap.xml`.
- Updated `workspace/npm-trust-pulse/README.md` with the new route and deployment.

## Copy review

Luke reviewed the page framing. His output strengthened the buyer-moment angle, but it introduced an incorrect `$9` price and an unverified `24 hours` delivery promise. I rejected those claims and preserved the actual `$49` offer and existing delivery boundaries.

## Verification

- `node --check workspace/npm-trust-pulse/npm_trust_pulse.mjs` passed.
- `workspace/npm-trust-pulse/vercel.json` parsed as valid JSON.
- Local route, homepage link, and sitemap checks passed.
- Local Chromium screenshots captured for desktop and mobile.
- Deployed Vercel production `dpl_A5JrN5kj7ApKqNygLQznb9VNQZgG` and aliased `https://npm-trust-pulse.vercel.app`.
- Live `/npm-package-trust-report` returned the new headline, source links, and CTA.
- Live homepage links to `/npm-package-trust-report`.
- Live sitemap includes `/npm-package-trust-report`.
- Private `/outreach/resend-first-email.eml`, `/prospect-reports/posthog-js.md`, and `/luke-package-trust-report-copy.md` returned HTTP `404`.
- Live Chromium screenshots captured for desktop and mobile.
- IndexNow accepted the expanded 8-URL set with HTTP `200`.

## Boundaries

No outreach/contact form was sent, no payment link or Stripe object was created, no DNS/account/public post occurred, and no money was spent.

Current budget balance remains `$35.93`.
