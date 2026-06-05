# Write My Formula ExcelGPT Alternative Page

Date: 2026-06-05 14:24 UTC

## Task
Ship one no-spend revenue-moving asset for the active Write My Formula lane while paid-search control and Fluent Forms remain gated.

## Output
- Shipped `https://writemyformula.com/excelgpt-alternative/`.
- Commit: `fd552b7 Add ExcelGPT alternative page`.
- Screenshots:
  - `workspace/sheetpilot-workbench/output/playwright/excelgpt-alternative-live/desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/excelgpt-alternative-live/mobile.png`

## Live Evidence
- ExcelGPT live page (`https://excelgpt.app/en`) currently positions the product as an AI Excel assistant and "Formula Generator & Automation Suite" with formula generation, uploaded-file analysis, chart builder, automation, auto Excel processing, file conversion, multi data source workflows, AI insights, Power Query/VBA-style help, SQL, regex, and script automation.
- ExcelGPT pricing section currently lists Free, Pro at `$19.90/month`, and Lifetime at `$299 one-time`.
- Broader active category evidence checked during selection included ExpressSheet (`https://expresssheet.com/`) with formula generation, spreadsheet/file analysis, AI chat, charts, PDF export, API, and paid Pro pricing, plus active search evidence for SumifAI and Sheet Copilot-style spreadsheet AI tools.

## Copy Guardrails
- Luke reviewed buyer-facing copy direction. Final implementation used the fit-based "sort, not sell" frame.
- Final copy stayed bounded to Write My Formula's actual scope: one Excel or Google Sheets formula, explanation, or repair in a browser tab.
- Final copy routes users to ExcelGPT-style tools when they need uploaded-file analysis, data cleaning, charts, dashboards, automation, file conversion, connected data sources, SQL, regex, VBA, scripts, or workbook-wide insights.
- Final copy avoids replacement, better-than, official-affiliation, partner, guarantee, perfect-formula, instant, one-click, automatic-fix, privacy-superiority, human-review, same-day/PDF, bloated, overpriced, and unsupported accuracy/speed claims.

## Verification
- `npm run build:seo && npm test` passed `127/127`.
- `python3 -m json.tool vercel.json` passed.
- Production HTTP checks returned `200` for:
  - `https://writemyformula.com/excelgpt-alternative/`
  - `https://writemyformula.com/`
  - `https://writemyformula.com/sitemap.xml`
  - `https://buy.stripe.com/5kQ5kw94pfXy3ziajM4F208`
- Live sitemap includes `https://writemyformula.com/excelgpt-alternative/`.
- Live homepage links to `/excelgpt-alternative/`.
- Live Chromium desktop and mobile checks confirmed:
  - expected title, H1, canonical URL
  - six live Stripe checkout links
  - required ExcelGPT boundary copy
  - no blocked overclaim copy
  - no horizontal overflow
  - `0` console messages
  - `0` page errors
- IndexNow accepted page/home/sitemap submission with HTTP `200`.

## Gates And Budget
- `config/OPEN_GATES.md` unchanged:
  - `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
  - `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`
- No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.
- Current cash balance remains `-$24.07`.
