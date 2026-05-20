# NPM Trust Pulse Snyk Advisor Alternative Page

Date: 2026-05-20 22:24 UTC

## Task

Ship one non-gated revenue-moving traffic asset for NPM Trust Pulse while the Write My Formula paid-search gate and Resend one-contact gate remain blocked.

## Result

- Live page: `https://npm-trust-pulse.vercel.app/snyk-advisor-alternative`
- Updated offer page link: `https://npm-trust-pulse.vercel.app/`
- Deployment: `dpl_7XBtA7dQWFcYbsH9VQzn8GAzDUgD`
- Screenshots:
  - `output/playwright/npm-trust-pulse-snyk-alternative/live-desktop.png`
  - `output/playwright/npm-trust-pulse-snyk-alternative/live-mobile.png`

## Market Evidence

Live checks reconfirmed that package trust and security-health review are established categories:

- Snyk Advisor publicly positions package health scoring around npm package security, popularity, maintenance, and community signals: `https://snyk.io/advisor/`
- OpenSSF Scorecard describes itself as security health metrics for open source, for maintainers improving security practices and consumers judging dependency safety: `https://github.com/ossf/scorecard`
- npm provenance docs say provenance lets consumers verify where and how a package was built before trusting it: `https://docs.npmjs.com/generating-provenance-statements`
- npm trusted publishing docs emphasize OIDC publishing, automatic provenance, and reduced long-lived token risk: `https://docs.npmjs.com/trusted-publishers`

The page does not claim to beat those tools. It positions NPM Trust Pulse as the maintainer-side companion: a `$49` public-surface report that turns visible npm/GitHub/README/support/provenance signals into paste-ready improvements.

## What Changed

- Added `workspace/npm-trust-pulse/snyk-advisor-alternative.html`.
- Added `/snyk-advisor-alternative` rewrite in `workspace/npm-trust-pulse/vercel.json`.
- Added the new URL to `workspace/npm-trust-pulse/sitemap.xml`.
- Linked the comparison page from the homepage, request page, and sample page nav.
- Added a homepage section for visitors looking for a Snyk Advisor alternative.
- Updated `workspace/npm-trust-pulse/README.md`.
- Routed public copy through Luke, then corrected his stale `$9` recommendation back to the established `$49` price.

## Verification

- Local HTTP check for `/snyk-advisor-alternative.html` passed and contained the H1, `$49` CTA, scope boundaries, and non-affiliation footer.
- Local screenshots captured at desktop and mobile widths.
- Deployed to Vercel production and aliased to `https://npm-trust-pulse.vercel.app`.
- Live checks returned HTTP `200` for `/`, `/request`, `/posthog-js-sample`, `/snyk-advisor-alternative`, `/sitemap.xml`, and the IndexNow key file.
- Live private-path checks returned HTTP `404` for `/outreach/resend-first-email.eml`, `/prospect-reports/resend.md`, and `/luke-snyk-alternative-copy.md`.
- Live page contains the H1, `$49` report CTA, no-source-code-review boundary, and non-affiliation footer.
- Live homepage links to the comparison page.
- Live sitemap includes `https://npm-trust-pulse.vercel.app/snyk-advisor-alternative`.
- Live desktop and mobile screenshots captured.
- IndexNow accepted the four public URLs with HTTP `200`.

## Boundaries

No outreach was sent. No payment link or Stripe object was created. No DNS change, public post, new account signup, or spend occurred. Existing gates remain:

- `APPROVED: LAUNCH WRITE MY FORMULA GOOGLE SEARCH TEST, MAX $15`
- `APPROVED: CONTACT RESEND WITH NPM TRUST PULSE SAMPLE`

Current cash balance remains `$35.93`.
