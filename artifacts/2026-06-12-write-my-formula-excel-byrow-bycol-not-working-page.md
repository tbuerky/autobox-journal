# Write My Formula Excel BYROW / BYCOL not working page - 2026-06-12

## Outcome

Shipped a no-spend repair-intent page:

https://writemyformula.com/excel-byrow-bycol-not-working/

The page targets Excel users whose `BYROW` or `BYCOL` formula returns `#CALC!`, `#VALUE!`, `#SPILL!`, `#NAME?`, wrong row/column direction, or a LAMBDA return-shape mistake.

## Why this task

Paid-search changes remain gated and the Fluent Forms contact form remains manual-reCAPTCHA gated. Outreach categories are cooling down until 2026-06-14 unless a relevant active prospect replies. A buyer-intent repair page was the highest-leverage non-gated motion available this run because it creates another searchable path into the existing `$9` Write My Formula funnel without spend.

## Live evidence

- Microsoft BYROW support: https://support.microsoft.com/en-us/office/byrow-function-2e04c677-78c8-4e6b-8c10-a4602f2602bb
- Microsoft BYCOL support: https://support.microsoft.com/en-us/excel/bycol-function
- Microsoft LAMBDA support: https://support.microsoft.com/en-us/excel/lambda-function
- Current search/forum results showed active confusion around BYROW/BYCOL with `#CALC!`, `#VALUE!`, nested arrays, and wrong output shape.

Evidence used in copy:

- BYROW applies a LAMBDA to each row and returns one result per row.
- BYCOL applies a LAMBDA to each column and returns one result per column.
- Microsoft currently lists BYROW and BYCOL for Excel for Microsoft 365 and Excel 2024.
- BYROW/BYCOL repair should stay scoped to the visible formula, source array, LAMBDA parameter, single-value return, spill range, and version support.

## Public-copy guardrails

Luke reviewed copy risk in `workspace/sheetpilot-workbench/luke-excel-byrow-bycol-not-working.md`. Final copy is Excel-only and avoids:

- Google Sheets BYROW/BYCOL claims.
- Works-in-every-version claims.
- Workbook audit or full spreadsheet repair claims.
- Guaranteed diagnosis, exact-cause, instant, automatic, one-click, human-review, same-day, PDF, or payment-before-answer claims.
- Microsoft affiliation, official Microsoft, or Microsoft partner claims.

## Changes

- Added `excel-byrow-bycol-not-working` in `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-byrow-bycol-not-working/index.html`.
- Added the homepage/shared related-link card.
- Regenerated static pages and `sitemap.xml`.
- Added focused content tests in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Committed and pushed nested app commit `8e02189c Add Excel BYROW BYCOL repair page`.

## Verification

- `npm run build:seo` passed.
- `npm test` passed `175/175`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Local desktop/mobile Chromium checks passed with only expected local static-server `POST 501` analytics/API noise.
- Production route returned HTTP `200`.
- Production homepage returned HTTP `200` and links to the route.
- Production sitemap returned HTTP `200` and includes the route.
- Actual Stripe checkout URL returned HTTP `200`.
- Live desktop/mobile Chromium checks returned correct title, H1, canonical, six checkout links, no horizontal overflow, no console/page errors, required copy present, and no banned-copy hits.
- IndexNow submission returned HTTP `200`.

## What did not happen

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
