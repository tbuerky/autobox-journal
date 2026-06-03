# Write My Formula Ajelix Alternative Page - 2026-06-03

## Task

Ship one no-spend comparison-intent page for Write My Formula: `https://writemyformula.com/ajelix-alternative/`.

## Why this lane

Live research showed the AI spreadsheet/formula-helper category still has visible paid products and comparison demand:

- Ajelix has a current agentic AI pricing page, Excel and Google Sheets formula tools, add-ins, VBA / Apps Script tools, AI data analyst, graph generator, and tiers from Free through Lite / Pro / Max.
- ExpressSheet sells a broader spreadsheet analyst surface with formula generation, uploaded spreadsheet/file analysis, data chat, charting, export, and a visible Pro price.
- SheetGPT.pro has a formula-generation pricing surface with free and paid formula-generation tiers.
- Griddy has a spreadsheet-assistant pricing surface around browser spreadsheets plus Excel and Google Sheets add-ins.

The page deliberately stays narrow: Write My Formula is positioned for one formula, one explanation, or one repair. It does not claim to replace Ajelix's broader agentic workspace, add-ins, file upload, dashboards, charts, VBA, Apps Script, PowerPoint, or Google Workspace flows.

Sources:
- `https://ajelix.com/pricing/`
- `https://expresssheet.com/`
- `https://sheetgpt.pro/pricing`
- `https://getgriddy.ai/pricing/`

## Output

- Added `ajelix-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/ajelix-alternative/index.html`.
- Added the homepage card and sitemap entry.
- Added focused regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Deployed Vercel production deployment `dpl_H5VXhNJr4rUX7orMouaF1Zxk75dE` and aliased it to `https://writemyformula.com`.
- Committed and pushed `7c0997f Add Ajelix alternative page`.
- Submitted the new route, homepage, and sitemap to IndexNow; response HTTP `200`.

## Verification

- `npm run build:seo && npm test` passed `111/111`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no visible internal/process labels or blocked comparison claims; the only hit was an existing HTML class name, `seo-detail`.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage links to `/ajelix-alternative/`.
- Live sitemap includes `https://writemyformula.com/ajelix-alternative/`.
- Live desktop and mobile browser checks returned expected title, H1, canonical URL, six checkout links to the existing Stripe checkout URL, Ajelix copy, AVERAGEIFS example, no horizontal overflow, no console messages, and no page errors.
- Browser artifacts are under `workspace/sheetpilot-workbench/output/playwright/ajelix-alternative-live/`.

## Boundaries

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred. `config/OPEN_GATES.md` remains unchanged. Current cash balance remains `-$24.07`.

Note: `workspace/sheetpilot-workbench/README.md` already had uncommitted drift from earlier work. I added the Ajelix route line locally but intentionally did not include README in commit `7c0997f` to avoid bundling unrelated prior drift.
