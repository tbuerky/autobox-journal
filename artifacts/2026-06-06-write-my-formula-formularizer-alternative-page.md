# Write My Formula Formularizer Alternative Page

Date: 2026-06-06 16:26 UTC

## Result

Shipped a new no-spend comparison-intent page:

- Live URL: https://writemyformula.com/formularizer-alternative/
- Commit: `f5d9079 Add Formularizer alternative page`
- Screenshots:
  - `workspace/sheetpilot-workbench/output/playwright/formularizer-alternative-live/desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/formularizer-alternative-live/mobile.png`

The page targets users comparing Formularizer-style spreadsheet assistant suites, but whose immediate problem is still one Excel or Google Sheets formula, explanation, or repair.

## Live Evidence Used

- Formularizer live homepage: https://formularizer.com/
  - Current positioning: AI assistant for spreadsheets.
  - Public feature evidence from search/opened page: Formula Assistant for Excel and Google Sheets generation/explanation, SQL Assistant, Regex Assistant, Script Assistant for Excel VBA and Google Apps Script, mode/platform selection, sample-data tip, 3 free credits to try, and 50 free credits after signup.
- Formulr live homepage: https://getformulr.app/
  - Broader active category evidence: Excel and Google Sheets formula generation, explanation, debugging, Gemini 2.5 Flash positioning, free monthly quotas, Pro pricing, and browser extension direction.
- Microsoft AppSource FormulAI listing: https://marketplace.microsoft.com/en-us/product/office/wa200005333
  - Broader category evidence: spreadsheet AI assistant add-ins with formula explanation, natural-language formula suggestions, data querying, and data simulation.

## Copy Direction

Luke reviewed the copy direction. Final public copy stayed scope-based:

- Use Write My Formula when the job is one Excel or Google Sheets formula, explanation, or repair, one formula at a time.
- Use Formularizer or a similar assistant suite when the work spans formulas, SQL queries, regex, Excel VBA, Google Apps Script, sample-data credit workflows, or several assistant types.

Avoided unsupported claims: replacement, better-than, official affiliation, partner, speed, accuracy, guarantee, instant/perfect formula, automatic fix, privacy superiority, upload/workbook audit, exact cause, human review, same-day/PDF, and competitor attacks.

## Files Changed

- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
- `workspace/sheetpilot-workbench/index.html`
- `workspace/sheetpilot-workbench/formularizer-alternative/index.html`
- generated static SEO pages
- `workspace/sheetpilot-workbench/sitemap.xml`
- `workspace/sheetpilot-workbench/tests/content.test.js`

## Verification

- `npm run build:seo && npm test` passed `138/138`.
- `python3 -m json.tool vercel.json` passed.
- Targeted public-copy scan found no blocked Formularizer claims or internal/process language in the new route/homepage card.
- Local Chromium desktop/mobile checks:
  - HTTP `200`
  - expected title, H1, canonical URL
  - `6` checkout links
  - Formularizer evidence and fit boundary visible
  - no horizontal overflow
  - no page errors
  - expected static-server `POST /api/*` `501` noise only
- Production checks:
  - `https://writemyformula.com/formularizer-alternative/` HTTP `200`
  - homepage HTTP `200` and links to `/formularizer-alternative/`
  - sitemap HTTP `200` and includes the new route
  - live Stripe checkout HTTP `200`
  - production Chromium desktop/mobile checks returned `0` console messages, `0` page errors, no horizontal overflow, expected H1/title/canonical, `6` checkout links, and Formularizer evidence visible.
- IndexNow submission for route/home/sitemap returned HTTP `200` after correcting an initial local key-selection mistake.

## Boundaries

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
