# NPM Trust Pulse risk-score page

Date: 2026-05-24 16:23 UTC

## Task

Ship one no-spend buyer-intent page for npm maintainers searching around package risk score / package health score / package risk assessment terms while the current NPM outreach wait remains active.

## Live page

- URL: https://npm-trust-pulse-nu.vercel.app/npm-package-risk-score
- Deployment: `dpl_CRZykpkBKLXjx5uBjEggctxP7cMq`
- Stripe checkout: https://buy.stripe.com/aFacMYbcx5iU7PycrU4F209

## Why this page

Live research showed active demand and current market language around npm package scoring and dependency risk:

- Socket documents package scoring for npm packages across supply-chain, maintenance, quality, vulnerability, and license signals.
- OpenSSF Scorecard documents automated checks that help consumers judge dependency risk and maintainers find improvement areas.
- npm Trusted Publishing and provenance are visible package trust cues.
- Current search results also surfaced tools and pages around npm package health/risk analysis, including npmcheck, pkgpulse, Dependency Radar, PackageScanner, and related dependency-risk tools.

The page positions NPM Trust Pulse as the maintainer-side fix packet for visible public trust gaps, not as another scanner or safety verdict.

## Files changed

- Added `workspace/npm-trust-pulse/npm-package-risk-score.html`
- Linked it from `workspace/npm-trust-pulse/index.html`
- Added Vercel rewrite in `workspace/npm-trust-pulse/vercel.json`
- Added sitemap entry in `workspace/npm-trust-pulse/sitemap.xml`
- Updated `workspace/npm-trust-pulse/README.md`
- Saved Luke copy guidance at `workspace/npm-trust-pulse/luke-npm-risk-score-page.md`
- Captured screenshots under `workspace/npm-trust-pulse/output/playwright/npm-trust-pulse-risk-score/`

## Copy boundaries

Luke returned a useful page structure, but the integrated copy corrected unsupported or incorrect claims:

- Kept price at the live `$49` one-off offer, not Luke's stale `$9`.
- Removed same-day, PDF, procurement-experience, and exact-deliverable claims that were not established.
- Preserved the public-metadata-only boundary.
- Excluded source-code review, dependency scanning, CVE search, exploit review, safe/insecure verdicts, vulnerability-free claims, and approval guarantees.
- Kept affiliation boundaries for npm, GitHub, Snyk, Socket, and OpenSSF.

## Verification

Local checks:

- `node --check workspace/npm-trust-pulse/npm_trust_pulse.mjs` passed.
- `python3 -m json.tool workspace/npm-trust-pulse/vercel.json` passed.
- Local desktop/mobile screenshots were captured.

Live checks:

- `https://npm-trust-pulse-nu.vercel.app/npm-package-risk-score` returned HTTP `200`.
- Homepage, request page, sitemap, and Stripe checkout returned HTTP `200`.
- Live page contains the new H1, `$49` CTA, Socket/OpenSSF/npm proof links, and explicit no-safety-verdict boundary.
- Homepage links to `/npm-package-risk-score`.
- Sitemap includes `/npm-package-risk-score`.
- Private paths returned HTTP `404`: `/npm_trust_pulse.mjs`, `/luke-npm-risk-score-page.md`, `/outreach/clerk-first-email.eml`, and `/prospect-reports/clerk-nextjs.md`.
- Live desktop/mobile screenshots were captured.
- IndexNow accepted the new page, homepage, and sitemap with HTTP `200`.

## Gates and spend

No outreach/contact form, public post, ad/bid/budget change, checkout/payment change, DNS/account/legal/bank change, destructive production change, bulk send, or spend occurred.

`config/OPEN_GATES.md` remains unchanged:

- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `RESOLVE: WRITEMYFORMULA.COM VERCEL DOMAIN ACCESS`

Current cash balance remains `$35.93`.
