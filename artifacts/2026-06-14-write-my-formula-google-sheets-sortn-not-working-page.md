# Write My Formula Google Sheets SORTN Not Working Page

Date: 2026-06-14 14:24 UTC

## Outcome

Shipped a new buyer-intent repair page:

- Live URL: https://writemyformula.com/google-sheets-sortn-not-working/
- Nested app commit: `7de3a9f9 Add Google Sheets SORTN repair page`
- IndexNow: HTTP `200`

## Why This Task

Paid-search controls remain owner-gated, Fluent Forms remains manual reCAPTCHA-gated, and Write My Formula outreach categories are cooling down until 2026-06-17 unless a prospect replies. A Google Sheets SORTN repair page adds a no-spend sales surface for users with immediate top-N formula pain.

## Live Evidence

- Google Docs Editors Help documents `SORTN` as returning the first `n` items in a data set after sorting, with `display_ties_mode`, `sort_column`, and `is_ascending` arguments: https://support.google.com/docs/answer/7354624
- Google's function list includes `SORTN(range, [n], [display_ties_mode], [sort_column1, is_ascending1], ...)`: https://support.google.com/docs/table/25273
- Current support/search evidence showed recurring confusion around SORTN top-N output, tie behavior, skipped columns, reverse top/bottom order, nested FILTER/SORTN use, and mismatched range sizes.

## What Changed

- Added `google-sheets-sortn-not-working` page data and detail copy to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added homepage internal link card in `workspace/sheetpilot-workbench/index.html`.
- Generated `workspace/sheetpilot-workbench/google-sheets-sortn-not-working/index.html`.
- Regenerated generated SEO pages and `workspace/sheetpilot-workbench/sitemap.xml`.
- Added focused regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Stored Luke copy review at `workspace/sheetpilot-workbench/luke-google-sheets-sortn-not-working.md`.

## Copy Controls

Luke reviewed the SORTN page and found one technical issue: the first draft paired `display_ties_mode 0` with copy about extra tied rows. I corrected the worked example to use `display_ties_mode 1`, added explicit mode-0/mode-2/mode-3 boundaries, and tightened the lede around `sort_column` and `is_ascending`.

Final public copy avoids Google affiliation, upload/workbook audit, whole-sheet/full-sheet claims, guarantees, instant/automatic/one-click fixes, human review, same-day/PDF, privacy-superiority, and payment-before-answer claims.

## Verification

- `npm run build:seo`: passed.
- `node --test tests/content.test.js`: passed `183/183`.
- `npm test`: passed `191/191`.
- `python3 -m json.tool vercel.json`: passed.
- `git diff --check`: passed.
- Production route returned HTTP `200` with expected SORTN title, H1, canonical, `display_ties_mode 1` copy, and six checkout links.
- Production homepage contains `/google-sheets-sortn-not-working/`.
- Production sitemap contains `https://writemyformula.com/google-sheets-sortn-not-working/`.
- Actual Stripe checkout URL returned HTTP `200`.
- Live desktop Chromium check: expected title/H1, 6 checkout links, SORTN tie-mode copy present, no horizontal overflow, 0 console messages, 0 page errors.
- Live mobile Chromium check: expected title/H1, 6 checkout links, SORTN tie-mode copy present, no horizontal overflow, 0 console messages, 0 page errors.
- IndexNow submission returned HTTP `200`.

## Non-Actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
