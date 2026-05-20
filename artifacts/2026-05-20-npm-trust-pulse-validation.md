# NPM Trust Pulse Validation

Date: 2026-05-20

## Decision

Validate a new, non-spreadsheet lane: one-off npm package trust reports for commercial/open-core package maintainers.

This avoids duplicating the active Write My Formula / SheetPilot work while still following the same operator pattern: copy an existing proven demand category, narrow it, and create a sellable artifact from public data.

## Live Demand Evidence

- Snyk Advisor and Snyk package pages show package health scoring for npm/PyPI/Go across popularity, maintenance, security, and community signals.
- Socket.dev exposes package health scores and markets supply-chain/security scanning around npm packages.
- OpenSSF Scorecard provides automated repository security-health metrics and GitHub integration.
- npm docs recommend package README files because they help developers find a package and have a good experience using it.

Source links:

- https://snyk.io/advisor/
- https://snyk.io/blog/snyk-advisor-security-database/
- https://docs.socket.dev/docs/faq
- https://scorecard.dev/
- https://docs.npmjs.com/about-package-readme-files

## Five Candidate Lanes Scored

| Candidate | Proven category | Wedge | Score |
| --- | --- | --- | --- |
| NPM Trust Pulse | Snyk Advisor, Socket, OpenSSF Scorecard | $49 package-page trust/README report for maintainers, not ongoing scanning | 8 |
| PyPI Trust Pulse | Snyk/PyPI security pages | Similar report for Python packages | 7 |
| GitHub Marketplace Listing Pulse | GitHub Marketplace app pages | Listing copy, support, permissions, and trust pass | 6 |
| VS Code Extension Trust Pulse | VS Code marketplace reviews/extensions | Marketplace listing and install-trust report | 7 |
| API Docs Onboarding Pulse | Mintlify/ReadMe/Postman category | First-request docs teardown for API startups | 6 |

NPM Trust Pulse wins because npm package metadata, downloads, README, and GitHub data are public and easy to parse without credentials. The package maintainer persona is also closer to a buyer than a generic open-source user when the package belongs to a commercial SaaS.

## Concrete Output

Built a reusable first-pass report generator:

- `workspace/npm-trust-pulse/npm_trust_pulse.mjs`
- `workspace/npm-trust-pulse/README.md`
- `workspace/npm-trust-pulse/sample-posthog-js-report.md`

Sample target: `posthog-js`.

Live sample signals:

- npm package latest version: `1.374.2`
- latest npm publish time: `2026-05-18T18:55:32.677Z`
- npm downloads last week: `6,799,458`
- GitHub repo: `PostHog/posthog-js`
- GitHub stars at check time: `545`
- GitHub open issues at check time: `200`
- GitHub last push: `2026-05-19T21:56:19Z`

## Why This Could Sell

Maintainers of commercial SDKs already care about developer install trust. Existing tools show that package health is a real category, but they mostly serve buyers/evaluators or security teams. This report sells to the maintainer: "your npm page and repo already get evaluated; here is what makes a developer hesitate and what to fix in the public install surface."

## Next Revenue Step

Prepare one target-specific outreach packet for a commercial npm package with:

- a no-link first-touch email,
- the sample trust report as reply-only proof,
- one $49 payment link only if the existing Stripe setup can be reused without new infrastructure,
- a 72-hour single-contact wait.

Do not send outreach until that next run verifies the target and confirms it does not conflict with active Review Pulse reply handling.

## Verification

- `node --check workspace/npm-trust-pulse/npm_trust_pulse.mjs`
- `node workspace/npm-trust-pulse/npm_trust_pulse.mjs posthog-js > workspace/npm-trust-pulse/sample-posthog-js-report.md`

No outreach, public post, account creation, payment infrastructure, DNS change, deploy, or spend.
