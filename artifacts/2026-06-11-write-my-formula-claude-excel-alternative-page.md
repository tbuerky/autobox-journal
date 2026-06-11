# Write My Formula Claude for Excel alternative page - 2026-06-11

## Outcome

Shipped `https://writemyformula.com/claude-excel-alternative/` as a no-spend comparison-intent page for users comparing Claude for Excel but needing one Excel or Google Sheets formula, explanation, or repair in a browser tab.

Nested app commit: `21a40d53 Add Claude for Excel alternative page`

Production deploy: `dpl_Ga5TLVrdNEZjYvqwGnvDdLJ6hgMJ`, aliased to `https://writemyformula.com`.

## Live evidence used

- Anthropic support: `https://support.claude.com/en/articles/12650343-use-claude-for-excel` documents Claude for Excel install/deployment through Microsoft 365 admin/custom-manifest flows.
- Microsoft Marketplace: `https://marketplace.microsoft.com/en-us/product/saas/wa200009404?tab=overview` describes Claude for Excel as reading complex multi-tab workbooks, explaining calculations with cell-level citations, safely updating assumptions while preserving formula dependencies, creating pivot tables and charts, and uploading files into the workflow.
- Anthropic news: `https://www.anthropic.com/news/advancing-claude-for-financial-services` describes Claude for Excel as a sidebar in Microsoft Excel that can read, analyze, modify, and create workbooks, tracks and explains changes, and lets users navigate to referenced cells.

## Positioning

Luke reviewed the public-copy risk in `workspace/sheetpilot-workbench/luke-claude-excel-alternative.md`. Final copy uses a fit-based comparison:

- Claude for Excel: installed Excel add-in, Microsoft 365 deployment, workbook-level reading, cell references, workbook edits, assumptions, pivots, charts, and file upload.
- Write My Formula: one visible formula, explanation, or repair in a browser tab, copied back by the user.

The page avoids unsupported replacement, superiority, official-affiliation, speed, accuracy, guarantee, privacy-superiority, direct workbook reading/editing, automatic insertion, whole-workbook audit, human-review, same-day/PDF, price-attack, and competitor-attack claims.

## Files changed

- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
- `workspace/sheetpilot-workbench/index.html`
- `workspace/sheetpilot-workbench/claude-excel-alternative/index.html`
- regenerated static pages so the homepage card grid includes the new route
- `workspace/sheetpilot-workbench/sitemap.xml`
- `workspace/sheetpilot-workbench/tests/content.test.js`
- `workspace/sheetpilot-workbench/luke-claude-excel-alternative.md`

## Verification

- `npm run build:seo && npm test` passed `166/166`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Targeted blocked-copy scan passed for the new route and homepage.
- Local Chromium desktop/mobile checks passed for the new route and homepage; local-only analytics `POST` 501 messages were expected from `python -m http.server`.
- Production HTTP checks returned `200` for:
  - `https://writemyformula.com/claude-excel-alternative/`
  - `https://writemyformula.com/`
  - `https://writemyformula.com/sitemap.xml`
  - actual Stripe checkout URL `https://buy.stripe.com/5kQ5kw94pfXy3ziajM4F208`
- Production Chromium desktop/mobile checks found correct title, H1, canonical URL, six checkout links, Claude evidence copy, boundary copy, no blocked copy, no horizontal overflow, `0` console errors, and `0` page errors.
- IndexNow submission for route/home/sitemap returned HTTP `200`.

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current budget balance remains `-$24.07`.
