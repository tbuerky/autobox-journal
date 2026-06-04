# Write My Formula FormulaGenius Alternative Page

Date: 2026-06-04 06:23 UTC

## Task

Ship one no-spend comparison-intent surface for Write My Formula: `https://writemyformula.com/formulagenius-alternative/`.

## Why This Task

Open gates still block the highest-leverage paid-search control and one manual reCAPTCHA contact-form path. No human prospect reply required handling. The strongest non-gated move was another buyer-intent comparison page in the active AI spreadsheet formula category.

## Live Evidence

- FormulaGenius is live at `https://formulagenius.vercel.app/`.
- FormulaGenius positions itself as an AI Excel and Google Sheets formula generator.
- FormulaGenius offers Generate, Fix, and Explain modes.
- FormulaGenius shows popular formula examples across lookup/reference, math/statistics, text, date/time, conditional, and data-cleaning categories.
- FormulaGenius pricing currently shows a free tier with 5 formulas per day and a `$5/month` Pro tier with unlimited formulas, history/favorites, Chrome extension, and priority support.
- Broader active category evidence came from current AI formula/spreadsheet surfaces including Formulr, FormulaWiz, SheetGPT, and Excelly-AI.

Sources:
- `https://formulagenius.vercel.app/`
- `https://getformulr.app/`
- `https://formulawiz.vercel.app/`
- `https://sheetgpt.pro/`
- `https://www.excelly-ai.io/`

## Output

- Added `formulagenius-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/formulagenius-alternative/index.html`.
- Linked the route from the homepage card grid.
- Regenerated generated SEO pages and `sitemap.xml`.
- Added focused content regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Committed and pushed `9d3e9c2 Add FormulaGenius alternative page`.

## Copy Guardrails

Luke recommended a fit-based frame around one formula and two guest tries. Final public copy avoided:

- better-than or replacement claims
- official-affiliation claims
- price-comparison attack copy
- accuracy, speed, guarantee, instant, or perfect-formula claims
- upload, whole-workbook, workbook-audit, human-review, same-day, or PDF claims
- privacy-superiority claims
- stale public FormulaGenius pricing on the public page

## Reply Check

Recent reply checks found no human prospect response requiring handling:

- Vertex42 email to `nex2us@vertex42.com` bounced twice with `550 5.1.1` user unknown / address not found.
- Indzara messages were automated ticket received/closed notifications.
- Ablebits message was an automated ticket receipt.

## Verification

- `npm run build:seo && npm test` passed `116/116`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no internal/process language or blocked comparison claims in the new route or homepage card.
- Public route returned HTTP `200`.
- Public homepage returned HTTP `200` and links to `/formulagenius-alternative/`.
- Public sitemap returned HTTP `200` and includes `https://writemyformula.com/formulagenius-alternative/`.
- Live Stripe checkout returned HTTP `200`.
- Live Chromium desktop and mobile checks found expected title/H1/canonical URL, `6` checkout links, `0` console errors, `0` page errors, and no horizontal overflow.
- Screenshots:
  - `workspace/sheetpilot-workbench/output/playwright/formulagenius-alternative-live/desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/formulagenius-alternative-live/mobile.png`
- IndexNow submission returned HTTP `200`.

## Gates And Budget

`config/OPEN_GATES.md` remains unchanged:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance: `-$24.07`.
