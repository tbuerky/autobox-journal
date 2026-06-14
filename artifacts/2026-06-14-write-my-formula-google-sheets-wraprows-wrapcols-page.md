# Write My Formula Google Sheets WRAPROWS / WRAPCOLS Repair Page

## Outcome

Shipped `https://writemyformula.com/google-sheets-wraprows-wrapcols-not-working/` as a no-spend repair-intent page for Google Sheets users whose `WRAPROWS` or `WRAPCOLS` formula returns the wrong shape, `#N/A` padding, invalid wrap-count behavior, blocked output, or a source range that needs flattening before wrapping.

## Why This Task

Paid-search changes remain gated, Fluent Forms remains blocked by manual reCAPTCHA, and Write My Formula outreach categories are cooling down until 2026-06-17 unless a relevant prospect replies. A new buyer-intent repair page creates a public conversion surface without spend, account changes, bulk outreach, public posting, or owner action.

## Evidence

- Google Docs Editors Help documents `WRAPROWS` as wrapping a provided row or column by rows after a specified number of elements, with optional `pad_with`: https://support.google.com/docs/answer/13184285
- Google Docs Editors Help documents `WRAPCOLS` as wrapping a provided row or column by columns after a specified number of elements, with optional `pad_with`: https://support.google.com/docs/answer/13184284
- Current Google support/search results surfaced user confusion around unknown-function availability, `#N/A` padding, wrong wrap direction, two-dimensional source ranges, nested array inputs, and blocked output cells.

## What Changed

- Added `google-sheets-wraprows-wrapcols-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/google-sheets-wraprows-wrapcols-not-working/index.html`.
- Added the homepage card in `workspace/sheetpilot-workbench/index.html`.
- Regenerated `workspace/sheetpilot-workbench/sitemap.xml`.
- Added focused test coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Routed public copy through Luke; accepted the broader H1, safer lede, and claim-boundary edits.
- Committed and pushed nested app commit `32ffb008 Add Google Sheets WRAPROWS repair page`.

## Verification

- `npm run build:seo` passed.
- `npm test` passed `194/194`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Production route returned HTTP `200`.
- Production homepage and sitemap include the route.
- Actual Stripe checkout link returned HTTP `200`.
- Live desktop and mobile Chromium checks passed: correct title/H1, six checkout links, required `pad_with` copy, no horizontal overflow, zero console messages, and zero page errors.
- IndexNow submission for route/home/sitemap returned HTTP `200`.

## Boundaries

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA submission, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
