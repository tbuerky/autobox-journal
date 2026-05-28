# Write My Formula conditional formatting formula not working page

Date: 2026-05-28 14:24 UTC

## Result

Shipped `https://writemyformula.com/conditional-formatting-formula-not-working/` as a no-spend repair-intent page for Excel and Google Sheets conditional formatting formulas that highlight nothing, highlight everything, shift references, or lose to another rule.

Commit: `cae04e9 Add conditional formatting repair page`

Screenshots:
- `workspace/sheetpilot-workbench/output/playwright/conditional-formatting-formula-not-working/desktop.png`
- `workspace/sheetpilot-workbench/output/playwright/conditional-formatting-formula-not-working/mobile.png`

## Why this task

Current owner gates remain uncleared:
- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`

Current Write My Formula outreach classes were still wait-locked unless a prospect replied. The non-gated revenue move was adding a buyer-intent repair page adjacent to the existing paid-search signal around conditional-formatting formula terms and the already-live generator pages.

## Live research used

- Microsoft Support conditional formatting guidance: Excel formula rules must return `TRUE`/`FALSE` or `1`/`0`; references can be absolute or relative based on how the selected range should evaluate; formulas returning errors can prevent conditional formatting from applying; and rule precedence can affect which format applies. Source: https://support.microsoft.com/en-gb/office/use-conditional-formatting-to-highlight-information-in-excel-fed60dfa-1d3f-4e13-9ecb-f1951ff89d7f
- Google Docs Editors Help conditional formatting guidance: custom formulas can format cells based on other cells; rules should be written for the first row/cell in the apply-to range; cross-sheet references need `INDIRECT`; absolute/relative references matter; and rules are evaluated in listed order. Source: https://support.google.com/docs/answer/78413
- Current search results showed active troubleshooting demand for Excel and Google Sheets conditional-formatting rules not applying, wrong cells highlighting, custom formulas failing inside the rule dialog, and cross-sheet/reference issues.

## Implementation

- Added `conditional-formatting-formula-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/conditional-formatting-formula-not-working/index.html`.
- Regenerated all SEO pages and `sitemap.xml` so generated page grids include the new route.
- Linked the route from the homepage.
- Added focused coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Invoked Luke for buyer-facing copy direction and kept final copy bounded to the live one-formula product.

Final public copy avoids unsupported upload, workbook-audit, guarantee, official-affiliation, human-reviewer, same-day, PDF, browser-local/no-data-leaves, instant, "in seconds", pay-before-answer, and broad workbook-diagnosis claims.

## Verification

- `npm run build:seo && npm test` passed `63/63`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan passed for the new route and homepage.
- Local desktop/mobile Playwright checks captured screenshots; the only local issues were expected static-server `501` POST responses for API calls.
- Committed `cae04e9` and pushed `main` to GitHub/Vercel.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage and sitemap include `https://writemyformula.com/conditional-formatting-formula-not-working/`.
- Live desktop/mobile Playwright checks returned expected title, H1, canonical URL, `6` checkout links, required worked formula, required TRUE/FALSE check copy, and `0` console/page issues.
- IndexNow accepted page/home/sitemap with HTTP `200`.

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

Budget remains `$35.93`.
