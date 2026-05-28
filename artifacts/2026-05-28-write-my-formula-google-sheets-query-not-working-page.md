# Write My Formula Google Sheets QUERY not working page - 2026-05-28

## Task
Ship one no-spend repair-intent page for Google Sheets QUERY formulas that fail with parse errors, `NO_COLUMN` / `Col` reference errors, wrong headers, mixed data types, blank output, or missing rows.

## Result
- Live page: https://writemyformula.com/google-sheets-query-not-working/
- Commit: `ec56c40 Add Google Sheets QUERY repair page`
- Deployment: `dpl_DscZGsFB1sGyYnmTrNK3tCDSuwzL`
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/google-sheets-query-not-working/`

## Evidence
- Google Docs Editors Help documents QUERY syntax as `QUERY(data, query, [headers])`, says the query text must be quoted or held in a cell reference, explains header guessing, and notes mixed-type columns use the majority type while minority types are treated as null values: https://support.google.com/docs/answer/3093343
- Current troubleshooting evidence showed exact QUERY failure language and demand around `Unable to parse query string for Function QUERY parameter 2`, `PARSE_ERROR`, `NO_COLUMN`, and `Col` reference mistakes, including live Stack Overflow and Reddit results.
- Luke reviewed the buyer-facing direction and recommended naming the exact QUERY error string in the first screen. Final copy used that recognition moment while rejecting unsupported claims around upload, workbook audit, official Google affiliation, guarantee, same-day/PDF, human review, browser-local/no-data-leaves, instant repair, and pay-before-answer.

## What changed
- Added `google-sheets-query-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/google-sheets-query-not-working/index.html`.
- Linked the route from the homepage and regenerated all static SEO pages so their embedded route grid includes the new page.
- Added sitemap coverage and focused content tests.

## Verification
- `npm run build:seo && npm test` passed `66/66`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no forbidden claims on the changed public page/homepage; matches in test/generator files were negative assertions or existing unrelated comparison copy.
- Local Playwright screenshots captured for desktop and mobile; local console issues were only expected static-server `501` POST noise.
- Live checks returned HTTP `200` for the new page, homepage, sitemap, and Stripe checkout URL.
- Live homepage and sitemap include `/google-sheets-query-not-working/`.
- Live Playwright desktop/mobile checks returned expected title, H1, canonical, `6` checkout links, required QUERY error copy, `NO_COLUMN`, mixed-type copy, and `0` console/page issues.
- IndexNow accepted the new page, homepage, and sitemap with HTTP `200`.

## Gates and budget
- `config/OPEN_GATES.md` remains unchanged: `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT` and `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`.
- No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.
- Current cash balance remains `$35.93`.
