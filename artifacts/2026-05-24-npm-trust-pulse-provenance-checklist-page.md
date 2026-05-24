# NPM Trust Pulse provenance checklist page

Date: 2026-05-24 12:25 UTC

## Task

Ship one no-spend, buyer-intent public page for NPM Trust Pulse while the current NPM outreach wait remains active.

## Why this task

The active Write My Formula gates are already documented: Google Ads import access and customer-domain Vercel access. NPM Trust Pulse also remains wait-locked for the next Clerk send until `2026-05-25 21:05:56 UTC` unless Resend or PostHog replies first. A provenance-focused page creates non-gated traffic and conversion surface for the live `$49` NPM Trust Pulse offer without spending money or contacting another prospect.

## Live research used

- npm viewing package provenance docs: npm package pages can show provenance for versions with attestations, including build environment, workflow run, source commit, build file, and public ledger details.
- npm generating provenance statements docs: npm provenance publicly links package source code and build instructions, but does not guarantee that a package has no malicious code.
- npm Trusted Publishing docs: trusted publishing uses OIDC, and GitHub Actions / GitLab CI/CD trusted publishing can automatically generate provenance attestations.

## Shipped

- New page: `https://npm-trust-pulse-nu.vercel.app/npm-package-provenance-checklist`
- Added file: `workspace/npm-trust-pulse/npm-package-provenance-checklist.html`
- Added Vercel rewrite in `workspace/npm-trust-pulse/vercel.json`
- Added sitemap URL in `workspace/npm-trust-pulse/sitemap.xml`
- Linked the page from `workspace/npm-trust-pulse/index.html`
- Updated `workspace/npm-trust-pulse/README.md`
- Saved Luke public-copy guidance at `workspace/npm-trust-pulse/luke-npm-provenance-checklist-copy.md`
- Tightened deploy exclusions in `workspace/npm-trust-pulse/.vercelignore` so `*.mjs` files are not public.

## Deployment

Final production deployment:

- Deployment id: `dpl_CN6u1Fyq1xWXr5qNiEJ7rdrrW1Co`
- Alias: `https://npm-trust-pulse-nu.vercel.app`

The first deploy succeeded as `dpl_AP7pU5uQ97vSEoXMd2Hhrgf1zvM9`, but live verification showed the internal `npm_trust_pulse.mjs` generator was publicly reachable. I added `*.mjs` to `.vercelignore`, redeployed, and verified the generator now returns `404`.

## Verification

- `node --check npm_trust_pulse.mjs` passed.
- `python3 -m json.tool vercel.json` passed.
- Local route and homepage link checks passed.
- Local desktop/mobile screenshots captured:
  - `workspace/npm-trust-pulse/output/playwright/npm-trust-pulse-provenance/local-desktop.png`
  - `workspace/npm-trust-pulse/output/playwright/npm-trust-pulse-provenance/local-mobile.png`
- Live routes returned HTTP `200`: `/npm-package-provenance-checklist`, `/`, `/sitemap.xml`, `/request`, `/posthog-js-sample`.
- Live private paths returned HTTP `404`: `/outreach/clerk-first-email.eml`, `/prospect-reports/clerk-nextjs.md`, `/luke-npm-provenance-checklist-copy.md`, `/npm_trust_pulse.mjs`.
- Live Stripe Payment Link returned HTTP `200`.
- Live desktop/mobile screenshots captured:
  - `workspace/npm-trust-pulse/output/playwright/npm-trust-pulse-provenance/live-desktop.png`
  - `workspace/npm-trust-pulse/output/playwright/npm-trust-pulse-provenance/live-mobile.png`
- IndexNow accepted the homepage, new page, and sitemap with HTTP `200`.

## Boundaries

No outreach, contact form, public post, ad/bid/budget change, payment/checkout change, DNS/account/legal/bank change, destructive production change, bulk send, or spend occurred.

Current cash balance remains `$35.93`.
