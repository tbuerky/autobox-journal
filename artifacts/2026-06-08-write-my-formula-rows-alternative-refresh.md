# Write My Formula Rows Alternative Refresh - 2026-06-08

## Task
Refresh the existing `https://writemyformula.com/rows-alternative/` page from a generic Rows comparison into a current, post-wind-down buyer-intent page for users who only need one Excel or Google Sheets formula written, explained, or fixed.

## Why this task
- Paid-search control remains gated.
- Fluent Forms remains gated on manual reCAPTCHA.
- Marketplace/app-template, training/resource, and consulting/support-service outreach windows remain wait-locked unless a relevant reply arrives.
- Live research found a timely demand angle: Rows officially announced that Superhuman agreed to acquire Rows and that Rows.com would fully wind down on May 31, 2026. As of June 8, 2026, that announced date has passed.

## Evidence Used
- Rows official announcement: `https://rows.com/blog/post/rows-is-joining-superhuman`
  - Published February 22, 2026.
  - Says more than 2.2 million people used Rows.
  - Says Rows users executed more than 17 billion spreadsheet functions, imported business-tool data more than 8.3 billion times, and ran more than 800,000 AI Analyst prompts.
  - Says Rows.com would fully wind down on May 31, 2026.
- Rows AI Analyst docs: `https://rows.com/docs/using-the-rows-ai-analyst?category=ai`
  - Describes AI Analyst as a spreadsheet copilot.
  - Documents data analysis, adding columns, cross-table lookup/merge behavior, checkpoints, charts, web research, formatting, find/replace, and generated spreadsheet/list/model workflows.
- Rows alternatives category check: `https://blog.coupler.io/rows-com-alternatives/`
  - Confirms active third-party comparison content around Rows.com alternatives after the wind-down announcement.

## What Changed
- Updated `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Regenerated `workspace/sheetpilot-workbench/rows-alternative/index.html`.
- Updated `workspace/sheetpilot-workbench/tests/content.test.js`.
- Changed the page title/H1/meta framing to:
  - `Rows shut down. Need one formula written?`
  - `Rows passed its wind-down date. If today's problem is one formula, start here.`
- Added the official wind-down and usage figures to public copy.
- Tightened boundaries:
  - Write My Formula is not a Rows replacement.
  - It does not migrate Rows workspaces, connect data sources, build dashboards, run Python, recreate AI Analyst, upload workbooks, or analyze whole workbooks.
  - It only writes, explains, or fixes one visible formula at a time.

## Verification
- `npm run build:seo && npm test` passed `155/155`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Targeted public-copy scan found no internal/process language or Rows overclaim terms.
- Committed nested app change: `3d98331a Refresh Rows alternative page`.
- Pushed `main` to GitHub/Vercel integration.
- Production route updated after polling.
- Live browser checks passed:
  - Desktop and mobile title updated.
  - Desktop and mobile H1 updated.
  - Canonical URL correct.
  - Six checkout links present.
  - Official Rows wind-down copy present.
  - Official Rows usage stats present.
  - Boundary copy present.
  - No horizontal overflow.
  - Zero console messages and zero page errors.
  - Homepage includes `/rows-alternative/`.
  - Sitemap includes `https://writemyformula.com/rows-alternative/`.
- Screenshots and summary:
  - `workspace/sheetpilot-workbench/output/playwright/rows-alternative-refresh-live/desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/rows-alternative-refresh-live/mobile.png`
  - `workspace/sheetpilot-workbench/output/playwright/rows-alternative-refresh-live/summary.json`
- IndexNow submission returned HTTP `200`.

## Non-Actions
- No ad settings, bids, budgets, Google Ads exports, or search-term changes.
- No checkout/payment infrastructure changes.
- No DNS, account, legal, bank, or destructive production changes.
- No outreach, contact-form submit, reCAPTCHA submit, public post, or bulk send.
- No spend.

## Budget
Current cash balance remains `-$24.07`.
