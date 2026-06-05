# Write My Formula Sourcetable Alternative Page

Date: 2026-06-05 22:25 UTC

## Result

Shipped `https://writemyformula.com/sourcetable-alternative/` as a no-spend comparison-intent page for users comparing Sourcetable-style AI spreadsheet platforms but needing one Excel or Google Sheets formula, explanation, or repair in the sheet they already use.

Commit: `6fbbdaa Add Sourcetable alternative page`

## Live Evidence Used

- Sourcetable pricing page: https://sourcetable.com/pricing
  - Regular plan is free with limited daily credits and includes AI spreadsheet assistant, AI analysis/insights/summarization, smart formulas, pivots, charts, visualizations, magic autofill, AI research, template generation, data cleaning, and transforms.
  - Pro is listed at `$29/user/month` with premium AI models, Python/data science toolkit, SQL editor/query builder/library, and up to 3 data connectors.
  - Max is listed at `$100/user/month` with advanced agent capabilities and unlimited data connectors subject to guardrails.
  - FAQ describes file upload and chat, `.xls`, `.xlsx`, `.csv`, `.tsv`, PDF, JSON, and database data support, multiple-tab analysis, visualizations, Python, SQL, and A1 formula references.
- Broader category evidence: Bricks docs show active AI formula generation inside an AI spreadsheet/workspace category, and Arcwise docs show an AI-first data-analysis platform with Google Sheets integration and spreadsheet-formula behaviors.

## Public Copy Boundary

Final page frames the choice as job-size fit:

- Use Write My Formula for one Excel or Google Sheets formula, explanation, or repair.
- Use Sourcetable or a similar AI spreadsheet workspace for uploads, spreadsheet chat, AI analysis, pivots, charts, visualizations, data cleaning, AI research, SQL, Python, connectors, or analysis across workbook tabs.

Avoided replacement, better-than, official-affiliation, partner, speed, accuracy, guarantee, perfect/instant/automatic fix, privacy-superiority, Write My Formula upload/whole-workbook support, exact-cause, human-review, same-day/PDF delivery, and competitor-attack claims.

## Changes

- Added `sourcetable-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added the homepage comparison card.
- Regenerated static pages and `sitemap.xml`.
- Added focused tests for Sourcetable scope, homepage link, sitemap URL, checkout links, live pricing facts, and blocked overclaims.
- Added Playwright live screenshots and summary under `workspace/sheetpilot-workbench/output/playwright/sourcetable-alternative-live/`.

## Verification

- `npm run build:seo && npm test` passed `131/131`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan on `sourcetable-alternative/index.html` and `index.html` found no internal/process language or blocked Sourcetable claims.
- Commit `6fbbdaa` was pushed to `main`, and Vercel served the new route on the second live check.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage includes `/sourcetable-alternative/`; live sitemap includes `https://writemyformula.com/sourcetable-alternative/`.
- Live Chromium desktop and mobile checks found expected title, H1, canonical URL, six Stripe checkout links, required Sourcetable boundary copy, no blocked copy, no horizontal overflow, no console messages, and no page errors.
- IndexNow submission for route, homepage, and sitemap returned HTTP `200`.

## Gates And Spend

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
