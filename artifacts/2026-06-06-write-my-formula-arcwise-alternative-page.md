# Write My Formula Arcwise Alternative Page

Date: 2026-06-06 10:25 UTC

## Outcome
Shipped `https://writemyformula.com/arcwise-alternative/` as a no-spend comparison-intent page for users comparing Arcwise / AI Copilot for Sheets but needing one Excel or Google Sheets formula, explanation, or repair in a browser tab rather than an in-Sheets AI analyst, connected-data, large-data formula, PDF-ingestion, ARCQUERY, GPT-formula, pivot, graph, report, or custom AI-function workflow.

Commit: `9b45527 Add Arcwise alternative page`

## Evidence
Live research checked Arcwise public docs and the Chrome Web Store listing on 2026-06-06. Current public positioning observed:
- Arcwise docs describe Arcwise as an AI-first data analysis and reporting platform deeply integrated with Google Sheets.
- Docs describe connecting data from data warehouses and other tools, working with large data, and using AI Analyst in Sheets.
- Docs say formulas can execute on full connected datasets in the database, connected-data previews may show 100 rows, and formula cells may need manual refresh and show `#N/A` until refreshed.
- Docs describe GPT formulas that require the Chrome extension and sheet permissions.
- Docs describe `ARCQUERY` for inline SQL and supported/limited spreadsheet-function subsets.
- Chrome Web Store listing for AI Copilot for Sheets by Arcwise showed `10,000 users`, `4.5` rating across `23` ratings, version `2.3.1`, updated September 14, 2024.
- The listing describes text-command data explanation/transformation/ingestion in Sheets, pivots, graphs, auto-generated insights, PDF table extraction, and `AI.TRANSFORM`, `AI.CLASSIFY`, and `AI.EXTRACT` functions.

## Public Copy Boundaries
Luke reviewed the copy direction. Final copy stayed fit-based: Write My Formula for one browser-tab formula, explanation, or repair; Arcwise-style tools for AI analysis inside Google Sheets, connected warehouse data, large-data formulas, pivots, graphs, reports, PDF table extraction, `ARCQUERY`, GPT formulas, and custom AI functions in sheet cells.

The page avoids unsupported replacement, better-than, official-affiliation, partner, speed, accuracy, guarantee, instant/perfect-formula, automatic-fix, privacy-superiority, upload/whole-workbook, exact-cause, human-review, same-day/PDF-delivery, competitor-attack, bloated, and overpriced claims.

## Files Changed
- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
- `workspace/sheetpilot-workbench/index.html`
- `workspace/sheetpilot-workbench/tests/content.test.js`
- `workspace/sheetpilot-workbench/arcwise-alternative/index.html`
- Generated SEO pages and `workspace/sheetpilot-workbench/sitemap.xml`
- Screenshots and summaries under `workspace/sheetpilot-workbench/output/playwright/arcwise-alternative-local/` and `workspace/sheetpilot-workbench/output/playwright/arcwise-alternative-live/`

## Verification
- `npm run build:seo && npm test` passed `135/135`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked internal/process language or unsupported Arcwise comparison claims in the new route or homepage card.
- Local Chromium desktop/mobile checks returned HTTP `200`, expected title/H1/canonical, 6 checkout links, homepage link present, required Arcwise boundary copy, no page errors, and no horizontal overflow. Static-server `POST /api/*` returned expected local `501` noise only.
- Production route, homepage, sitemap, and actual Stripe checkout URL returned HTTP `200`.
- Production homepage and sitemap include `/arcwise-alternative/`.
- Production Chromium desktop/mobile checks returned expected title, H1, canonical URL, 6 checkout links, required Arcwise boundary copy, no blocked copy, no horizontal overflow, no console messages, and no page errors.
- IndexNow submission for route/home/sitemap returned HTTP `200`.

## Permissions And Budget
No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
