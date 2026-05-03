# StrikeRewind canonical/sitemap/robots www-alignment

**Date:** 2026-05-03
**Branch:** `autobox/strikerewind-rename`
**Commit:** `1dbebb2`
**Vercel deploy:** `dpl_CTzesofjqaT1WfzNV2WoJKnvCD5v` (READY, production)
**Spend:** $0
**Cash balance:** $162.45

## What was wrong

Earlier today's pre-testing smoke test (`artifacts/2026-05-03-strikerewind-pre-testing-smoke-test.md`) surfaced an apex/www canonical mismatch:

- Vercel project has `strikerewind.com` configured to redirect to `www.strikerewind.com` (verified: `HTTP/2 307` → `location: https://www.strikerewind.com/`).
- Source tree declared the apex (`https://strikerewind.com/`) as the canonical URL on five surfaces:
  - `frontend/index.html` — `<link rel="canonical">`, `og:url`, `og:image`, `twitter:image`
  - `frontend/public/sitemap.xml` — three `<loc>` URLs
  - `frontend/public/robots.txt` — `Sitemap:` directive

Net effect: every crawler that hit a canonical URL would have followed a 301/307 to www, then potentially indexed the redirect target as a separate URL from the declared canonical, splitting page-level SEO signal between apex and www variants of every page.

Soft issue today (marketing freeze in place, no traffic to lose), but a real problem to land before `TESTING COMPLETE: STRIKEREWIND` clears and crawl/indexing kicks on.

## What changed

Two paths considered:

1. **Swap Vercel redirect direction** (www → apex) so canonical=apex matches live behavior. Modern SEO preference. Requires touching live infra config on a recently-launched production site.
2. **Update source-tree canonical to www** to match the existing redirect direction. No infra change. Single commit, deploys via existing pipeline.

Picked option 2 — lower risk, no live infra touch, and the canonical-vs-redirect symmetry is what the SEO signal actually cares about; apex-vs-www brand preference is a separate cosmetic call we can revisit later.

Five-line edit across three files (`+9 / -9`):

- `frontend/index.html:12` — `<link rel="canonical" href="https://strikerewind.com/" />` → `https://www.strikerewind.com/`
- `frontend/index.html:16` — `og:url` content → www
- `frontend/index.html:19` — `og:image` content → www
- `frontend/index.html:27` — `twitter:image` content → www
- `frontend/public/sitemap.xml` — three `<loc>` URLs → www; `lastmod` on root URL bumped from `2026-05-01` → `2026-05-03` to reflect the change
- `frontend/public/robots.txt` — `Sitemap:` URL → www

## Verification

- `cd frontend && npm run build` clean (1921 modules, JS `353.76 kB`, CSS `22.83 kB`, no warnings).
- Built artifacts contain only `https://www.strikerewind.com/` references for canonical/og/sitemap/robots.
- Pushed `1dbebb2` to `autobox/strikerewind-rename` on `tbuerky/StrikeSight`.
- `vercel deploy --prod --token $VERCEL_TOKEN_TSS --yes` from `frontend/` returned `dpl_CTzesofjqaT1WfzNV2WoJKnvCD5v` `READY` `production`.
- Live verification:
  - `https://www.strikerewind.com/` HTTP 200, all 5 head meta tags now reference www.
  - `https://www.strikerewind.com/sitemap.xml` returns the new sitemap with 3 www URLs.
  - `https://www.strikerewind.com/robots.txt` returns the new sitemap directive pointing at www.
  - `https://strikerewind.com/` still 307→`https://www.strikerewind.com/` (apex redirect intact).
  - `https://strikerewind.com/sitemap.xml` 307→ www (apex redirect applies sitewide, expected).

## What was deliberately NOT done

- Did NOT swap Vercel redirect direction (option 1 above) — would require touching live domain config; not worth the risk vs source-tree fix.
- Did NOT route through Cove or Luke — purely mechanical SEO alignment, no design or copy judgment.
- Did NOT touch `Privacy.tsx` / `Terms.tsx` email mentions of `privacy@strikerewind.com` / `support@strikerewind.com` — those are bare email addresses, not URLs. Apex is correct in an email address regardless of redirect direction.
- Did NOT add new pages to the sitemap — landing/privacy/terms is the right public surface set; auth surfaces stay disallowed in robots.txt as before.
- Did NOT trigger Render redeploy — backend is unaffected (no canonical references in backend code).

## Open gates after this run

Unchanged:
- `STRIPE LIVE CONFIGURED: STRIKEREWIND` — Travis-side, 3-step Stripe Dashboard packet at `artifacts/2026-05-02-strikerewind-stripe-live-products-and-webhook-packet.md`.
- `TESTING COMPLETE: STRIKEREWIND` — Travis-side, marketing freeze stays until done.

No new gates raised. No spend.
