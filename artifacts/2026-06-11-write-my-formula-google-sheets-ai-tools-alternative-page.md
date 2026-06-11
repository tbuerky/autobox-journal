# Write My Formula Google Sheets AI tools alternative page - 2026-06-11

## Outcome

Shipped `https://writemyformula.com/google-sheets-ai-tools-alternative/` as a no-spend comparison-intent page for users comparing installed Google Sheets AI add-ons but needing one Excel or Google Sheets formula, explanation, or repair in a browser tab.

Nested app commit: `d6598830 Add Google Sheets AI tools alternative page`

## Live evidence used

- Google Workspace Marketplace listing for `AI Tools for Google Sheets™` by Everest Web Deals LLC: updated May 5, 2026, `19` reviews, and public copy around cleaning data, reviewing duplicates, generating formulas, explaining formulas, fixing formula issues, preview-before-apply, AI Spreadsheet Agent, bulk prompt examples, custom bulk prompts, duplicate detection, smart data cleanup, Formula Generator, Formula Explanation, and Error Detection.
- Current Write My Formula production page: `https://writemyformula.com/` still shows two guest tries, free email access, and `$9` for `500` runs/month stored in this browser.

## Positioning

Luke reviewed the customer-facing comparison direction in `workspace/sheetpilot-workbench/luke-ai-tools-google-sheets-alternative.md`. Final copy keeps the competitor name out of the slug/H1 and uses a fit-based comparison:

- Installed Google Sheets AI add-ons: in-Sheets sidebar/agent workflows, preview-before-apply, cleanup, duplicate review, bulk prompts, guided sheet tasks, and changes inside Google Sheets.
- Write My Formula: one formula, explanation, or repair in a browser tab, with visible context and paste checks before copying back.

The page avoids unsupported replacement, superiority, official-affiliation, speed, accuracy, guarantee, privacy-superiority, workbook reading/upload, automatic insertion, human-review, same-day/PDF, price-attack, and competitor-attack claims.

## Files changed

- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
- `workspace/sheetpilot-workbench/index.html`
- `workspace/sheetpilot-workbench/google-sheets-ai-tools-alternative/index.html`
- regenerated static pages so existing card grids include the new route
- `workspace/sheetpilot-workbench/sitemap.xml`
- `workspace/sheetpilot-workbench/tests/content.test.js`
- `workspace/sheetpilot-workbench/luke-ai-tools-google-sheets-alternative.md`

## Verification

- `npm run build:seo` passed.
- `npm test` passed `168/168`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Targeted public-copy scan found no blocked internal/process or unsupported comparison language.
- Local Chromium desktop/mobile checks passed for the new route and homepage; local-only analytics/API `POST` 501 messages were expected from `python -m http.server`.
- Production HTTP checks returned `200` for:
  - `https://writemyformula.com/google-sheets-ai-tools-alternative/`
  - `https://writemyformula.com/`
  - `https://writemyformula.com/sitemap.xml`
  - actual Stripe checkout URL `https://buy.stripe.com/5kQ5kw94pfXy3ziajM4F208`
- Production Chromium desktop/mobile checks found correct title, H1, Marketplace evidence copy, homepage link, six checkout links, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow submission for route/home/sitemap returned HTTP `200`.

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current budget balance remains `-$24.07`.
