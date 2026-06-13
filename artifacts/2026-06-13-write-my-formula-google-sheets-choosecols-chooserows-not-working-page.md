# Write My Formula Google Sheets CHOOSECOLS / CHOOSEROWS not working page

Date: 2026-06-13 16:28 UTC

## Result

Shipped `https://writemyformula.com/google-sheets-choosecols-chooserows-not-working/` as a no-spend repair-intent page for Google Sheets users whose `CHOOSECOLS` or `CHOOSEROWS` formula returns `#VALUE!`, selects the wrong rows or columns, uses negative positions incorrectly, cannot expand because output cells are occupied, or is nested inside a broken `FILTER`, `QUERY`, `SORT`, or `IMPORTRANGE` chain.

Nested app commit: `efd12ba4 Add Google Sheets CHOOSECOLS repair page`

## Why this task

The current owner instruction emphasized revenue operations, live web research, one task, and state-file updates before exit. Paid-search control and Fluent Forms manual reCAPTCHA remain gated; a buyer-intent formula-repair page created a non-gated sales surface without spend.

## Evidence used

- Google Docs Editors Help `CHOOSECOLS` documentation: validates selected column positions, negative positions from the end of the range, and invalid selector behavior.
- Google Docs Editors Help `CHOOSEROWS` documentation: validates selected row positions, negative positions from the end of the range, and invalid selector behavior.
- Google Sheets array-output behavior: array results cannot expand when output cells are occupied, so the final copy avoids Excel-specific `#SPILL!` wording in the target page copy.
- Current search/community evidence showed confusion around `#VALUE!`, wrong selected rows or columns, negative indexing, and nesting selectors after `FILTER`, `QUERY`, `SORT`, or `IMPORTRANGE`.
- Luke reviewed buyer-facing copy. Final target-page copy avoids Google affiliation, guarantees, automatic or instant fix claims, direct sheet editing, whole-sheet/workbook audit, human review, same-day/PDF claims, privacy-superiority claims, and Sheets-inaccurate `#SPILL!` framing.

## What changed

- Added the `google-sheets-choosecols-chooserows-not-working` page definition to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added a homepage card linking to the new page.
- Generated `workspace/sheetpilot-workbench/google-sheets-choosecols-chooserows-not-working/index.html`.
- Regenerated shared generated static pages and `sitemap.xml`.
- Added route-level and homepage tests in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Stored Luke review notes at `workspace/sheetpilot-workbench/luke-google-sheets-choosecols-chooserows-not-working.md`.

## Verification

- `npm run build:seo` passed.
- `node --test tests/content.test.js` passed `177/177`.
- `npm test` passed `185/185`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- `npm run qa:frontend -- --base http://127.0.0.1:4173 --routes /google-sheets-choosecols-chooserows-not-working/` passed `16/16`.
- Production route, homepage, sitemap, and actual Stripe checkout URL returned HTTP `200`.
- Live Chromium desktop/mobile checks found the correct title/H1, six checkout links, required `ARRAYFORMULA` warning, no horizontal overflow, no console messages, and no page errors.
- IndexNow submission for the route, homepage, and sitemap returned HTTP `200`.

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
