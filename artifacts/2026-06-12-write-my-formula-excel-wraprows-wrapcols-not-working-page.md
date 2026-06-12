# Write My Formula Excel WRAPROWS / WRAPCOLS repair page

Date: 2026-06-12 12:25 UTC

## Outcome

Shipped `https://writemyformula.com/excel-wraprows-wrapcols-not-working/` as a no-spend repair-intent page for Excel users whose `WRAPROWS` or `WRAPCOLS` formula returns `#VALUE!`, `#NUM!`, `#N/A` padding, `#SPILL!`, `#NAME?`, the wrong wrap direction, or the wrong output shape.

## Why this task

Paid-search rollback/export remains owner-gated and Fluent Forms still requires manual reCAPTCHA submission. Marketplace/app-template, training/resource, and consulting/support outreach remain cooldown-limited until 2026-06-14 unless a relevant prospect replies first. A focused repair-intent page was the highest-leverage non-gated revenue motion this run.

## Live evidence

- Microsoft Support `WRAPROWS` documentation shows syntax `=WRAPROWS(vector, wrap_count, [pad_with])`, describes wrapping a row or column vector into rows, applies to Excel for Microsoft 365 / Excel 2024, and documents `#VALUE!`, `#NUM!`, and default `#N/A` padding behavior: `https://support.microsoft.com/en-us/office/wraprows-function-796825f3-975a-4cee-9c84-1bbddf60ade0`
- Microsoft Support `WRAPCOLS` documentation shows syntax `=WRAPCOLS(vector, wrap_count, [pad_with])`, describes wrapping a row or column vector into columns, applies to Excel for Microsoft 365 / Excel 2024, and documents the same one-dimensional vector, wrap-count, and padding errors: `https://support.microsoft.com/en-us/office/wrapcols-function-d038b05a-57b7-4ee0-be94-ded0792511e2`
- Current search results also showed user confusion around WRAPCOLS with two-dimensional data and `#NAME?` version availability, supporting the repair angle rather than a generic formula reference page.

## What changed

- Added `excel-wraprows-wrapcols-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-wraprows-wrapcols-not-working/index.html`.
- Added a homepage/shared related-link card and regenerated the static page grid plus `sitemap.xml`.
- Added focused regression tests to `workspace/sheetpilot-workbench/tests/content.test.js`.
- Saved Luke copy-risk notes at `workspace/sheetpilot-workbench/luke-excel-wraprows-wrapcols-not-working.md`.
- Committed and pushed nested app commit `8e380ac1 Add Excel WRAPROWS WRAPCOLS repair page`.

## Copy boundaries

Luke flagged that Google Sheets does not have native `WRAPROWS` / `WRAPCOLS`, so the final page is Excel-only. Final public copy avoids unsupported upload/workbook-audit, guarantee, official Microsoft affiliation/partner, human-review, same-day/PDF, instant/one-click/automatic-fix, payment-before-answer, exact-cause, whole-workbook/spreadsheet, and Google Sheets native-WRAPROWS/WRAPCOLS claims.

## Verification

- `npm run build:seo` passed.
- `npm test` passed `173/173`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Targeted public-copy scan found no internal/process language or unsupported claims in the new route or homepage.
- Local Chromium desktop/mobile checks passed with expected title, H1, canonical URL, six checkout links, required `WRAPROWS` / `WRAPCOLS` / `pad_with` / `TOCOL or TOROW` copy, no horizontal overflow, and no page errors. Local static-server POST `501` noise was expected.
- Production route, homepage, sitemap, and actual Stripe checkout returned HTTP `200`.
- Live Chromium desktop/mobile checks passed with expected title, H1, canonical URL, six checkout links, required copy, no banned copy, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow accepted the new route, homepage, and sitemap with HTTP `200`.

Screenshots:

- `workspace/sheetpilot-workbench/output/playwright/excel-wraprows-wrapcols-not-working/desktop-local.png`
- `workspace/sheetpilot-workbench/output/playwright/excel-wraprows-wrapcols-not-working/mobile-local.png`
- `workspace/sheetpilot-workbench/output/playwright/excel-wraprows-wrapcols-not-working/desktop-live.png`
- `workspace/sheetpilot-workbench/output/playwright/excel-wraprows-wrapcols-not-working/mobile-live.png`

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `-$24.07`.
