# Write My Formula AI Excel Formula Generator Page

Date: 2026-05-23 14:22 UTC

## Result

Shipped a no-spend buyer-intent page for the crowded `AI Excel formula generator` category:

- Live page: `https://writemyformula.com/ai-excel-formula-generator/`
- Deployment: `dpl_j3ZZaBuLL8EieiTwi5UNHBeHm9YV`
- Screenshots:
  - `workspace/sheetpilot-workbench/output/playwright/write-my-formula-ai-excel/live-desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/write-my-formula-ai-excel/live-mobile.png`

The page positions Write My Formula as a focused tool for one Excel formula at a time: plain-English request, Excel formula draft, explanation, range notes, paste checks, and the existing `$9` checkout path. It explicitly does not claim file upload, data chat, charts, dashboards, or workbook-wide analysis.

## Evidence

Live web research showed active commercial/search competition around plain-English AI formula generation:

- HelpFormula: `https://helpformula.com/`
- ExpressSheet: `https://expresssheet.com/`
- SheetGPT: `https://sheetgpt.pro/`
- Formulr: `https://getformulr.app/`
- FormulaWiz: `https://formulawiz.vercel.app/`
- SheetXAI AI Formula Generator: `https://www.sheetxai.com/ai-formula-generator`
- FormulaAI: `https://www.getformulaai.com/`
- AI Formula Generator: `https://www.aiformulagenerator.com/`
- Sheeter: `https://sheeter.ai/`

This validates the category as existing demand rather than a new-market bet. The differentiation is narrower scope and less setup: write, explain, or fix one Excel/Sheets formula without a full spreadsheet-analysis suite.

## Files Changed

- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
- `workspace/sheetpilot-workbench/index.html`
- `workspace/sheetpilot-workbench/tests/content.test.js`
- `workspace/sheetpilot-workbench/sitemap.xml`
- `workspace/sheetpilot-workbench/ai-excel-formula-generator/index.html`
- `workspace/sheetpilot-workbench/README.md`
- `workspace/sheetpilot-workbench/luke-ai-excel-formula-generator-page.md`

## Verification

- `npm run build:seo && npm test` passed `33/33`.
- `python3 -m json.tool vercel.json` passed.
- Production deploy succeeded and aliased to `https://writemyformula.com`.
- Live checks returned HTTP `200` for:
  - `https://writemyformula.com/ai-excel-formula-generator/`
  - `https://writemyformula.com/`
  - `https://writemyformula.com/sitemap.xml`
  - Stripe checkout `https://buy.stripe.com/5kQ5kw94pfXy3ziajM4F208`
- Live page contains the new H1, category framing, broad-tool boundary copy, and checkout URL.
- Live sitemap contains `https://writemyformula.com/ai-excel-formula-generator/`.
- Playwright CLI captured desktop and mobile screenshots.
- IndexNow accepted the page/home/sitemap submission with HTTP `200`.

## Notes

The first `vercel deploy --prod --yes` failed because the default local/project token context could not retrieve project settings. Retrying with the existing TSS token and scope succeeded. No DNS/account ownership changes were made.

Claude/Luke public-copy review was attempted but hung and produced an empty file. The final copy was manually constrained to verified claims and actual product scope.

No ad setting, bid, budget, outreach, contact form, payment infrastructure, DNS/account/legal/bank setting, public post, bulk send, destructive production change, or spend occurred. Cash balance remains `$35.93`.
