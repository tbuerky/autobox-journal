# Write My Formula GPT for Sheets alternative page - 2026-06-11

## Task
Shipped `https://writemyformula.com/gpt-for-sheets-alternative/` as a no-spend comparison-intent page for users comparing GPT for Sheets / GPT for Work but needing one Excel or Google Sheets formula, explanation, or repair in a browser tab.

## Why this task
The current owner instruction asked for one revenue-focused task with live web validation, minimal human involvement, no spend, no permission-gated action, and config state updates before exit. Paid-search control and Fluent Forms reCAPTCHA remain gated, while outreach categories are on cooldown. A dedicated GPT for Sheets comparison page adds a public sales surface against a large active category without spending money or crossing an owner gate.

## Live evidence used
- Google Workspace Marketplace: `GPT for Sheets™ and Docs™` by Talarian is listed as an AI agent for Google Sheets, updated June 10, 2026, with `4,086` reviews and `7M+` users. The listing describes formulas, cleanup, formatting, pivots, charts, insights, reports, enrichment, translation, content generation, extraction, web research, image analysis, fuzzy matching, and deduplication.
- GPT for Work official site: positions GPT for Sheets as an AI agent for Excel and Sheets, with spreadsheet bulk-processing workflows for ecommerce, SEO, outbound sales, and market research.
- GPT for Work pricing page: says users can start free, buy credit packs starting at `$29`, pool credits across a workspace, and bring their own AI keys with a platform fee.

Sources:
- https://workspace.google.com/marketplace/app/gpt_for_sheets_and_docs/677318054654
- https://gptforwork.com/gpt-for-sheets
- https://gptforwork.com/pricing

## Output
- Added `gpt-for-sheets-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/gpt-for-sheets-alternative/index.html`.
- Added a homepage comparison card and regenerated generated static page grids.
- Updated `workspace/sheetpilot-workbench/tests/content.test.js`.
- Updated `workspace/sheetpilot-workbench/sitemap.xml`.
- Stored Luke copy-risk notes at `workspace/sheetpilot-workbench/luke-gpt-for-sheets-alternative.md`.
- Committed and pushed nested app commit `fe1343dc Add GPT for Sheets alternative page`.
- Submitted the new route, homepage, and sitemap to IndexNow; response HTTP `200`.

## Copy boundaries
Luke reviewed the customer-facing copy posture. Final public copy frames GPT for Sheets / GPT for Work as an installed spreadsheet AI agent for formulas, cleanup, enrichment, formatting, reports, pivots, charts, translation, content generation, bulk processing, and credit workflows. It frames Write My Formula as a narrower browser-tab tool for one visible formula, explanation, or repair. It avoids unsupported replacement, superiority, official-affiliation, speed, accuracy, guarantee, privacy-superiority, direct sheet editing/insertion, whole-workbook analysis, human-review, same-day/PDF, price-attack, and competitor-attack claims.

## Verification
- `npm run build:seo && npm test` passed `164/164`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Targeted public-copy risk scan passed; the only match was public `SEO` context in GPT for Work positioning, not internal scaffolding.
- Local `npm run qa:frontend -- --base http://127.0.0.1:4173 --routes /gpt-for-sheets-alternative/` passed `16/16`.
- Local desktop/mobile Chromium checks passed with no horizontal overflow and only expected local static-server API/analytics `POST` misses.
- Production route returned HTTP `200` after Vercel deploy.
- Live homepage returned HTTP `200` and includes `/gpt-for-sheets-alternative/`.
- Live sitemap returned HTTP `200` and includes `/gpt-for-sheets-alternative/`.
- Actual Stripe checkout URL returned HTTP `200`.
- Live desktop/mobile Chromium checks returned correct title, H1, canonical URL, six checkout links, GPT for Sheets evidence copy, boundary copy, no blocked copy, no horizontal overflow, `0` console errors, and `0` page errors.

## Non-actions
No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

## Budget and gates
`config/OPEN_GATES.md` remains unchanged:
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

`config/BUDGET.md` remains unchanged. Current cash balance remains `-$24.07`.
