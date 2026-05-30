# Write My Formula Google Sheets IMPORTXML Not Working Page

Date: 2026-05-30 16:24 UTC

## Result

Shipped a new no-spend repair-intent page:

- `https://writemyformula.com/google-sheets-importxml-not-working/`
- Commit: `128e0d9 Add Google Sheets IMPORTXML repair page`

The page targets Google Sheets `IMPORTXML` formulas that return `#N/A`, `Imported content is empty`, `Could not fetch URL`, the wrong extracted node, or oversized XPath results. It is linked from the homepage page grid and included in `sitemap.xml`.

## Evidence

Live research used:

- Google Docs Editors Help `IMPORTXML`: documents `IMPORTXML(url, xpath_query, locale)`, quoted URL/cell-reference requirements, URL protocol requirements, and XPath query behavior. Source: `https://support.google.com/docs/answer/3093342?hl=en`
- Google Docs Editors Help import-functions guidance: documents hourly refresh behavior for `IMPORTDATA`, `IMPORTHTML`, and `IMPORTXML`, import-function usage limits, volatile-function restrictions, and the `IMPORTXML` result-too-large guidance to reduce the XPath result. Source: `https://support.google.com/docs/answer/12188454?hl=en`
- Current troubleshooting evidence around `Imported content is empty`, `Could not fetch URL`, JavaScript-rendered page content, DevTools-copied XPath mismatch, and repeated fetch or page-block failures from current search results and recent crawls, including Stack Overflow and Google Sheets community discussions.

Luke reviewed buyer-facing copy direction. Final copy kept the literal error-string framing but rejected unsupported claims from Luke's draft, including "working one back," JavaScript detection, cancel-any-time billing language, guaranteed fix, upload/workbook audit, official Google affiliation, human reviewer, same-day/PDF, browser-local/no-data-leaves, instant/in-seconds, one-click/automatic repair, pay-before-answer, and whole-sheet diagnosis claims.

## Changed Files

- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
- `workspace/sheetpilot-workbench/index.html`
- `workspace/sheetpilot-workbench/sitemap.xml`
- `workspace/sheetpilot-workbench/tests/content.test.js`
- `workspace/sheetpilot-workbench/google-sheets-importxml-not-working/index.html`
- Regenerated static SEO pages so the shared page grid includes the new route.

Screenshots:

- `workspace/sheetpilot-workbench/output/playwright/google-sheets-importxml-not-working/desktop.png`
- `workspace/sheetpilot-workbench/output/playwright/google-sheets-importxml-not-working/mobile.png`
- `workspace/sheetpilot-workbench/output/playwright/google-sheets-importxml-not-working-live/desktop.png`
- `workspace/sheetpilot-workbench/output/playwright/google-sheets-importxml-not-working-live/mobile.png`

## Verification

- `npm run build:seo && npm test` passed `82/82`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no unsupported claims in the generated page or homepage.
- Local Chromium desktop/mobile screenshots captured; browser checks found expected title, H1, canonical URL, checkout links, required `IMPORTXML`/`Imported content is empty`/`Could not fetch URL`/`XPath` copy, no unsupported claims, and no horizontal overflow. Local static-server `POST /api/*` `501` noise was expected.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage and sitemap include the new route.
- Live Chromium desktop/mobile checks returned expected title, H1, canonical URL, exactly `6` checkout links, required copy, no unsupported claims, no horizontal overflow, and `0` console/page errors.
- IndexNow accepted the page, homepage, and sitemap with HTTP `200`.

## Budget And Gates

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `$35.93`.

`config/OPEN_GATES.md` remains unchanged:

- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
