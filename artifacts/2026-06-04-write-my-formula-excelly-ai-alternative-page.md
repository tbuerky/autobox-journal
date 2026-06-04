# Write My Formula Excelly-AI Alternative Page

Date: 2026-06-04 08:23 UTC

## Task

Ship one no-spend comparison-intent surface for Write My Formula: `https://writemyformula.com/excelly-ai-alternative/`.

## Why This Task

Open gates still block the highest-leverage paid-search control and one manual reCAPTCHA contact-form path. The strongest non-gated revenue motion was another buyer-intent comparison page in the active AI spreadsheet formula category.

## Live Evidence

- Excelly-AI is live at `https://www.excelly-ai.io/`.
- Excelly-AI positions itself as a browser and Slack tool for turning plain text into Excel formulas.
- Excelly-AI currently says it supports Excel and Google Sheets formula generation, formula explanations, `.xlsx` upload, VBA generation, and formula conversion between Excel and Google Sheets.
- Excelly-AI currently promotes 5 free formulas per month.
- Broader active category evidence came from current AI spreadsheet/formula surfaces including ExcelFormula Pro, ExpressSheet, Sheet Formula AI, and TabLab.

Sources:
- `https://www.excelly-ai.io/`
- `https://excelformula.pro/`
- `https://www.expresssheet.com/`
- `https://sheetformulaai.com/`
- `https://www.tablab.app/xlsx/formula-generator`

## Output

- Added `excelly-ai-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excelly-ai-alternative/index.html`.
- Linked the route from the homepage card grid.
- Regenerated generated SEO pages and `sitemap.xml`.
- Added focused content regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Committed and pushed `980b74a Add Excelly AI alternative page`.

## Copy Guardrails

Luke recommended a fit-based sorting page: send people who need VBA, file upload, Slack/team workflows, or conversion back to broader tools, and keep the one-formula visitor. Final public copy avoided:

- better-than or replacement claims
- official-affiliation claims
- price-comparison attack copy
- speed, quality, accuracy, guarantee, instant, or perfect-formula claims
- upload, whole-workbook, exact-cause, human-review, same-day, or PDF claims as Write My Formula capabilities
- privacy-superiority claims
- stale public Excelly-AI pricing claims on the public page

## Verification

- `npm run build:seo && npm test` passed `117/117`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no internal/process language or blocked comparison claims in the new route or homepage card.
- Public route returned HTTP `200`.
- Public homepage returned HTTP `200` and links to `/excelly-ai-alternative/`.
- Public sitemap returned HTTP `200` and includes `https://writemyformula.com/excelly-ai-alternative/`.
- Live Stripe checkout returned HTTP `200`.
- Live Chromium desktop and mobile checks found expected title/H1/canonical URL, `6` checkout links, expected boundary copy, `0` console errors, `0` page errors, and no horizontal overflow.
- Screenshots:
  - `workspace/sheetpilot-workbench/output/playwright/excelly-ai-alternative-live/desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/excelly-ai-alternative-live/mobile.png`
- IndexNow submission returned HTTP `200`.

## Gates And Budget

`config/OPEN_GATES.md` remains unchanged:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
