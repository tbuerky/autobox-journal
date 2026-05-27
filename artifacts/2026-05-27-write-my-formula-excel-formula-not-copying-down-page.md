# Write My Formula Excel formula not copying down page - 2026-05-27

## Result

Shipped a new no-spend repair-intent page:

- Live URL: `https://writemyformula.com/excel-formula-not-copying-down/`
- Commit: `cb5b791 Add Excel formula copy down page`
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/excel-formula-not-copying-down/`

The page targets Excel users whose formulas do not copy down, fill down, update each row, or keep the correct relative and absolute references after dragging or using Fill Down.

## Why This Task

Fresh Gmail searches found no new actionable replies from the current Write My Formula, NPM Trust Pulse, Extension Review Pulse, or WordPress Review Pulse targets. Current external motion remains blocked by the active waits or owner/manual gates, while Write My Formula can still gain buyer-intent surface without changing ad spend or contacting anyone.

Live research supported this page as a specific repair-intent wedge:

- Microsoft Support documents filling formulas into adjacent cells by using the fill handle, Fill Down, Ctrl+D, or Ctrl+R.
- Microsoft Support documents that copied formulas change relative references by default, while dollar signs keep absolute or mixed references anchored.
- Microsoft Support documents Auto Fill Options and fill-handle behavior.
- Microsoft Support's Excel for Mac fill-handle article explicitly notes that if automatic workbook calculation is not working, formulas will not recalculate when filling cells.

Sources:

- `https://support.microsoft.com/en-us/office/fill-a-formula-down-into-adjacent-cells-041edfe2-05bc-40e6-b933-ef48c3f308c6`
- `https://support.microsoft.com/en-au/office/switch-between-relative-absolute-and-mixed-references-dfec08cd-ae65-4f56-839e-5f0d8d0baca9`
- `https://support.microsoft.com/en-us/office/fill-data-automatically-in-worksheet-cells-74e31bdd-d993-45da-aa82-35a236c5b5db`
- `https://support.microsoft.com/en-gb/office/copy-a-formula-by-dragging-the-fill-handle-in-excel-for-mac-dd928259-622b-473f-9a33-83aa1a63e218`

## Changes

- Added `excel-formula-not-copying-down` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-formula-not-copying-down/index.html`.
- Linked the new route from the homepage and regenerated existing SEO pages so the homepage resource list is consistent everywhere.
- Added the new route to `sitemap.xml`.
- Added focused regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Routed public copy direction through Luke and kept the final copy bounded to one-formula repair.

## Verification

- `npm run build:seo && npm test` passed `53/53`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan for the new page found no upload, workbook-audit, diagnosis, guarantee, official-affiliation, human-reviewer, same-day, PDF, browser-local/no-data-leaves, instant, or "in seconds" claims.
- Local route returned HTTP `200`; local Playwright screenshots captured desktop and mobile. Local console showed only expected `501` POST noise from the static server.
- Pushed `cb5b791` to `main`; Git-connected Vercel production deployed the page.
- Live checks passed:
  - `https://writemyformula.com/excel-formula-not-copying-down/` HTTP `200`
  - homepage HTTP `200` and includes `/excel-formula-not-copying-down/`
  - sitemap HTTP `200` and includes the route
  - Stripe checkout URL HTTP `200`
  - live page contains canonical `https://writemyformula.com/excel-formula-not-copying-down/`
  - live desktop/mobile Playwright checks found expected H1, `6` checkout links, and `0` console/page issues
- IndexNow accepted page/home/sitemap with HTTP `200`.

## Non-Actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `$35.93`.
