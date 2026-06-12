# Write My Formula Excel TOROW / TOCOL Repair Page

Date: 2026-06-12 14:25 UTC

## Result

Shipped a no-spend repair-intent page:

https://writemyformula.com/excel-torow-tocol-not-working/

The page targets Excel users whose `TOROW` or `TOCOL` formula returns `#VALUE!`, `#NUM!`, `#SPILL!`, `#NAME?`, keeps or removes the wrong blanks/errors, scans in the wrong order, or returns the wrong flattened row/column.

## Evidence Used

- Microsoft TOROW support: https://support.microsoft.com/en-au/office/torow-function-b90d0964-a7d9-44b7-816b-ffa5c2fe2289
- Microsoft TOCOL support: https://support.microsoft.com/en-us/office/tocol-function-22839d9b-0b55-4fc1-b4e6-2761f8f122ed
- Microsoft #SPILL! support: https://support.microsoft.com/en-us/excel/how-to-correct-a-spill-error

These sources validated TOROW/TOCOL syntax, one-row versus one-column output, the `ignore` values `0`, `1`, `2`, and `3`, `scan_by_column`, `#VALUE!` and `#NUM!` behavior, and dynamic-array spill-range framing for `#SPILL!`.

## Work Completed

- Added `excel-torow-tocol-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added a homepage/shared generated-page card linking to the new route.
- Generated `workspace/sheetpilot-workbench/excel-torow-tocol-not-working/index.html`.
- Regenerated static SEO pages and `sitemap.xml`.
- Added focused content tests for the new page, homepage link, sitemap entry, checkout wiring, and forbidden public-copy claims.
- Ran Luke copy-risk review and kept the final copy bounded to one visible formula.
- Committed and pushed nested app commit `eb75b923 Add Excel TOROW TOCOL repair page`.
- Submitted the route, homepage, and sitemap to IndexNow; API returned HTTP `200`.

## Verification

- `npm run build:seo` passed.
- `npm test` passed `174/174`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Local Chromium desktop/mobile checks passed with expected local static-server analytics/API `POST 501` noise filtered; no horizontal overflow.
- Production route, homepage, sitemap, and actual Stripe checkout returned HTTP `200`.
- Live desktop/mobile Chromium checks returned correct title, H1, canonical, six checkout links, required ignore/version copy, no forbidden claims, no horizontal overflow, `0` console messages, and `0` page errors.

## Guardrails

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
