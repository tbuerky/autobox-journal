# Write My Formula Excel Formulator Alternative Page

Date: 2026-06-09 14:24 UTC

## Task

Shipped `https://writemyformula.com/excel-formulator-alternative/` as a no-spend comparison-intent page for users comparing Excel Formulator but needing one Excel or Google Sheets formula, explanation, or repair in a browser tab rather than a monthly Excel/Sheets/Airtable formula app.

## Why this task

Paid-search rollback/export and Fluent Forms manual reCAPTCHA remain owner-gated, and outreach categories remain wait-locked unless a relevant prospect replies. A new comparison-intent page creates another indexed sales surface without spend, payment infrastructure changes, public posting, bulk outreach, or account changes.

## Live evidence

- Excel Formulator public page: `https://excelformulator.com/`
  - Positions Excel Formulator as an AI-powered spreadsheet assistant.
  - Says users can convert simple text prompts into Excel, Google Sheets, and Airtable formulas.
  - Describes plain-English explanations for complex or simple formulas.
  - Says it is optimized for Microsoft Excel, Google Sheets, and Airtable.
  - Lists a free Starter plan with `7` formulas per month and basic email support.
  - Lists Pro at `$5.99/month` with unlimited formulas, priority email support, and early access to features.
  - Lists annual Pro at `$4.49/month` when paid annually.

Search result context also showed active competing spreadsheet formula-generator surfaces including FormulaWiz, SheetSolver AI, SheetGPT, Formulr, ExcelGPT, ExpressSheet, and ExcelFormula Pro.

Luke reviewed the buyer-facing direction in `workspace/sheetpilot-workbench/luke-excel-formulator-alternative.md`. The final page uses comparison/fit framing, explicitly notes Write My Formula does not cover Airtable, and avoids accuracy, speed, safety-superiority, unlimited, leading-alternative, official-affiliation, and competitor-attack claims.

## What changed

- Added `excel-formulator-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added a homepage comparison card in `workspace/sheetpilot-workbench/index.html`.
- Regenerated `workspace/sheetpilot-workbench/excel-formulator-alternative/index.html`, static SEO pages, and `sitemap.xml`.
- Added focused assertions to `workspace/sheetpilot-workbench/tests/content.test.js`.
- Saved local and live screenshots under:
  - `workspace/sheetpilot-workbench/output/playwright/excel-formulator-alternative-local/`
  - `workspace/sheetpilot-workbench/output/playwright/excel-formulator-alternative-live/`
- Committed and pushed nested app commit `0697d939 Add Excel Formulator alternative page`.

## Verification

- `npm run build:seo` passed.
- `npm test` passed `161/161`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Targeted public-copy scan found no internal/process language or blocked Excel Formulator claims; `placeholder` hits were normal form placeholders.
- Local desktop/mobile Chromium route checks passed: HTTP `200`, correct title/H1/canonical, six checkout links, Excel Formulator detail copy present, Airtable boundary copy present, no horizontal overflow, and no page errors. The only console noise was expected local static-server `POST` 501.
- Production route returned HTTP `200`.
- Live homepage contains `/excel-formulator-alternative/`.
- Live sitemap contains `https://writemyformula.com/excel-formulator-alternative/`.
- Actual live Stripe checkout returned HTTP `200`.
- Live desktop/mobile Chromium checks passed: route HTTP `200`, correct title/H1/canonical, six checkout links, Excel Formulator detail copy present, Airtable boundary copy present, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow accepted route/home/sitemap submission with HTTP `200`.

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
