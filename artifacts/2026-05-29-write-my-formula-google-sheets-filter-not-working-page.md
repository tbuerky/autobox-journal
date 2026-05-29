# Write My Formula Google Sheets FILTER not working page - 2026-05-29

## Task
Ship one no-spend repair-intent page for Google Sheets `FILTER` formulas that return `#N/A`, show `FILTER has mismatched range sizes`, pull the wrong rows, return no rows, or mix row and column condition shapes.

## Result
- Live page: https://writemyformula.com/google-sheets-filter-not-working/
- Commit: `82b8d6e Add Google Sheets FILTER repair page`
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/google-sheets-filter-not-working/`

## Evidence
- Google Docs Editors Help documents `FILTER(range, condition1, [condition2, ...])`, requires condition arguments to have the same length as the filtered range, prohibits mixing row and column condition types in one call, and returns `#N/A` when no values satisfy the provided conditions: https://support.google.com/docs/answer/3093197
- Current search evidence showed visible repair demand around `FILTER has mismatched range sizes`, no-match `#N/A`, wrong rows, and range-size mistakes, including spreadsheet help pages and forum/Reddit/Stack Overflow threads.
- Luke reviewed the copy direction. Final copy kept the one-formula repair scope and avoided unsupported upload, workbook-audit, guarantee, official-affiliation, human-reviewer, same-day, PDF, browser-local/no-data-leaves, instant, "in seconds", pay-before-answer, and "fixes any FILTER error" claims.

## What changed
- Added `google-sheets-filter-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/google-sheets-filter-not-working/index.html`.
- Linked the route from the homepage and regenerated all static SEO pages so their embedded route grid includes the new page.
- Added sitemap coverage and focused content tests.

## Verification
- `npm run build:seo && npm test` passed `68/68`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no forbidden claims on the changed public page/homepage; matches for `task`/`run` are existing UI labels/copy, not internal process language.
- Local Firefox desktop/mobile screenshots and checks passed.
- Pushed `82b8d6e` to GitHub/Vercel.
- Live route, homepage, sitemap, and Stripe checkout URL returned HTTP `200`.
- Live homepage and sitemap include `/google-sheets-filter-not-working/`.
- Live Firefox desktop/mobile checks returned expected title, H1, canonical, `6` checkout links, required `FILTER has mismatched range sizes`, same-size range, row-versus-column, and no-match `#N/A` copy, with `0` console/page issues.
- IndexNow accepted the new page, homepage, and sitemap with HTTP `200`.

## Gates and budget
- `config/OPEN_GATES.md` remains unchanged: `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT` and `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`.
- No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.
- Current cash balance remains `$35.93`.
