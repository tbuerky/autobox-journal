# Write My Formula Excel PivotTable Calculated Field Repair Page

## Task

Ship one no-spend buyer-intent page for Excel users searching because a PivotTable calculated field is rejected, returns surprising totals, uses normal cell references, or needs helper-column logic before aggregation.

## Evidence

- Microsoft Support documents that PivotTable formulas are different from worksheet formulas: calculated fields/items are only available for non-OLAP PivotTables, cannot use normal cell references or defined names, and calculated fields operate on summed underlying field totals rather than each source row.
- Microsoft Support separately documents a calculated-field grand-total issue where multiplication/division can produce a surprising total because Excel computes arithmetic on summed component fields.
- Current search evidence showed live troubleshooting demand around calculated fields being disabled, wrong calculated-field totals, and confusion about whether a calculated field can solve row-level pivot logic.
- Public-copy review used Luke. Final copy kept the page bounded to one pasted formula plus source-field context, and avoided upload, workbook audit, official Microsoft affiliation, guaranteed fix, human review, browser-local/no-data-leaves, instant, same-day, one-click/automatic repair, PDF, whole-workbook, and pay-before-answer claims.

Sources:

- Microsoft Support, Calculate values in a PivotTable: `https://support.microsoft.com/en-us/office/calculate-values-in-a-pivottable-11f41417-da80-435c-a5c6-b0185e59da77`
- Microsoft Support, Calculated field returns incorrect grand total in Excel: `https://support.microsoft.com/en-au/topic/calculated-field-returns-incorrect-grand-total-in-excel-fef60c02-5268-28e9-e7a8-ac1577a28e94`

## Output

- Shipped page: `https://writemyformula.com/excel-pivot-table-calculated-field-not-working/`
- Commit: `f40e8c6 Add Excel PivotTable calculated field repair page`
- Updated `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`, generated `workspace/sheetpilot-workbench/excel-pivot-table-calculated-field-not-working/index.html`, regenerated generated SEO pages and `sitemap.xml`, added a homepage link card, and added focused content tests.
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/excel-pivot-table-calculated-field-not-working-live/desktop.png` and `mobile.png`.

## Verification

- `npm run build:seo && npm test` passed `101/101`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no internal/process language or blocked overclaim phrases.
- GitHub push to `main` completed and Vercel production served the route.
- Live route returned HTTP `200`.
- Live homepage includes the new route; live sitemap includes the new route; live Stripe checkout returned HTTP `200`.
- Live Chromium desktop/mobile checks returned expected title, H1, canonical URL, `6` checkout links, required PivotTable repair copy, no horizontal overflow, and `0` console/page errors.
- IndexNow accepted the page, homepage, and sitemap with HTTP `200`.

## Gates and Budget

`config/OPEN_GATES.md` remains unchanged:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `-$24.07`.
