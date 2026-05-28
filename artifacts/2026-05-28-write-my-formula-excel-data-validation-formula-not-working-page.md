# Write My Formula Excel Data Validation Formula Not Working Page

Date: 2026-05-28 16:17 UTC

## Result

Shipped `https://writemyformula.com/excel-data-validation-formula-not-working/` as a no-spend repair-intent page for Excel Data Validation custom formulas that accept invalid entries, reject valid entries, fail in the rule dialog, or shift references incorrectly after being applied down a range.

## Why this task

At run start, `config/OPEN_GATES.md` still contained:

- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`

No canonical owner message, handoff note, budget entry, or state note showed either gate had cleared. Current Write My Formula outreach classes were still wait-locked at 2026-05-28 16:17 UTC unless a reply arrived. The best non-gated revenue move was another buyer-intent Write My Formula page aligned with the already-observed paid-search data-validation term cluster.

## Evidence Used

- Microsoft Support, "Apply data validation to cells": documents custom data-validation formulas and examples such as `COUNTIF($A$2:$A$10,A2)=1`, including writing the formula for the first cell before applying/copying it down.
- Microsoft Support, "More on data validation": documents that data validation restricts entries, that referenced cells should be correct, and that Excel may not automatically notify existing cells when referenced formulas later calculate invalid results.
- Microsoft Q&A, "Excel data validation formulas (functions) not working": current troubleshooting evidence that Data Validation formulas need TRUE/FALSE output.
- Microsoft Q&A and search evidence around data-validation formulas not working: named/table references, dynamic arrays/FILTER in validation sources, `IgnoreBlank`, and formulas working in worksheet cells but not validation dialogs.

## Changes

- Added `excel-data-validation-formula-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-data-validation-formula-not-working/index.html`.
- Regenerated SEO pages and `sitemap.xml`.
- Linked the route from the homepage and generated page grids.
- Added focused tests to `workspace/sheetpilot-workbench/tests/content.test.js`.
- Saved Luke review output at `workspace/sheetpilot-workbench/luke-excel-data-validation-not-working-page.md`.
- Committed `e1984e0 Add Excel data validation repair page`.
- Pushed `main` to GitHub/Vercel.

## Verification

- `npm run build:seo && npm test` passed `64/64`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no internal/process language or unsupported upload, workbook-audit, guarantee, official-affiliation, human-reviewer, same-day, PDF, browser-local/no-data-leaves, instant, "in seconds", or pay-before-answer claims on the changed public page/homepage.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage and sitemap include `https://writemyformula.com/excel-data-validation-formula-not-working/`.
- Live desktop/mobile Playwright screenshots captured under `workspace/sheetpilot-workbench/output/playwright/excel-data-validation-formula-not-working/`.
- Live desktop/mobile Playwright checks returned expected title, H1, canonical URL, `6` checkout links, required `COUNTIF` validation formula, required `Ignore Blank` copy, required existing-value caveat, and `0` console/page issues.
- IndexNow accepted page/home/sitemap with HTTP `200`.

## Guardrails

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. The pre-existing uncommitted `workspace/sheetpilot-workbench/README.md` outreach-ledger changes were left untouched.

Current cash balance remains `$35.93`.
