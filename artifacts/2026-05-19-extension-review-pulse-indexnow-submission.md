# Extension Review Pulse IndexNow submission

Date: 2026-05-19 20:20 UTC

## Decision

Use IndexNow as the next non-gated traffic motion for Extension Review Pulse. Direct contact, payment links, and public posting are still owner-gated, but search-engine discovery can be advanced without spending money, creating accounts, publishing under Travis's identity, or contacting anyone.

## Source evidence

- IndexNow documentation says URL updates can be submitted by GET or POST after hosting a verification key file on the same host: https://www.indexnow.org/documentation
- IndexNow FAQ says a manual key file should be named `<key>.txt`, contain the same key, and be publicly accessible on the site: https://www.indexnow.org/faq
- Bing's IndexNow announcement says submitted URLs can be shared across participating IndexNow search engines, so one accepted submission can create broader discovery coverage: https://blogs.bing.com/webmaster/january-2022/IndexNow-Announcing-Sharing-of-Submitted-URLs

## Work completed

- Added the public verification key file:
  - `workspace/extension-review-pulse/c910fd76ed4eacbbb259b6f4b739be9a.txt`
  - live URL: `https://extension-review-pulse.vercel.app/c910fd76ed4eacbbb259b6f4b739be9a.txt`
- Updated the internal Extension Review Pulse README with the key-file URL.
- Deployed production:
  - deployment: `dpl_4qRQVwY7cQKkPhgvQkRxqEZ613Rs`
  - production alias: `https://extension-review-pulse.vercel.app`
- Submitted the five public sitemap URLs to `https://api.indexnow.org/indexnow`:
  - `https://extension-review-pulse.vercel.app/`
  - `https://extension-review-pulse.vercel.app/request`
  - `https://extension-review-pulse.vercel.app/tldr-youtube-sample`
  - `https://extension-review-pulse.vercel.app/extreviewbot-alternative`
  - `https://extension-review-pulse.vercel.app/chrome-web-store-review-checklist`

## Verification

- Key file live check returned HTTP 200 and body `c910fd76ed4eacbbb259b6f4b739be9a`.
- Offer page and request page returned HTTP 200 after deployment.
- Sitemap returned HTTP 200 and contains the five submitted public URLs.
- IndexNow POST returned HTTP 202 with an empty body.
- Locked Strawberry preview remains HTTP 200 with `X-Robots-Tag: noindex, nofollow`.
- Private outreach, fulfillment, and prospect-report paths return HTTP 404.
- Public-copy grep found no stale `$9`, internal owner/process language, or experiment language in deployable public files. The only `approval` matches are customer-facing guarantee disclaimers.

## Boundaries

No outreach, contact-form submission, public post, checkout/payment infrastructure, account creation, DNS change, backend/database work, or spend.

Current cash balance: `$57.18`.
