# Write My Formula Google Sheets SPLIT Not Working Page

Date: 2026-06-14 12:24 UTC

## Outcome

Shipped a new buyer-intent repair page:

- Live URL: https://writemyformula.com/google-sheets-split-not-working/
- Nested app commit: `e517cc58 Add Google Sheets SPLIT repair page`
- IndexNow: HTTP `200`

## Why This Task

Paid-search controls remain owner-gated, Fluent Forms remains manual reCAPTCHA-gated, and Write My Formula outreach categories are cooling down until 2026-06-17 unless a prospect replies. A Google Sheets SPLIT repair page adds a no-spend sales surface for users with immediate formula pain.

## Live Evidence

- Google Docs Editors Help documents `SPLIT(text, delimiter, [split_by_each], [remove_empty_text])`, with `split_by_each` defaulting to TRUE and `remove_empty_text` defaulting to TRUE: https://support.google.com/docs/answer/3094136
- Current search/support evidence showed recurring confusion around Google Sheets SPLIT delimiter behavior, preserving blank fields, split output space, and split-text-to-columns workflows.

## What Changed

- Added `google-sheets-split-not-working` page data and detail copy to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added homepage internal link card in `workspace/sheetpilot-workbench/index.html`.
- Generated `workspace/sheetpilot-workbench/google-sheets-split-not-working/index.html`.
- Regenerated generated SEO pages and `workspace/sheetpilot-workbench/sitemap.xml`.
- Added focused regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Stored Luke copy review at `workspace/sheetpilot-workbench/luke-google-sheets-split-not-working.md`.

## Copy Controls

Luke reviewed the SPLIT page. Accepted copy edits narrowed the page from "separating text correctly" to "separating text the way you expect", changed the lede from a broad "repair path" promise to a concrete workbench check and revised-SPLIT-to-test promise, and clarified the `split_by_each` default behavior. I did not apply Luke's unrelated pricing suggestions in this run.

Final public copy avoids Google affiliation, guarantees, upload/workbook audit, whole-sheet/full-sheet claims, instant/automatic/one-click fixes, human review, same-day/PDF, privacy-superiority, and payment-before-answer claims.

## Verification

- `npm run build:seo`: passed.
- `node --test tests/content.test.js`: passed `182/182`.
- `python3 -m json.tool vercel.json`: passed.
- `git diff --check`: passed.
- Production route returned HTTP `200` with expected SPLIT H1 and copy.
- Production homepage contains `/google-sheets-split-not-working/`.
- Production sitemap contains `https://writemyformula.com/google-sheets-split-not-working/`.
- Live desktop Chromium check: title/H1 expected, 6 checkout links, SPLIT copy present, no horizontal overflow, 0 console messages, 0 page errors.
- Live mobile Chromium check: title/H1 expected, 6 checkout links, SPLIT copy present, no horizontal overflow, 0 console messages, 0 page errors.
- Actual Stripe checkout URL returned HTTP `200`.
- IndexNow submission returned HTTP `200`.

## Non-Actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
