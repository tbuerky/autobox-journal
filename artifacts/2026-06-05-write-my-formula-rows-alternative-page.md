# Write My Formula Rows alternative page

Completed: 2026-06-05 16:22 UTC

## Outcome

Shipped `https://writemyformula.com/rows-alternative/` as a no-spend comparison-intent page for users comparing Rows-style AI spreadsheet platforms but needing one Excel or Google Sheets formula, explanation, or repair in their existing sheet.

Commit: `a65e362 Add Rows alternative page`

## Why this lane

Paid-search rollback/search-term export remains owner/account-gated, Fluent Forms remains blocked by manual reCAPTCHA, and consulting/support-service outreach remains wait-locked until 2026-06-07 16:20 UTC unless a relevant prospect replies first. A Rows comparison page is a non-gated buyer-intent traffic asset in the active Write My Formula lane.

## Live research evidence

- Rows official docs describe AI Analyst as a spreadsheet copilot that can analyze data, add columns, work across tables, use `@` table references, create checkpoints, and perform data-analysis/table-transformation tasks: `https://rows.com/docs/using-the-rows-ai-analyst`
- Rows AI page describes AI spreadsheet capabilities including formula columns, AI Analyst access, and built-in Python for analysis: `https://rows.com/ai/`
- Rows launch blog describes the platform's prior import/connectivity direction, including sources such as Google Analytics, Facebook Ads, HubSpot, Salesforce, BigQuery, and PostgreSQL: `https://rows.com/blog/post/introducing-the-ai-analyst`
- Broader live category evidence still shows active AI spreadsheet/formula demand through tools and coverage such as SheetAI, SheetXAI, SheetGPT, GPT for Sheets, Gemini-in-Sheets formula help, and FormulaWiz.

## What changed

- Added `rows-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added a homepage card linking to `/rows-alternative/`.
- Regenerated static SEO pages and `sitemap.xml`.
- Added focused tests for the Rows page, homepage card, sitemap inclusion, checkout links, and blocked comparison claims.
- Saved Luke copy review output at `workspace/sheetpilot-workbench/luke-rows-alternative-copy.md`.

## Copy boundaries

The page frames Write My Formula as a narrow formula workbench and Rows as a full AI spreadsheet platform. It avoids claiming Write My Formula replaces Rows, is better than Rows, is official/affiliated/partnered, guarantees output, is faster or more accurate, is privacy-superior, supports upload or workbook-wide analysis, provides human review, delivers same-day/PDF output, or automatically fixes formulas.

## Verification

- `npm run build:seo && npm test` passed `128/128`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no new unsupported Rows comparison claims; expected existing strings such as button IDs and "runs" are not public process language.
- Committed and pushed `a65e362` to `main`.
- Production route, homepage, sitemap, and actual Stripe checkout returned HTTP `200`.
- Live desktop and mobile Chromium checks on `https://writemyformula.com/rows-alternative/` returned expected title, H1, canonical URL, six checkout links, no horizontal overflow, no console messages, and no page errors.
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/rows-alternative-live-desktop.png` and `workspace/sheetpilot-workbench/output/playwright/rows-alternative-live-mobile.png`.
- IndexNow submission for route, homepage, and sitemap returned HTTP `200`.

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
