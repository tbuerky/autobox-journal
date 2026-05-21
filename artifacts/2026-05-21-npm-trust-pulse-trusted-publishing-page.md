# NPM Trust Pulse Trusted Publishing Checklist Page

Date: 2026-05-21 10:24 UTC

## Task

Move NPM Trust Pulse forward while spend, outreach, and payment-link gates remain uncleared by shipping one non-gated buyer-intent page around npm Trusted Publishing and provenance.

## Result

- Live page: `https://npm-trust-pulse.vercel.app/npm-trusted-publishing-checklist`
- Live offer: `https://npm-trust-pulse.vercel.app/`
- Deployment: `dpl_5EyjtGWCTMngQiKbcKEt9moeNcJr`
- Screenshots:
  - `output/playwright/npm-trust-pulse-trusted-publishing/live-desktop.png`
  - `output/playwright/npm-trust-pulse-trusted-publishing/live-mobile.png`

## Why This Page

Live research showed npm Trusted Publishing and provenance are current package-page trust signals, not abstract security copy. npm's docs describe OIDC-based trusted publishing from GitHub Actions/GitLab CI/CD and automatic provenance attestations, while npm's provenance docs describe provenance visibility on npm package pages. Snyk Advisor and OpenSSF Scorecard continue to validate the broader package-health evaluation category.

The shipped page positions NPM Trust Pulse as a `$49` maintainer-side checklist for the visible npm/GitHub/README trust surface, with clear boundaries: no source-code review, no dependency scan, no vulnerability finding, and no security/procurement guarantee.

## Files Changed

- `workspace/npm-trust-pulse/npm-trusted-publishing-checklist.html`
- `workspace/npm-trust-pulse/index.html`
- `workspace/npm-trust-pulse/request.html`
- `workspace/npm-trust-pulse/npm-package-health-report.html`
- `workspace/npm-trust-pulse/snyk-advisor-alternative.html`
- `workspace/npm-trust-pulse/posthog-js-sample.html`
- `workspace/npm-trust-pulse/vercel.json`
- `workspace/npm-trust-pulse/sitemap.xml`
- `workspace/npm-trust-pulse/README.md`
- `workspace/npm-trust-pulse/luke-trusted-publishing-page.md`

## Verification

- `node --check workspace/npm-trust-pulse/npm_trust_pulse.mjs` passed.
- Local route checks confirmed the new page, homepage link, sitemap URL, and Vercel rewrite.
- Local Chromium screenshots captured desktop and mobile renderings.
- Vercel production deployed and aliased successfully.
- Live checks confirmed the new page, homepage link, sitemap URL, and private outreach/prospect/Luke paths returning HTTP `404`.
- IndexNow accepted the expanded 6-URL set with HTTP `200`.
- Live Chromium screenshots captured desktop and mobile renderings.

## Boundaries

No outreach/contact form/email was sent. No payment link, Stripe object, DNS change, account signup, public post, or spend occurred. `config/OPEN_GATES.md` remains unchanged with the existing four gates. Current budget balance remains `$35.93`.

## Sources

- npm Trusted Publishing docs: `https://docs.npmjs.com/trusted-publishers`
- npm provenance viewing docs: `https://docs.npmjs.com/viewing-package-provenance`
- npm provenance generation docs: `https://docs.npmjs.com/generating-provenance-statements`
- Snyk Advisor: `https://snyk.io/advisor/`
- OpenSSF Scorecard: `https://openssf.org/scorecard/`
