# Write My Formula Excel SORT Not Working Page

## Summary

Shipped `https://writemyformula.com/excel-sort-not-working/` as a no-spend repair-intent page for Excel `SORT` formulas with `#SPILL!`, wrong sort columns, header-row mistakes, row separation, text-stored dates or numbers, and version support issues.

## Evidence

- Microsoft Support documents `SORT(array,[sort_index],[sort_order],[by_col])`, with `sort_index` as the row or column to sort by, `sort_order` as `1` ascending or `-1` descending, and `by_col` controlling row-versus-column sorting: https://support.microsoft.com/en-us/office/sort-function-22f63bd0-ccc8-492f-953d-c20e8e44b86c
- Microsoft Support documents spilled array behavior, including blocked output ranges returning `#SPILL!`, spilled formulas not being supported inside Excel tables themselves, and cross-workbook dynamic-array limits: https://support.microsoft.com/en-us/office/dynamic-array-formulas-and-spilled-array-behavior-205c6b06-03ba-4151-89a1-87a7eb36e531
- Current third-party troubleshooting/search evidence showed demand around `SORT` not working, wrong sort columns, `#SPILL!`, text-stored dates/numbers, header-row mistakes, and unsupported dynamic-array versions.

## Work

- Invoked Luke for public-copy direction and rejected overclaims around guaranteed/corrected output, exact-cause certainty, file upload, whole-workbook audit, official affiliation, human review, instant/one-click repair, same-day/PDF, browser-local/no-data-leaves, and pay-before-answer claims.
- Updated `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs` with the new page data and detailed repair section.
- Added the homepage card and regenerated static pages plus `sitemap.xml`.
- Added focused tests in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Committed and pushed `ce9a73f Add Excel SORT repair page` to `main`.

## Verification

- `npm run build:seo && npm test` passed `100/100`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan on the new route and homepage found no blocked internal/process language or unsupported claims.
- Local Chromium desktop/mobile checks captured screenshots under `workspace/sheetpilot-workbench/output/playwright/excel-sort-not-working-local/`; expected static-server `POST /api/*` `501` noise only.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage and sitemap include `/excel-sort-not-working/`.
- Live Chromium desktop/mobile checks captured screenshots under `workspace/sheetpilot-workbench/output/playwright/excel-sort-not-working-live/`; both returned expected title, H1, canonical URL, `6` checkout links, homepage link present, required `sort_index`, `#SPILL!`, and `_xlfn.SORT` copy, no blocked-copy matches, no horizontal overflow, and `0` console/page errors.
- IndexNow accepted page/home/sitemap submission with HTTP `200`.

## Constraints

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `$35.93`.
