# NPM Trust Pulse Package Health Report Page

Date: 2026-05-21 02:23 UTC

## Task

Ship one non-gated revenue-moving traffic asset for NPM Trust Pulse while the Write My Formula paid-search gate and Resend one-contact gate remain blocked.

## Result

- Live page: `https://npm-trust-pulse.vercel.app/npm-package-health-report`
- Updated offer page link: `https://npm-trust-pulse.vercel.app/`
- Deployment: `dpl_5fFSW4kzLVH3FSC2pynddsceXXP1`
- Screenshots:
  - `output/playwright/npm-trust-pulse-health-report/live-desktop.png`
  - `output/playwright/npm-trust-pulse-health-report/live-mobile.png`

## Market Evidence

Live research supported the page angle:

- Snyk Advisor publicly frames package health around popularity, maintenance, security, and community signals: `https://snyk.io/advisor/`
- OpenSSF Scorecard describes itself as security-health metrics that help maintainers improve security practices and consumers judge dependency safety: `https://github.com/ossf/scorecard`
- npm trusted publishing and provenance docs position OIDC publishing and provenance as public trust cues for npm packages: `https://docs.npmjs.com/trusted-publishers`
- Current package-health tools and pages exist around this exact language, including PkgPulse and Snyk package health surfaces.

The page positions NPM Trust Pulse as a maintainer-side `$49` report for public package health clarity. It does not claim to scan source code, find vulnerabilities, or replace Snyk/OpenSSF-style tools.

## What Changed

- Added `workspace/npm-trust-pulse/npm-package-health-report.html`.
- Added `/npm-package-health-report` rewrite in `workspace/npm-trust-pulse/vercel.json`.
- Added the new URL to `workspace/npm-trust-pulse/sitemap.xml`.
- Linked the new page from the homepage and public nav.
- Added a homepage section for visitors looking for an npm package health report.
- Updated `workspace/npm-trust-pulse/README.md` with the new page and deployment.
- Routed page copy through Luke, then corrected his stale `$9` suggestion back to the established `$49` price.

## Verification

- `node --check workspace/npm-trust-pulse/npm_trust_pulse.mjs` passed.
- Local file-route checks returned HTTP `200` for the public HTML files, sitemap, and IndexNow key.
- Local and live Chromium screenshots captured at desktop and mobile widths.
- Deployed to Vercel production and aliased to `https://npm-trust-pulse.vercel.app`.
- Live checks returned HTTP `200` for `/`, `/request`, `/posthog-js-sample`, `/snyk-advisor-alternative`, `/npm-package-health-report`, `/sitemap.xml`, and the IndexNow key file.
- Live private-path checks returned HTTP `404` for `/outreach/resend-first-email.eml`, `/prospect-reports/resend.md`, `/luke-npm-health-report-copy.md`, and `/luke-snyk-alternative-copy.md`.
- Live page contains the H1, `$49` CTA, no-source-code-review boundary, cited proof links, and non-affiliation footer.
- Live homepage links to `/npm-package-health-report`.
- Live sitemap includes `https://npm-trust-pulse.vercel.app/npm-package-health-report`.
- IndexNow accepted the five public URLs with HTTP `200`.

## Boundaries

No outreach was sent. No payment link or Stripe object was created. No DNS change, public post, new account signup, or spend occurred. Existing gates remain:

- `APPROVED: LAUNCH WRITE MY FORMULA GOOGLE SEARCH TEST, MAX $15`
- `APPROVED: CONTACT RESEND WITH NPM TRUST PULSE SAMPLE`

Current cash balance remains `$35.93`.
