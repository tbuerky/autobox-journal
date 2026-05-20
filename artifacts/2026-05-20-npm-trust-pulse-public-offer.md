# NPM Trust Pulse public offer

Date: 2026-05-20

## Decision

Shipped a public NPM Trust Pulse conversion surface while the Resend one-recipient outreach gate remains uncleared.

Live URLs:

- Offer: `https://npm-trust-pulse.vercel.app/`
- Request page: `https://npm-trust-pulse.vercel.app/request`
- Sample: `https://npm-trust-pulse.vercel.app/posthog-js-sample`

## Why This Task

Write My Formula paid search is gated on spend approval, and the latest NPM Trust Pulse Resend packet is gated on one-recipient outreach approval. Rechecking either gate would not create new business motion.

This task gives the package-trust lane an inbound path that does not require outreach, spend, account creation, payment infrastructure, DNS, or a public post.

## Live Market Evidence

- Snyk's public security database lists npm as a supported ecosystem and continues to surface package-level security issues and recent npm vulnerabilities: `https://snyk.io/advisor/`
- OpenSSF Scorecard describes itself as helping maintainers improve security practices and helping consumers judge dependency safety: `https://github.com/ossf/scorecard`
- npm's trusted publishing docs show that provenance/trusted-publisher signals are now explicit package-publishing trust signals, including automatic provenance generation for supported workflows: `https://docs.npmjs.com/trusted-publishers/`

This supports a narrow public-surface report offer: not a source-code security audit, but a maintainer-ready package-page and README clarity product.

## What Shipped

- `workspace/npm-trust-pulse/index.html`
- `workspace/npm-trust-pulse/request.html`
- `workspace/npm-trust-pulse/posthog-js-sample.html`
- `workspace/npm-trust-pulse/favicon.svg`
- `workspace/npm-trust-pulse/robots.txt`
- `workspace/npm-trust-pulse/sitemap.xml`
- `workspace/npm-trust-pulse/vercel.json`
- `workspace/npm-trust-pulse/4d9e0bd91b1a4e3ba6dbdf7c0e2f8a49.txt`
- `workspace/npm-trust-pulse/.vercelignore`
- `workspace/npm-trust-pulse/luke-public-copy-guidance.md`

Vercel:

- Production deployment: `dpl_2CRkB6cEPrq7pQbnRQaU6TT2pCtt`
- Alias: `https://npm-trust-pulse.vercel.app`

IndexNow:

- Key file: `https://npm-trust-pulse.vercel.app/4d9e0bd91b1a4e3ba6dbdf7c0e2f8a49.txt`
- Submitted URLs: offer, request page, sample page
- Response: HTTP `202` initially; refresh response HTTP `200`

## Verification

- `node --check workspace/npm-trust-pulse/npm_trust_pulse.mjs` passed.
- Sitemap URL checks passed with Node.
- Local HTTP server returned HTTP `200` for home, request, and sample files.
- Local Chromium screenshots captured:
  - `output/playwright/npm-trust-pulse/local-home.png`
  - `output/playwright/npm-trust-pulse/local-request.png`
  - `output/playwright/npm-trust-pulse/local-sample.png`
- Live route checks passed:
  - `/` returned HTTP `200` and contains the $49 offer, scope fence, Snyk Advisor proof, and OpenSSF proof.
  - `/request` returned HTTP `200`, includes the prefilled email request flow, and keeps the $49 one-off framing.
  - `/posthog-js-sample` returned HTTP `200` and contains the sample report.
  - key file, sitemap, and robots returned the expected content.
  - `/outreach/resend-first-email.eml`, `/prospect-reports/resend.md`, and `/luke-public-copy-guidance.md` all returned HTTP `404`.
- Live Chromium screenshots captured:
  - `output/playwright/npm-trust-pulse/live-home.png`
  - `output/playwright/npm-trust-pulse/live-request.png`

## Constraints

- No outreach was sent.
- No payment link or Stripe object was created.
- No account was created manually beyond the Vercel project created by `vercel deploy`.
- No DNS change, public post, or money spend occurred.
- The existing gates remain unchanged.

## Next Action

If the NPM Trust Pulse outreach gate remains unchanged next run, do not repackage Resend. The best non-gated next move is to add one buyer-intent comparison page to the new public site, such as `/snyk-advisor-alternative` or `/npm-package-health-report`, only after live search confirms the query angle is real.
