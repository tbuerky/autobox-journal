# Write My Formula AI Formula Generator Alternative Page

Date: 2026-06-04 12:23 UTC

## Outcome
Shipped `https://writemyformula.com/ai-formula-generator-alternative/` as a no-spend comparison-intent page for users comparing AI Formula Generator-style tools but needing one Excel or Google Sheets formula, explanation, or repair rather than SQL, CSV/Excel file-context, bulk generation, VBA, Apps Script, templates, or conversational formula workflow.

Commit: `c93e857 Add AI Formula Generator alternative page`

## Evidence
- Live research validated `aiformulagenerator.com` as an active AI formula-generator surface for Excel, Google Sheets, and SQL, with public positioning around Excel functions, Google Sheets functions, SQL query generation, CSV/Excel/PDF context, formula explanation/debugging, templates, bulk generation, VBA, Apps Script, Starter `$9/month`, and Pro `$19/month`.
- Broader category evidence came from Formula Bot official docs, Formula Bot's Google Sheets formula page, SheetSolver AI, and current AI spreadsheet-tool roundups mentioning Formula Bot / GPTExcel / ExcelMaster-style formula products.
- Luke reviewed the copy direction; final public copy stayed fit-based and avoided better-than/replacement, official-affiliation, accuracy, speed, guarantee, instant/perfect-formula, upload/whole-workbook/exact-cause/human-review/same-day/PDF/privacy-superiority, and competitor-attack claims.

Sources used:
- `https://www.aiformulagenerator.com/`
- `https://www.formulabot.com/docs/tools/formula-generator`
- `https://www.formulabot.com/google-sheets-formula-generator`
- `https://www.sheetsolverai.com/`

## Changes
- Added `ai-formula-generator-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/ai-formula-generator-alternative/index.html`.
- Added a homepage card and sitemap entry.
- Added focused regression tests to `workspace/sheetpilot-workbench/tests/content.test.js`.
- Regenerated all static SEO pages because the homepage card grid is embedded in each generated page.

## Verification
- `npm run build:seo && npm test` passed `119/119`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan passed for the new route and homepage card.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live desktop and mobile Chromium checks found expected title, H1, canonical URL, six checkout links, required boundary copy, no horizontal overflow, no console messages, and no page errors.
- IndexNow returned HTTP `200`.

## Non-actions
No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred. Current budget balance remains `-$24.07`.
