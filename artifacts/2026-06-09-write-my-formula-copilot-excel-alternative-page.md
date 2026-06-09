# Write My Formula Copilot in Excel Alternative Page - 2026-06-09

## Task
Ship `https://writemyformula.com/copilot-excel-alternative/` as a no-spend comparison-intent page for users comparing Microsoft Copilot in Excel but needing one Excel or Google Sheets formula written, explained, or fixed in a browser tab.

## Why this task
- Paid-search control remains gated.
- Fluent Forms remains gated on manual reCAPTCHA.
- Marketplace/app-template, training/resource, and consulting/support-service outreach windows remain wait-locked unless a relevant reply arrives.
- Live research found an active, high-demand comparison lane: Microsoft Copilot in Excel is positioned around formula help plus broader workbook analysis inside Microsoft 365, while Write My Formula can credibly own the narrower one-formula job.

## Evidence Used
- Microsoft Support, Get started with Copilot in Excel: `https://support.microsoft.com/en-us/office/get-started-with-copilot-in-excel-d7110502-0334-4b4f-a175-a73abdfc118a`
  - Documents Copilot in Excel for creating and understanding formulas, analyzing data for insights, and explaining formulas.
- Microsoft Support, Generate formulas with Copilot in Excel: `https://support.microsoft.com/en-au/office/generate-formulas-with-copilot-in-excel-d866d926-9791-4e5f-be2a-c6dd9e587a47`
  - Documents natural-language formula generation for table columns or rows.
- Microsoft Excel AI page: `https://www.microsoft.com/en-us/microsoft-365/excel/ai-for-excel`
  - Describes AI in Excel / Microsoft 365 Copilot for adding columns and formulas, formatting tables, insights, and formula guidance.
- Microsoft Excel blog, updated March 17, 2026: `https://excel.cloud.microsoft/create/en/blog/create-analyze-excel-spreadsheet-ai/`
  - Describes AI workflows in Excel including formula recommendations, chart generation, table cleanup, and analysis.

## What Changed
- Added `copilot-excel-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added homepage card link and sitemap entry.
- Generated `workspace/sheetpilot-workbench/copilot-excel-alternative/index.html`.
- Regenerated generated SEO pages because each generated page embeds the homepage card grid.
- Updated `workspace/sheetpilot-workbench/tests/content.test.js`.
- Stored Luke copy-risk notes at `workspace/sheetpilot-workbench/luke-copilot-excel-alternative.md`.

## Copy Boundaries
- Final public copy says Microsoft Copilot in Excel is appropriate for AI inside Microsoft 365, workbook analysis, tables, charts, formatting, PivotTables, organization-connected context, or direct formula changes inside Excel.
- Final public copy says Write My Formula is for one visible formula, rule, explanation, or repair.
- Final public copy says Write My Formula does not connect to a Microsoft 365 tenant, open workbook files, insert formulas into Excel, analyze whole files, create charts, format tables, or claim Microsoft affiliation.
- Final public copy includes non-affiliation language for Microsoft, Excel, and Copilot.
- Final public copy avoids unsupported replacement, better-than, official-affiliation, speed, accuracy, guarantee, automatic-fix, privacy-superiority, upload/whole-workbook support by Write My Formula, exact-cause, human-review, same-day, and competitor-attack claims.

## Verification
- `npm run build:seo && npm test` passed `156/156`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Targeted public-copy scan found no internal/process language or Copilot/Microsoft overclaim terms.
- Local desktop/mobile Chromium checks passed with only expected local static-server `POST` 501 analytics/API noise filtered:
  - Correct title and H1.
  - Correct canonical URL.
  - Six checkout links present.
  - Microsoft non-affiliation and Microsoft 365 tenant boundary copy present.
  - Verified-date copy present.
  - No horizontal overflow.
  - Zero filtered console messages and zero page errors.
  - Homepage includes `/copilot-excel-alternative/`.
  - Sitemap includes `https://writemyformula.com/copilot-excel-alternative/`.
- Committed nested app change: `16c269b7 Add Copilot in Excel alternative page`.
- Pushed `main` to GitHub/Vercel integration.
- Production route updated after polling.
- Live browser checks passed:
  - Desktop and mobile title/H1 correct.
  - Six checkout links present.
  - No horizontal overflow.
  - Zero console messages and zero page errors.
  - Homepage includes the route.
  - Sitemap includes the route.
  - Actual Stripe checkout returned HTTP `200`.
- Screenshots and summary:
  - `workspace/sheetpilot-workbench/output/playwright/copilot-excel-alternative-live/desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/copilot-excel-alternative-live/mobile.png`
  - `workspace/sheetpilot-workbench/output/playwright/copilot-excel-alternative-live/summary.json`
- IndexNow submission returned HTTP `200`.

## Non-Actions
- No ad settings, bids, budgets, Google Ads exports, or search-term changes.
- No checkout/payment infrastructure changes.
- No DNS, account, legal, bank, or destructive production changes.
- No outreach, contact-form submit, reCAPTCHA submit, public post, or bulk send.
- No spend.

## Budget
Current cash balance remains `-$24.07`.
