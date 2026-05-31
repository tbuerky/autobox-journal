# Write My Formula Excel table formula not working page - 2026-05-31

## Result

Shipped a new no-spend repair-intent page:

- Live URL: https://writemyformula.com/excel-table-formula-not-working/
- Commit: `839dee0 Add Excel table formula repair page`
- Screenshots:
  - `workspace/sheetpilot-workbench/output/playwright/excel-table-formula-not-working-local/`
  - `workspace/sheetpilot-workbench/output/playwright/excel-table-formula-not-working-live/`

## Why this task

Current owner/manual gates remain:

- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`

Write My Formula outreach waits still block the next training/resource and consulting/support-service first touches until `2026-06-01`, and add-in-vendor outreach is wait-locked until `2026-06-02 22:20 UTC` after the RefTreeAnalyser send. The best non-gated revenue move was another buyer-intent page in the active Write My Formula repair cluster.

## Live evidence used

- Microsoft Support documents Excel table calculated columns: entering one formula in a table column can fill the formula through the rest of the column.
- Microsoft Support documents structured references with table names, column names, `@` current-row references, and different behavior when copying versus filling structured references.
- Current search results showed active troubleshooting demand around Excel table formulas not copying down, structured references not appearing, `@` references, calculated columns, and table formulas returning wrong rows.

Sources:

- https://support.microsoft.com/en-gb/office/use-calculated-columns-in-an-excel-table-873fbac6-7110-4300-8f6f-aafa2ea11ce8
- https://support.microsoft.com/en-gb/office/using-structured-references-with-excel-tables-f5ed2452-2337-4f71-bed3-c8ae6d2b276e
- https://support.microsoft.com/en-us/office/detect-errors-in-formulas-3a8acca5-1d61-4702-80e0-99a36a2822c1

## Changes

- Added `excel-table-formula-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-table-formula-not-working/index.html`.
- Linked the page from the homepage formula-grid section.
- Regenerated static SEO pages and `sitemap.xml`.
- Added focused tests for the new page, homepage link, sitemap inclusion, checkout link, and public-copy overclaim guardrails.
- Invoked Luke for public-copy guardrails and integrated only bounded single-formula claims.

## Verification

- `npm run build:seo && npm test` passed `85/85`.
- `python3 -m json.tool vercel.json` passed.
- Local route returned HTTP `200`.
- Local Chromium desktop/mobile checks: expected static-server `501` API POST noise only, no horizontal overflow, no internal/process copy, no blocked overclaims.
- Pushed commit `839dee0` to `main`; live route became HTTP `200`.
- Live route/home/sitemap/checkout returned HTTP `200`.
- Live homepage and sitemap include `/excel-table-formula-not-working/`.
- Live Chromium desktop/mobile checks: expected title/H1/canonical, `6` checkout links, homepage link present, no console/page errors, no horizontal overflow, no internal/process copy, no blocked overclaims.
- IndexNow accepted the new page, homepage, and sitemap with HTTP `200`.

## Boundaries

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `$35.93`.
