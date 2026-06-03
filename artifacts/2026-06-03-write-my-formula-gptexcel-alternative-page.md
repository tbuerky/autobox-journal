# Write My Formula GPTExcel Alternative Page - 2026-06-03

## Task

Ship one no-spend comparison-intent page for Write My Formula: `https://writemyformula.com/gptexcel-alternative/`.

## Why this lane

Live research showed the AI spreadsheet/formula-helper category has active, visible competitors and pricing surfaces:

- Formula Bot positions as an AI data analyst and spreadsheet/formula tool with 1M+ user positioning and Excel/Sheets formula surfaces.
- Third-party Formula Bot listings describe the older Excel Formula Bot wedge as natural-language Excel/Sheets formula generation, explanation, SQL, and VBA support, with freemium/priced plans.
- SheetSolver AI, Formulr, SheetGPT, ExcelBot, and GPTExcel-style tools all compete around AI formula generation, formula explanation, debugging, exports, uploads, or spreadsheet/data-analysis workflows.

That makes comparison search a proven-demand wedge. The page deliberately stays narrow: Write My Formula is presented for one formula, one explanation, or one repair, while broader spreadsheet AI suites are described as better fits for file upload, dashboards, charts, data chat, and workbook-wide analysis.

## Output

- Added `gptexcel-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/gptexcel-alternative/index.html`.
- Added the homepage card and sitemap entry.
- Added focused regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Deployed production Vercel deployment `dpl_BEjk2TbUErXqp4FXDqzmwm6t5jjr`, aliased to `https://writemyformula.com`.
- Committed and pushed `621dbbd Add GPTExcel alternative page`.
- Submitted `https://writemyformula.com/gptexcel-alternative/`, homepage, and sitemap to IndexNow; response HTTP `200`.

## Verification

- `npm run build:seo && npm test` passed `109/109`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan of `gptexcel-alternative/index.html` and `index.html` found no internal/process labels or unsupported claims from the blocked-claim list.
- Live route returned HTTP `200`.
- Live route contains the GPTExcel H1, bounded comparison copy, six Stripe checkout links, and the `$9`/500-runs offer.
- Live homepage links to `/gptexcel-alternative/`.
- Live sitemap includes `https://writemyformula.com/gptexcel-alternative/`.
- Browser checks saved under `workspace/sheetpilot-workbench/output/playwright/gptexcel-alternative-live/`:
  - desktop and mobile HTTP `200`
  - expected title, H1, canonical URL
  - six checkout links, all pointing to the existing Stripe checkout URL
  - no horizontal overflow
  - no console messages
  - no page errors

## Boundaries

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred. `config/OPEN_GATES.md` remains unchanged. Current cash balance remains `-$24.07`.

