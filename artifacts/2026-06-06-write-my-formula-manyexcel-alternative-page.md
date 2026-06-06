# Write My Formula ManyExcel Alternative Page

Date: 2026-06-06 18:22 UTC

## Task
Ship one no-spend revenue motion for the active Write My Formula lane while paid-search control and Fluent Forms manual reCAPTCHA remain gated.

## Output
Shipped `https://writemyformula.com/manyexcel-alternative/` as a comparison-intent page for users comparing ManyExcel-style formula, regex, script, chart, and Excel-file tools but needing one Excel or Google Sheets formula, explanation, or repair they can inspect in a browser tab.

Commit: `a388098 Add ManyExcel alternative page`

Changed product files under `workspace/sheetpilot-workbench/`:
- `scripts/build-seo-pages.mjs`
- `tests/content.test.js`
- `index.html`
- generated static pages and `sitemap.xml`
- new `manyexcel-alternative/index.html`
- `luke-manyexcel-alternative.md`

## Live Research
ManyExcel was live on 2026-06-06. Its public homepage presented:
- Excel and Google Sheets AI formula generation.
- Regex pattern generation.
- VBA and Google Apps Script generation.
- Charts and Excel-file interaction.
- Free Plan at `$0/month` with 5 formula generations, 5 regex generations, 5 script generations, and unlimited explanations.
- Pro Plan at `$2.50/month` with unlimited formula, regex, and script generation/explanations plus priority support.

Broader active category evidence came from current formula AI tools surfaced in live search, including SheetGPT, Excelly-AI, FormulaGenius, FormulaWiz, Smart Excel, FormulaZa, Formula Workspace, and Formularizer.

## Copy Guardrails
Luke reviewed the copy direction. Final copy intentionally stayed fit-based:
- Use Write My Formula for one formula, one explanation, or one repair.
- Use ManyExcel or a similar broader tool for regex, VBA, Apps Script, charts, Excel-file interaction, or low-cost unlimited multi-tool generation.

The public page avoids unsupported replacement, better-than, official-affiliation, partner, speed, accuracy, guarantee, perfect/automatic-fix, privacy-superiority, upload/workbook-audit, exact-cause, human-review, same-day/PDF, cheaper-than, price-superiority, and competitor-attack claims.

## Verification
- `npm run build:seo && npm test` passed `139/139`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy/overclaim scan found no ManyExcel-specific blocked claims.
- Commit `a388098` pushed to GitHub; Vercel GitHub integration served the new route live.
- Live `https://writemyformula.com/manyexcel-alternative/` returned HTTP `200` and contained the expected title, canonical, H1, ManyExcel boundary copy, `$0/month` Free plan evidence, and `$2.50/month` Pro plan evidence.
- Live homepage returned HTTP `200` and links to `/manyexcel-alternative/`.
- Live sitemap returned HTTP `200` and contains `https://writemyformula.com/manyexcel-alternative/`.
- Live Stripe checkout returned HTTP `200`.
- Live Chromium desktop and mobile checks passed with `0` console messages, `0` page errors, no horizontal overflow, and `6` checkout links all pointing to the active Stripe checkout.
- Screenshots and browser-check JSON saved under `workspace/sheetpilot-workbench/output/playwright/manyexcel-alternative-live/`.
- IndexNow accepted page/home/sitemap submission with HTTP `202`.

## Gates and Spend
`config/OPEN_GATES.md` remains unchanged:
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.

## Next
Continue respecting the paid-search and reCAPTCHA gates. Watch for Write My Formula replies. Consulting/support-service outreach remains wait-locked until `2026-06-07 16:20 UTC` unless GetSpreadsheet, Easy Excel Answers, SpreadsheetClass, Excelerate Solutions, or Excel Spreadsheet Service replies first. If no reply or gate clears, favor another distinct buyer-intent page or researched one-to-one outreach only after the relevant wait window clears.
