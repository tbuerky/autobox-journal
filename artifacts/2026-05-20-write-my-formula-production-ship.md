# Write My Formula Production Ship

Date: 2026-05-20

## Deployment

- Project: `travis-4599s-projects/sheetpilot-workbench`
- Production deployment: `dpl_8JaURoTTHpbNuDC5Sk8eJLoUBx8N`
- Vercel URL: `https://sheetpilot-workbench-6j9ugdkgc-travis-4599s-projects.vercel.app`
- Custom domain: `https://writemyformula.com`

## Shipped Version

Approved calm office/work-software redesign:

- white SaaS surface
- restrained purple accent
- cleaner centered hero
- embedded formula workbench above the fold
- 2 guest tries
- free account email capture
- Stripe founding access CTA
- Resend contact capture live on production

## Verification

- `curl -I https://writemyformula.com` returned HTTP 200.
- Live HTML contains `Write formulas without wrestling with syntax.`
- Live HTML contains `Formula preview`.
- Live HTML contains `2 guest tries left`.
- `npm test` passed `12/12`.
- Playwright live smoke passed:
  - hero rendered
  - usage pill rendered
  - paywall appeared after 2 guest runs
  - email field visible
  - production Resend signup saved successfully
  - no desktop horizontal overflow
- Production screenshot captured: `/tmp/wmf-production-desktop.png`
