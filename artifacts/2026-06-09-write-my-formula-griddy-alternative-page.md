# Write My Formula Griddy Alternative Page

Date: 2026-06-09 12:29 UTC

## Task

Shipped `https://writemyformula.com/griddy-alternative/` as a no-spend comparison-intent page for users comparing Griddy but needing one Excel or Google Sheets formula, explanation, or repair in a browser tab rather than a broader spreadsheet assistant, add-on/sidebar, chart, cleanup, formatting, sorting/filtering, or direct spreadsheet-edit workflow.

## Why this task

The open paid-search rollback/export and Fluent Forms reCAPTCHA actions remain owner-gated. Marketplace/app-template, training/resource, and consulting/support-service outreach are still under cooldown unless a relevant prospect replies. A new comparison-intent page creates another indexed sales surface without spend, new payment infrastructure, public posting, bulk outreach, or account changes.

## Live evidence

- Griddy official site: `https://getgriddy.ai/`
  - Positions Griddy as an AI spreadsheet users can talk to.
  - Says it works in Excel, Sheets, and the web.
  - Says users can tell it what they need, and it writes formulas, analyzes data, and builds the sheet.
  - Shows formula writing, data cleanup, charts and summaries, an Excel add-in, and a Google Sheets add-on.
- Google Workspace Marketplace Griddy listing: `https://workspace.google.com/marketplace/app/griddy/206105793696`
  - Lists Griddy as an AI-powered spreadsheet assistant in the Google Sheets sidebar.
  - Listing updated May 13, 2026; visible Marketplace usage shows `8K+`.
  - Describes writing and applying formulas across ranges, creating/customizing charts, cleaning/transforming data, formatting cells/rows/columns, sorting/filtering/organizing data, and undoing changes.
  - Lists free-to-try with paid features and permissions around managing installed spreadsheets, running third-party web content inside Google apps, and seeing account identity details.

Luke reviewed the buyer-facing direction in `workspace/sheetpilot-workbench/luke-griddy-alternative.md`. The final page uses his fit-based framing and avoids calling Griddy risky, intrusive, overkill, worse, or replaced by Write My Formula.

## What changed

- Added `griddy-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added a homepage comparison card in `workspace/sheetpilot-workbench/index.html`.
- Regenerated `workspace/sheetpilot-workbench/griddy-alternative/index.html`, generated static pages, and `sitemap.xml`.
- Added focused assertions to `workspace/sheetpilot-workbench/tests/content.test.js`.
- Committed and pushed nested app commit `0528122a Add Griddy alternative page`.

## Verification

- `npm run build:seo` passed.
- `npm test` passed `160/160`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Targeted public-copy scan found no blocked Griddy claims or internal/process copy; the only `placeholder` hits were normal form placeholders.
- Local Chromium desktop/mobile route checks passed: HTTP `200`, correct title/H1/canonical, six checkout links, Griddy scope copy present, boundary copy present, no horizontal overflow, `0` page errors, and only expected local static-server `POST` 501 noise before filtering.
- Optional broader `npm run qa:frontend -- --base http://127.0.0.1:4173 --routes /griddy-alternative/` returned `15/16`; the single fail was an existing formula-engine explanation expectation for Google Sheets `REGEXEXTRACT`, not the new page.
- Production route updated after polling.
- Live Chromium desktop/mobile checks passed: route HTTP `200`, correct title/H1/canonical, six checkout links, Griddy detail and boundary copy present, no horizontal overflow, `0` console messages, and `0` page errors.
- Live homepage contains `Griddy alternative`.
- Live sitemap contains `https://writemyformula.com/griddy-alternative/`.
- Actual live Stripe checkout returned HTTP `200`.
- IndexNow accepted route/home/sitemap submission with HTTP `200`.

Screenshots and summary:

- `workspace/sheetpilot-workbench/output/playwright/griddy-alternative-local/`
- `workspace/sheetpilot-workbench/output/playwright/griddy-alternative-live/`

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
