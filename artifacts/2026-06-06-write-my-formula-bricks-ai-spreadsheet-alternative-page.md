# Write My Formula Bricks AI Spreadsheet Alternative Page

Date: 2026-06-06 12:26 UTC

## Outcome
Shipped `https://writemyformula.com/bricks-ai-spreadsheet-alternative/` as a no-spend comparison-intent page for users comparing Bricks-style AI spreadsheet workspaces but needing one Excel or Google Sheets formula, explanation, or repair in a browser tab rather than a full AI spreadsheet, dashboard, chart, report, upload, slide, template, or collaboration workflow.

Commit: `0408140 Add Bricks AI spreadsheet alternative page`

## Evidence
Live research checked official Bricks pages on 2026-06-06:
- Bricks' public AI Spreadsheet page positions Bricks as an AI spreadsheet and AI data analyst for analyzing data, performing calculations, formatting and cleaning data, creating charts, dashboards, reports, importing Excel/CSV files, exporting data, using traditional formulas and functions, templates, mobile/web access, and real-time collaboration.
- Bricks' AI Basics docs describe AI Chat across Grid and Board work, including row analysis, cleaning and formatting tables, writing formulas or conditional-formatting rules, sorting, filtering, duplicate removal, and generating reports from structured data.
- Bricks' formula docs describe Excel-style formula generation from natural-language prompts and examples for whole-column formulas, math, date/time, text, logical, and lookup/reference formulas.

Sources used:
- `https://www.thebricks.com/ai-spreadsheet`
- `https://www.thebricks.com/docs/ai/ai-basics`
- `https://www.thebricks.com/docs/ai/ai-formulas`

## Public Copy Boundaries
Luke reviewed the copy direction. Final copy stayed fit-based: Write My Formula for one formula, explanation, or repair; Bricks or another AI spreadsheet workspace for file import, data cleaning, row analysis, dashboards, charts, reports, slides, templates, real-time collaboration, or AI changes inside a spreadsheet grid.

The page avoids unsupported replacement, better-than, official-affiliation, partner, speed, accuracy, guarantee, instant/perfect-formula, automatic-fix, privacy-superiority, upload/whole-workbook support, exact-cause, human-review, same-day/PDF-delivery, competitor-attack, bloated, and overpriced claims.

## Files Changed
- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
- `workspace/sheetpilot-workbench/index.html`
- `workspace/sheetpilot-workbench/tests/content.test.js`
- `workspace/sheetpilot-workbench/bricks-ai-spreadsheet-alternative/index.html`
- Generated SEO pages and `workspace/sheetpilot-workbench/sitemap.xml`
- Screenshots and summaries under `workspace/sheetpilot-workbench/output/playwright/bricks-ai-spreadsheet-alternative-local/` and `workspace/sheetpilot-workbench/output/playwright/bricks-ai-spreadsheet-alternative-live/`

## Verification
- `npm run build:seo && npm test` passed `136/136`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked internal/process language or unsupported Bricks comparison claims in the new route or homepage card.
- Local Chromium desktop/mobile checks returned HTTP `200`, expected title/H1/canonical, 6 checkout links, homepage link present, required Bricks boundary copy, no blocked copy, no horizontal overflow, and no page errors. Static-server `POST /api/*` returned expected local `501` noise only.
- Production route, homepage, sitemap, and actual Stripe checkout URL returned HTTP `200`.
- Production homepage and sitemap include `/bricks-ai-spreadsheet-alternative/`.
- Production Chromium desktop/mobile checks returned expected title, H1, canonical URL, 6 checkout links, required Bricks boundary copy, no blocked copy, no horizontal overflow, no console messages, and no page errors.
- IndexNow submission for route/home/sitemap returned HTTP `200`.

## Permissions And Budget
No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
