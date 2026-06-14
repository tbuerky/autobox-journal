# Write My Formula Google Sheets IMPORTHTML Not Working Page

Date: 2026-06-14 20:23 UTC

## Task

Shipped a no-spend repair-intent page for Google Sheets users whose `IMPORTHTML` formula returns `#N/A`, `"imported content is empty"`, `"could not fetch URL"`, the wrong table/list, or no output because the result cannot expand.

Live URL: https://writemyformula.com/google-sheets-importhtml-not-working/

Nested app commit: `8231f956 Add Google Sheets IMPORTHTML repair page`

## Live Research

- Google Docs Editors Help documents `IMPORTHTML(url, query, index)` as importing data from a table or list in an HTML page. It also documents quoted URL/cell-reference behavior, `query` values of `"list"` or `"table"`, and separate table/list indexes starting at `1`: https://support.google.com/docs/answer/3093339
- Current public support/search evidence showed recurring IMPORTHTML friction around `"imported content is empty"`, `"could not fetch URL"`, public page accessibility, JavaScript-loaded content, wrong table/list index, and output space issues.

## What Changed

- Added `google-sheets-importhtml-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/google-sheets-importhtml-not-working/index.html`.
- Linked the new route from the homepage/shared generated page grid.
- Added the route to `sitemap.xml`.
- Added focused tests in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Saved Luke copy-risk review at `workspace/sheetpilot-workbench/luke-google-sheets-importhtml-not-working.md`.

Final copy avoids Google affiliation, upload/workbook audit, whole-sheet/full-sheet audit, guarantees, instant/automatic/one-click fixes, human-review, same-day/PDF, privacy-superiority, payment-before-answer claims, and claims that JavaScript/private/blocked pages can always be repaired from a formula rewrite.

## Verification

- `npm run build:seo` passed.
- `npm test` passed `193/193`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Production route returned HTTP `200` after deployment.
- Production homepage returned HTTP `200` and links the new page.
- Production sitemap returned HTTP `200` and includes the new URL.
- Actual Stripe checkout returned HTTP `200`.
- Live desktop and mobile Chromium checks returned correct title/H1, six checkout links, required import-index copy, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow POST for route, homepage, and sitemap returned HTTP `200`.

## Gates, Spend, and Non-Actions

Open gates remain unchanged:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
