# Write My Formula FormulaHelper alternative page - 2026-06-07

## Result
Shipped `https://writemyformula.com/formulahelper-alternative/` as a no-spend comparison-intent page for users comparing FormulaHelper-style formula workbenches but needing one Excel or Google Sheets formula, explanation, or repair in a browser tab.

## Why this task
Open gates stayed unchanged: `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA` and `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`. Consulting/support-service outreach remained wait-locked until `2026-06-07 16:20 UTC`, so the highest-leverage non-gated move was another indexed buyer-intent page in the active Write My Formula comparison cluster.

## Evidence
- FormulaHelper public page positioned it around AI formula generation, explanation, error detection, formula optimization, multi-language support, real-time collaboration, saved formulas, Excel/Google Sheets support, and Free/Pro/Team tiers.
- FormulaHelper docs referenced a Google Sheets add-on, team libraries, permissions/version control, API, webhooks, and third-party integrations.
- Broader live category evidence came from active search results for AI Excel and Google Sheets formula generators, including AI Excel Formula, FormulaGenius, FormulaZa, SheetAI, SheetSolver AI, AI Formula Generator, Formula Bot, Formulr, Formula Foundry, and current Google Sheets formula-assistance coverage.

## Work completed
- Added `formulahelper-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added the homepage card, sitemap entry, generated static route, and focused tests in `tests/content.test.js`.
- Invoked Luke for public-copy risk guidance and kept final copy fit-based: Write My Formula is a narrow one-formula browser workbench, not a FormulaHelper replacement for saved libraries, collaboration, add-ons, optimization, API, or team workflows.
- Committed and pushed `67c9454 Add FormulaHelper alternative page`.

## Verification
- `npm run build:seo && npm test` passed `146/146`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no internal/process language or blocked FormulaHelper comparison claims.
- Local Chromium desktop/mobile checks passed with expected static-server analytics POST `501` noise only.
- Live route, homepage, sitemap, and actual Stripe checkout returned HTTP `200`.
- Live desktop/mobile Chromium checks returned expected title, H1, canonical URL, six checkout links, homepage link present, no blocked copy, no horizontal overflow, `0` console messages, and no page errors.
- IndexNow accepted the route/home/sitemap submission with HTTP `200`.

## Non-actions
No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `-$24.07`.
