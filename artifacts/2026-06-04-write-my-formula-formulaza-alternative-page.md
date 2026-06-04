# Write My Formula FormulaZa Alternative Page - 2026-06-04

## Result

Shipped `https://writemyformula.com/formulaza-alternative/` as a no-spend comparison-intent page for users comparing FormulaZa-style formula tools but needing one Excel or Google Sheets formula, explanation, or repair.

Commit: `84da590 Add FormulaZa alternative page`

Screenshots and browser summary:
- `workspace/sheetpilot-workbench/output/playwright/formulaza-alternative-live/live-desktop.png`
- `workspace/sheetpilot-workbench/output/playwright/formulaza-alternative-live/live-mobile.png`
- `workspace/sheetpilot-workbench/output/playwright/formulaza-alternative-live/summary.json`

## Evidence

Live research validated FormulaZa as an active Excel and Google Sheets formula tool with Generate, Explain, and Fix modes; 50 free formulas per day; 16-language support; formula history; saved formulas; formula library / formula of the day; daily quiz / interview prep style learning surfaces; Excel-to-Sheets translator; AI Excel chat; recommended resources; and contact/legal pages updated in May 2026.

Broader category evidence came from active AI spreadsheet/formula tools including SheetGPT, ExpressSheet, Sheet Formula AI, AI Formula Generator, FormulaGenius, and current Google Gemini-in-Sheets formula-help coverage.

Sources:
- FormulaZa: https://formulaza.com/
- SheetGPT: https://sheetgpt.pro/
- ExpressSheet: https://www.expresssheet.com/
- Sheet Formula AI: https://sheetformulaai.com/
- AI Formula Generator: https://www.aiformulagenerator.com/
- FormulaGenius: https://formulagenius.vercel.app/
- TechRadar on Gemini formula help in Sheets: https://www.techradar.com/pro/forget-microsoft-excel-pain-google-sheets-can-now-tell-you-exactly-why-your-formulas-failed

## Copy Boundaries

Luke reviewed copy direction and advised a fit-based page that does not claim parity or superiority. Final public copy stayed bounded to Write My Formula's visible one-formula workflow and routed users back to broader tools when they need FormulaZa's learning/history/translator/chat/resource surface.

Avoided claims:
- replacement or better-than language
- official FormulaZa relationship, partner, or affiliation
- accuracy, speed, guarantee, instant, perfect-formula, automatic-fix, one-click, exact-cause claims
- upload, whole-workbook, workbook-audit, human-review, same-day/PDF, privacy-superiority, or data-never-leaves claims

## Files Changed

- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
- `workspace/sheetpilot-workbench/formulaza-alternative/index.html`
- regenerated static route pages because the homepage card grid is embedded in generated pages
- `workspace/sheetpilot-workbench/index.html`
- `workspace/sheetpilot-workbench/sitemap.xml`
- `workspace/sheetpilot-workbench/tests/content.test.js`
- `workspace/sheetpilot-workbench/luke-formulaza-alternative-page.md`

## Verification

- `npm run build:seo && npm test` passed `120/120`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no prohibited FormulaZa comparison claims; hits for words like `task` and `run` were existing product UI language, such as "Job to do" and "formula runs."
- Live `https://writemyformula.com/formulaza-alternative/` returned HTTP `200`.
- Live homepage includes `/formulaza-alternative/`.
- Live sitemap includes `https://writemyformula.com/formulaza-alternative/`.
- Live Stripe checkout returned HTTP `200`.
- Live Chromium desktop and mobile checks returned:
  - HTTP `200`
  - expected title, H1, and canonical
  - `6` checkout links
  - required FormulaZa boundary copy present
  - no horizontal overflow
  - `0` console warnings/errors
  - `0` page errors
- IndexNow submission returned HTTP `200`.

## Permission / Spend

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA submit, public post, bulk send, destructive production change, or spend occurred.

Open gates remain:
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

Current cash balance remains `-$24.07`.
