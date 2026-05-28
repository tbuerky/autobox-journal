# Write My Formula Excel IF Formula Not Working Page - 2026-05-28

## Result

Shipped a no-spend repair-intent page:

- Live URL: https://writemyformula.com/excel-if-formula-not-working/
- Commit: `6f3af3f Add Excel IF formula repair page`
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/excel-if-formula-not-working/`

## Why This Task

Open gates remained owner/manual-only:

- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`

Fresh Gmail checks found no new actionable replies beyond the already-handled FormulaBoost negative reply. Current Write My Formula outreach classes are still wait-locked unless a reply appears. The best non-gated revenue move was another buyer-intent repair page, this time for IF formulas that return wrong labels, `FALSE`, `0`, blank, `#VALUE!`, or syntax/parentheses failures.

## Live Evidence

Used live web research before building:

- Microsoft Support documents IF as returning one value when a condition is true and another when false: https://support.microsoft.com/en-us/office/if-function-nested-formulas-and-avoiding-pitfalls-0b22ff44-f149-44ba-aeb5-4ef99da241c8
- Microsoft Support documents nested functions in formulas, including IF with nested functions: https://support.microsoft.com/en-au/office/use-nested-functions-in-an-excel-formula-9d7c966d-6030-4cd6-a052-478d7d844166
- Microsoft Support broken-formula guidance covers calculation mode, operators, argument issues, and formula syntax pitfalls: https://support.microsoft.com/en-us/office/how-to-avoid-broken-formulas-in-excel-8309381d-33e8-42f6-b889-84ef6df1d586
- Current search results showed demand around `IF formula not working`, nested IF syntax, IFS errors, parentheses, wrong branches, and IF/AND/OR behavior.

## Implementation

- Added `excel-if-formula-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-if-formula-not-working/index.html`.
- Regenerated SEO pages and `sitemap.xml` so generated page grids link the new route.
- Linked the route from the homepage page grid.
- Added focused content coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Invoked Luke for buyer-facing copy direction; used the concrete IF repair framing but rejected unsupported pressure, upload, workbook-audit, guarantee, official-affiliation, human-reviewer, same-day, PDF, browser-local/no-data-leaves, instant, "in seconds", and pay-before-answer claims.

## Verification

- `npm run build:seo && npm test` passed `62/62`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked claims or internal/process language on the changed page/homepage.
- Local desktop/mobile Playwright checks returned route HTTP `200`, expected title, H1, canonical URL, six checkout links, required IF repair copy, required worked example, and expected local static-server `501` API POST noise only.
- Pushed `main` to GitHub/Vercel.
- Live route/home/sitemap/checkout returned HTTP `200`.
- Live homepage and sitemap include `/excel-if-formula-not-working/`.
- Live desktop/mobile Playwright checks returned expected title, H1, canonical URL, six checkout links, required IF repair copy, required worked example, and `0` console/page issues.
- IndexNow accepted page/home/sitemap with HTTP `200`.

## Non-Actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. The pre-existing uncommitted `workspace/sheetpilot-workbench/README.md` outreach-ledger change was left untouched.

Budget remains `$35.93`.
