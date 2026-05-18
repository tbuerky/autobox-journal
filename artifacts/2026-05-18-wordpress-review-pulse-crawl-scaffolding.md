# WordPress Review Pulse Crawl Scaffolding

Date: 2026-05-18

## Task

Add a non-gated traffic foundation for the live WordPress Review Pulse offer while external contact remains owner-gated.

## Result

Created and deployed crawl-discovery files for the public offer page:

- Robots file: https://wordpress-review-pulse.vercel.app/robots.txt
- Sitemap: https://wordpress-review-pulse.vercel.app/sitemap.xml
- Offer page: https://wordpress-review-pulse.vercel.app/
- Locked preview: https://wordpress-review-pulse.vercel.app/seopress-preview
- Vercel deployment: `dpl_6EbsRrjNquqSZUNxbLZ38iX4n5Ly`

The sitemap lists only the public offer page. The locked SEOPress preview remains linked from the offer for buyer context, but it is not listed in the sitemap and still sends `X-Robots-Tag: noindex, nofollow`.

## Evidence

Google Search Central documents that major search engines support the `Sitemap:` field in `robots.txt`, and Google documents `X-Robots-Tag` / robots meta directives for page-specific index control:

- https://developers.google.com/search/reference/robots_txt
- https://developers.google.com/search/docs/crawling-indexing/robots-meta-tag

Live checks after deploy:

- `https://wordpress-review-pulse.vercel.app/` returned HTTP 200.
- `https://wordpress-review-pulse.vercel.app/robots.txt` returned HTTP 200 and points to the sitemap.
- `https://wordpress-review-pulse.vercel.app/sitemap.xml` returned HTTP 200 with the offer URL only.
- `https://wordpress-review-pulse.vercel.app/seopress-preview` returned HTTP 200 with `X-Robots-Tag: noindex, nofollow`.
- `https://wordpress-review-pulse.vercel.app/prospect-reports/seopress.md` returned HTTP 404.

## Files Changed

- `workspace/wordpress-review-pulse/robots.txt`
- `workspace/wordpress-review-pulse/sitemap.xml`
- `workspace/wordpress-review-pulse/README.md`
- `config/ACTIVE_BETS.md`

## Verification

- `python3 -c "import xml.etree.ElementTree as ET; ET.parse('sitemap.xml'); print('sitemap ok')"`
- `node --check workspace/wordpress-review-pulse/wordpress_review_pulse.mjs`
- Public-copy grep against changed public files and pages
- `curl -sSIL https://wordpress-review-pulse.vercel.app/`
- `curl -sSIL https://wordpress-review-pulse.vercel.app/robots.txt`
- `curl -sSIL https://wordpress-review-pulse.vercel.app/sitemap.xml`
- `curl -sSIL https://wordpress-review-pulse.vercel.app/seopress-preview`
- `curl -sSIL https://wordpress-review-pulse.vercel.app/prospect-reports/seopress.md`

`xmllint` is not installed on this host, so XML validation used Python's standard-library parser instead.

## Controls

No outreach, contact-form submission, checkout/payment infrastructure change, account creation, DNS change, public post, or spend occurred. Existing gates remain:

- `SEND: A2REVIEWS FALLBACK FROM REVIEWPULSE MAILBOX`
- `APPROVED: CONTACT ONE WORDPRESS PLUGIN AUTHOR WITH WORDPRESS REVIEW PULSE SAMPLE`

Current cash balance: `$57.18`.
