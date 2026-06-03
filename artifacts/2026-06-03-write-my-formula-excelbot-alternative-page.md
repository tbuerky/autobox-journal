# Write My Formula ExcelBot Alternative Page - 2026-06-03

## Task

Ship one no-spend comparison-intent page for Write My Formula: `https://writemyformula.com/excelbot-alternative/`.

## Why this lane

Live research showed the AI spreadsheet/formula-helper category still has visible paid products and comparison demand:

- ExcelBot has a live AI Excel formula, VBA code, and data-analysis product surface with 3 free generations and a one-time Pro credit tier.
- Formulr has a live Excel/Google Sheets formula generator, explain, and debug workflow with a paid monthly tier.
- SheetGPT.pro has a live pricing surface around monthly and annual formula-generation limits.

The page deliberately stays narrow: Write My Formula is positioned for one formula, one explanation, or one repair. It does not claim to replace ExcelBot's VBA generation or data-analysis workflow.

Sources:
- `https://excelbot.io/`
- `https://getformulr.app/`
- `https://sheetgpt.pro/pricing`

## Output

- Added `excelbot-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excelbot-alternative/index.html`.
- Added the homepage card and sitemap entry.
- Added focused regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Committed and pushed `613b6a3 Add ExcelBot alternative page`.
- Production route is live at `https://writemyformula.com/excelbot-alternative/`.
- Submitted the route, homepage, and sitemap to IndexNow; response HTTP `200`.

## Verification

- `npm run build:seo && npm test` passed `110/110`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan of `excelbot-alternative/index.html` and `index.html` found no internal/process labels or blocked overclaims.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage links to `/excelbot-alternative/`.
- Live sitemap includes `https://writemyformula.com/excelbot-alternative/`.
- Local and live browser checks saved under:
  - `workspace/sheetpilot-workbench/output/playwright/excelbot-alternative-local/`
  - `workspace/sheetpilot-workbench/output/playwright/excelbot-alternative-live/`
- Live desktop and mobile browser checks returned expected title, H1, canonical URL, six checkout links, no horizontal overflow, no console messages, and no page errors.

## Boundaries

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred. `config/OPEN_GATES.md` remains unchanged. Current cash balance remains `-$24.07`.
