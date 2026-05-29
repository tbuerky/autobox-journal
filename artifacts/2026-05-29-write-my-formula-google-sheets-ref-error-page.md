# Write My Formula Google Sheets #REF! error page - 2026-05-29

## Task
Ship one no-spend buyer-intent page for Google Sheets `#REF!` repair demand while outreach classes and owner/manual gates remained closed.

## Live research
- Google `ERROR.TYPE` maps `#REF!` as a recognized spreadsheet error value and documents companion error-checking functions: https://support.google.com/docs/answer/3238305?hl=en
- Google Sheets function list documents `ISREF` for checking valid cell references, `INDIRECT` for text-built references, `IMPORTRANGE`, `FILTER`, `QUERY`, and other functions implicated in broken-reference repairs: https://support.google.com/docs/table/25273?hl=en
- Google `INDIRECT` docs specify that it returns a reference from a quoted reference string, supporting the page's focus on text-built references that no longer resolve: https://support.google.com/docs/answer/3093377?hl=en
- Current search evidence showed active repair demand around Google Sheets `#REF!`, deleted or renamed sheets/ranges, invalid references, blocked array output, `IMPORTRANGE` source/access issues, and formula references that worked before a sheet restructure.

## Output
- Added `https://writemyformula.com/google-sheets-ref-error/`.
- Updated `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Regenerated static SEO pages and `sitemap.xml`.
- Linked the new route from the homepage formula grid.
- Added focused content tests in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Luke copy direction saved at `workspace/sheetpilot-workbench/luke-google-sheets-ref-error-page.md`.
- Commit: `60d2c35 Add Google Sheets REF error page`.
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/google-sheets-ref-error/live-desktop.png` and `live-mobile.png`.

## Verification
- `npm run build:seo && npm test` passed `72/72`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no internal/process language on the changed page; the only matched term was existing customer-facing `IMPORTRANGE` copy.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage and sitemap include `/google-sheets-ref-error/`.
- Live browser check returned expected title, H1, canonical URL, `6` checkout links, required `#REF!`, `IMPORTRANGE`, and `INDIRECT` copy, and `0` console/page errors on desktop and mobile.
- IndexNow accepted page/home/sitemap with HTTP `200`.

## Gates and spend
`config/OPEN_GATES.md` remains unchanged with:
- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `$35.93`.
