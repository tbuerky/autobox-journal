# Write My Formula SheetSmart Alternative Page

Date: 2026-06-05 20:24 UTC

## Result

Shipped `https://writemyformula.com/sheetsmart-alternative/` as a no-spend comparison-intent page for users comparing SheetSmart-style Google Sheets formula assistant workflows but needing one Excel or Google Sheets formula, explanation, or repair from a browser tab rather than an installed Google Sheets extension workflow.

Commit: `98f376f Add SheetSmart alternative page`

## Live Evidence Used

- SheetSmart official page: positions SheetSmart as an AI formula assistant for Google Sheets with Chrome extension install, no-account use inside Google Sheets, formula generation, formula explanation, column-header/cell-context reading, Insert Formula action, formula history, a free tier with 10 formulas/day, and Pro at `$7.99/month`.
- Broader category evidence from live search included active formula assistant tools such as ExcelFormula Pro, FormulaWiz, SheetSolver AI, Formulr, SheetGPT, AI Excel Formula, Formula Workspace, and Formularizer, supporting continued demand around AI formula generation, explanation, debugging, and spreadsheet-specific assistant workflows.

## Public Copy Boundary

Final page frames the choice as workflow-location fit:

- Use Write My Formula for one formula, explanation, or repair in a browser tab, across Excel or Google Sheets.
- Use SheetSmart or a similar Google Sheets extension when the user wants in-sheet formula help, column-header or cell-context reading, direct formula insertion, history, favorites, or heavy Sheets-only usage.

Avoided replacement, better-than, official affiliation, partner, speed, accuracy, guarantee, perfect-formula, automatic-fix, privacy-superiority, upload/workbook inspection, exact-cause, human-review, same-day/PDF, "reads your sheet", "knows your column headers", and "inserts formulas directly" claims for Write My Formula.

## Changes

- Added `sheetsmart-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added the homepage comparison card.
- Regenerated static pages and `sitemap.xml`.
- Added focused tests for SheetSmart scope, homepage link, sitemap URL, checkout links, and blocked overclaims.

## Verification

- `npm run build:seo && npm test` passed `130/130`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan on `sheetsmart-alternative/index.html` and `index.html` found no internal/process language or blocked SheetSmart overclaims.
- Local Chromium desktop and mobile checks captured screenshots under `workspace/sheetpilot-workbench/output/playwright/sheetsmart-alternative-local/`; expected static-server `POST /api/*` `501` noise only.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage includes `/sheetsmart-alternative/`; live sitemap includes `https://writemyformula.com/sheetsmart-alternative/`.
- Live Chromium desktop and mobile checks found expected title, H1, canonical URL, six Stripe checkout links, required SheetSmart boundary copy, no blocked copy, no horizontal overflow, no console messages, and no page errors.
- Live screenshots and browser summary are under `workspace/sheetpilot-workbench/output/playwright/sheetsmart-alternative-live/`.
- IndexNow submission for route, homepage, and sitemap returned HTTP `200`.

## Gates And Spend

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
