# Write My Formula Sheeter Alternative Page - 2026-06-04

## Result
Shipped `https://writemyformula.com/sheeter-alternative/` as a no-spend comparison-intent page for users comparing Sheeter-style formula generators but needing one Excel or Google Sheets formula, explanation, or repair.

Commit: `366fa4e Add Sheeter alternative page`

## Live Evidence
- Sheeter.ai is active and positions itself as an Excel formula generator that accepts a query, generates a formula for Excel and Google Sheets, lets users copy the formula, and points users toward a Sheeter.ai add-on. It also showed lifetime plans starting at `$69.99` during this run. Source: https://sheeter.ai/
- FormulaBerry validates broader category demand with Excel and Google Sheets formula generation, explanation, corrections, multilingual support, and a spreadsheet AI bot framing. Source: https://www.formulaberry.com/
- ExcelFormula Pro validates paid category demand with two free trial formulas and a `$15/month` Pro plan. Source: https://excelformula.pro/
- FormulaPilot validates free tool and library/checker demand for Excel and Google Sheets formula suggestions. Source: https://formulapilot.com/
- SheetGPT validates the broader spreadsheet AI category with formulas, explanations, chat with data, OCR, charts, data analysis, and paid/free plan positioning. Source: https://sheetgpt.pro/

## Copy Direction
Luke reviewed the buyer-facing comparison angle. Final copy stayed fit-based: Write My Formula is the lighter path for one formula-sized problem; Sheeter or similar tools are better fits when the user wants an add-on, saved formula workspace, query examples, or a lifetime-plan path.

The page avoids replacement, better-than, official-affiliation, partner, accuracy, speed, guarantee, instant/perfect-formula, privacy-superiority, upload, whole-workbook, exact-cause, human-review, same-day/PDF, and lifetime-deal claims.

## Changes
- Added `sheeter-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/sheeter-alternative/index.html`.
- Added the homepage card and sitemap entry.
- Regenerated all static SEO pages because the homepage card grid is embedded into generated pages.
- Added focused tests for homepage/sitemap coverage, checkout links, and overclaim avoidance.

## Verification
- `npm run build:seo && npm test` passed `118/118`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked internal/process language or unsupported comparison claims in the new route/homepage.
- Local desktop/mobile Chromium checks captured screenshots under `workspace/sheetpilot-workbench/output/playwright/sheeter-alternative-local/`; static-server-only `POST /api/*` `501` noise was expected.
- Live route/home/sitemap/Stripe checkout returned HTTP `200`.
- Live desktop/mobile Chromium checks captured screenshots under `workspace/sheetpilot-workbench/output/playwright/sheeter-alternative-live/`; both had expected title, H1, canonical URL, six checkout links, homepage route link, boundary copy, no horizontal overflow, no console messages, and no page errors.
- IndexNow returned HTTP `200` for the new route, homepage, and sitemap.

## Gates, Spend, And Boundaries
Open gates remain:
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance: `-$24.07`.
