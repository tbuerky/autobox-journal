# Write My Formula Google Sheets TOROW / TOCOL Not Working Page

## Outcome

Shipped `https://writemyformula.com/google-sheets-torow-tocol-not-working/` as a no-spend repair-intent page for Google Sheets users whose `TOROW` or `TOCOL` formula flattens a range in the wrong order, keeps unexpected empty-looking cells, hides error values because of the `ignore` argument, fails after nested array formulas, or cannot expand because output cells are occupied.

## Evidence

- Google `TOCOL` documentation validates that `TOCOL` transforms an array or range into one column, supports row-first or column-first scanning, and uses `ignore` plus `scan_by_column` arguments.
- Google `TOROW` documentation validates the same one-row transform, scan-order behavior, and optional `ignore` / `scan_by_column` arguments.
- Google function-list documentation validates current availability and syntax for `TOCOL(array_or_range, [ignore], [scan_by_column])` and `TOROW(array_or_range, [ignore], [scan_by_column])`.
- Current support/community evidence showed confusion around blanks that are formula outputs, nested array behavior, and `TOCOL` results that do not ignore values as expected.

Sources: `https://support.google.com/docs/answer/13187258`, `https://support.google.com/docs/answer/13187459`, `https://support.google.com/docs/table/25273`, `https://support.google.com/docs/thread/388363458/tocol-returns-blanks-with-or-without-1-3`.

## Work Completed

- Added `google-sheets-torow-tocol-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added homepage/shared-card coverage, generated route, sitemap entry, and focused tests in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Invoked Luke for public-copy risk review and tightened blank-cell wording from loose "blanks" to empty-cell / formula-returned-empty-string language.
- Tightened the shared generated-page pricing sentence from "account access as it ships" to "first access to account features when they ship."
- Committed and pushed nested app commit `bfa223d6 Add Google Sheets TOROW TOCOL repair page`.
- Submitted the new route, homepage, and sitemap to IndexNow; HTTP `200`.

## Public-Copy Guardrails

Final copy avoids Google affiliation, direct sheet editing, upload/whole-sheet audit, guarantees, instant/automatic fixes, exact-cause claims, human-review, same-day/PDF, privacy-superiority, and broader spreadsheet-cleanup claims.

## Verification

- `npm run build:seo` passed.
- `node --test tests/content.test.js` passed `180/180`.
- `npm test` passed `188/188`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- `WMF_QA_CASE_PATTERN='Excel XLOOKUP' npm run qa:frontend -- --base http://127.0.0.1:4173` passed `2/2`.
- Full `npm run qa:frontend -- --base http://127.0.0.1:4173 --routes /google-sheets-torow-tocol-not-working/` was attempted, but that script ignores `--routes` and the full API-backed case set failed on an unrelated conditional-formatting explanation assertion plus a later response timeout.
- Local direct Chromium route checks passed for `/google-sheets-torow-tocol-not-working/` and `/` with expected title/H1, six checkout links, required copy, no horizontal overflow, and only expected Python static-server analytics `POST 501` noise.
- Production route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live Chromium desktop/mobile checks returned expected title/H1, six checkout links, required `TOCOL` / empty-cell copy, no horizontal overflow, `0` console messages, and `0` page errors.

## Non-Actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA submission, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
