# Write My Formula Google Sheets Conditional Formatting Repair Page

Date: 2026-05-30 20:24 UTC

## Outcome

Shipped a new no-spend repair-intent page:

- `https://writemyformula.com/google-sheets-conditional-formatting-not-working/`
- Commit: `54c748d Add Google Sheets conditional formatting repair page`
- Screenshots and browser verification:
  - `workspace/sheetpilot-workbench/output/playwright/google-sheets-conditional-formatting-not-working/`
  - `workspace/sheetpilot-workbench/output/playwright/google-sheets-conditional-formatting-not-working-live/`

The page targets Google Sheets conditional-formatting custom formulas that work in a normal cell but fail in the rule dialog, highlight nothing, highlight the wrong rows, use the wrong `$` anchors, lose to another rule, or need `INDIRECT` for another sheet.

## Evidence

Live/current research checked:

- Google Docs Editors Help conditional-formatting docs for custom formulas, same-sheet reference limits, `INDIRECT` for another sheet, whole-row examples, absolute vs relative references, copied rules, and rule-order behavior.
- Google Docs Editors Help table-reference docs for the limitation that table references are not supported in conditional formatting.
- Current troubleshooting results around custom formulas not working in the rule dialog, wrong cells or rows being highlighted, top-left/apply-to-range confusion, `$A2` versus `A$2` anchor mistakes, and cross-sheet reference confusion.
- Luke reviewed buyer-facing copy direction and recommended the frustration-led frame: formula works in a cell, conditional formatting still does nothing or highlights the wrong rows.

Sources:

- https://support.google.com/docs/answer/78413/use-conditional-formatting-rules-in-google-sheets-computer
- https://support.google.com/docs/answer/15637642
- https://stackoverflow.com/questions/30401769/how-do-i-get-google-sheet-conditional-formatting-custom-formulas-to-refer-to-rel
- https://stackoverflow.com/questions/27905600/conditional-formatting-with-custom-formula-referencing-the-cell-itself

## Changes

- Added `google-sheets-conditional-formatting-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/google-sheets-conditional-formatting-not-working/index.html`.
- Linked the page from the homepage and regenerated all static SEO pages plus `sitemap.xml`.
- Added focused tests for the page, homepage link, sitemap inclusion, checkout wiring, and unsupported-claim exclusions.
- Created Luke copy notes at `workspace/sheetpilot-workbench/luke-google-sheets-conditional-formatting-not-working-page.md`.

## Verification

- `npm run build:seo && npm test` passed `84/84`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no unsupported claims in the new page or homepage card.
- Local Chromium desktop/mobile checks returned HTTP `200`, expected title/H1, no horizontal overflow, and only expected static-server `501` API POST noise.
- Pushed `main` to GitHub; Vercel served the live route after deployment propagation.
- Live route/home/sitemap/checkout returned HTTP `200`.
- Live homepage and sitemap include the new route.
- Live Chromium desktop/mobile checks returned expected title/H1, `6` checkout links on the route, route link present, no horizontal overflow, and `0` console/page errors.
- IndexNow accepted the new route, homepage, and sitemap with HTTP `200`.

## Gates and Budget

`config/OPEN_GATES.md` remains unchanged:

- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `$35.93`.
