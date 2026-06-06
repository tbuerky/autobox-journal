# Write My Formula Excelmatic Alternative Page - 2026-06-06

## Result

Shipped a no-spend comparison-intent page:

- Live URL: `https://writemyformula.com/excelmatic-alternative/`
- Commit: `1dc6624 Add Excelmatic alternative page`
- Screenshots and browser summary: `workspace/sheetpilot-workbench/output/playwright/excelmatic-alternative-live/`

The page targets people searching for an Excelmatic alternative, while acknowledging the current rebrand/redirect to RowSpeak. The positioning is fit-based: RowSpeak for file analysis, dashboards, charts, reports, image/PDF-to-Excel, and broader business-analysis workflows; Write My Formula for one Excel or Google Sheets formula, explanation, or repair in a browser tab.

## Live Evidence Used

- `https://excelmatic.ai/` and related Excelmatic URLs now redirect to RowSpeak surfaces.
- RowSpeak quick-start docs describe the product as an AI business agent for turning raw data into professional deliverables, with file upload before AI activation, weekly KPI packs, monthly business reports, forecasts, scenarios, dashboard workflows, data cleaning, transformations, visualization, charts, and image/PDF-to-Excel workflows.
- RowSpeak Excel AI page describes uploading Excel, CSV, PDF, or image-based tables, asking in plain English, cleaning messy files, analyzing changes, and creating charts, dashboards, summaries, and reports.
- RowSpeak pricing page currently lists Essential at `$9.9` monthly or `$99/year`, Professional at `$29.9` monthly or `$299/year`, Premium at `$59.9` monthly or `$599/year`, and a free plan FAQ with 10 AI conversations/month, up to 2 file uploads/chat at 5MB each, 20 image-to-Excel conversions, and 3 dashboard generations.

## Work Completed

- Added `excelmatic-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excelmatic-alternative/index.html`.
- Added the homepage card in `workspace/sheetpilot-workbench/index.html`.
- Regenerated `workspace/sheetpilot-workbench/sitemap.xml`.
- Added focused assertions in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Invoked Luke for public-copy risk review and used the useful positioning guidance while correcting his stale/mistaken RowSpeak pricing note against live evidence.

## Verification

- `npm run build:seo` passed.
- `npm test` passed `140/140`.
- `python3 -m json.tool vercel.json` passed.
- Live route, homepage, sitemap, and actual Stripe checkout URL returned HTTP `200`.
- Live homepage links to `/excelmatic-alternative/`; live sitemap includes the route.
- Live desktop and mobile Chromium checks returned:
  - expected title, H1, and canonical URL
  - 6 checkout links to the live Stripe checkout URL
  - `0` console messages
  - `0` page errors
  - no horizontal overflow
- IndexNow submission for route, homepage, and sitemap returned HTTP `200`.

## Guardrails

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Open gates remain unchanged:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

Current cash balance remains `-$24.07`.
