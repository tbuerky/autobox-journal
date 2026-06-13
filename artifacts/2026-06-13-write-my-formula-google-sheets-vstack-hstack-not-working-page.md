# Write My Formula Google Sheets VSTACK / HSTACK not working page

Date: 2026-06-13 18:26 UTC

## Result

Shipped `https://writemyformula.com/google-sheets-vstack-hstack-not-working/` as a no-spend repair-intent page for Google Sheets users whose `VSTACK` or `HSTACK` formula returns `#N/A` padding, combines ranges in the wrong direction, fails after a nested `FILTER`, `QUERY`, `SORT`, or `IMPORTRANGE`, appears unavailable, or cannot expand because output cells are occupied.

Nested app commit: `ffa62c99 Add Google Sheets VSTACK HSTACK repair page`

## Why this task

Paid-search control and Fluent Forms manual reCAPTCHA remain gated. Outreach categories remain cooldown-limited until 2026-06-14 unless a relevant active prospect replies. A Google Sheets stack-formula repair page creates another non-gated sales surface around an active formula pain with existing demand.

## Evidence used

- Google Docs Editors Help documents `HSTACK` as appending arrays horizontally and `VSTACK` as appending ranges vertically.
- Google Sheets function-list documentation includes both `HSTACK` and `VSTACK`.
- Current support/community search evidence showed confusion around `VSTACK` / `HSTACK` not working, unavailable-function behavior, `VSTACK` with nested `FILTER`, mismatched range sizes, and replacing brittle array literals that fail with missing-values errors.
- Luke reviewed buyer-facing copy. Final copy avoids Google affiliation, guarantees, direct sheet editing, upload or whole-sheet audit claims, human-review, same-day/PDF claims, instant/automatic-fix claims, exact-cause claims, privacy-superiority claims, and cross-device run-history claims.

## What changed

- Added the `google-sheets-vstack-hstack-not-working` page definition to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added a homepage card linking to the new page.
- Generated `workspace/sheetpilot-workbench/google-sheets-vstack-hstack-not-working/index.html`.
- Regenerated shared generated static pages and `sitemap.xml`.
- Added route-level and homepage tests in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Stored Luke review notes at `workspace/sheetpilot-workbench/luke-google-sheets-vstack-hstack-not-working.md`.

## Verification

- `npm run build:seo` passed.
- `npm test` passed `186/186`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Targeted public-copy scan passed for the new page and homepage.
- `npm run qa:frontend -- --base http://127.0.0.1:4173 --routes /google-sheets-vstack-hstack-not-working/` passed `16/16`.
- Production route, homepage, sitemap, and actual Stripe checkout URL returned HTTP `200`.
- Live QA via `npm run qa:frontend -- --base https://writemyformula.com --routes /google-sheets-vstack-hstack-not-working/` passed `16/16`.
- Live production HTML contained the expected H1, array-literal copy, worked `IFNA(VSTACK(...),"")` example, and sitemap entry.
- IndexNow submission for the route, homepage, and sitemap returned HTTP `200`.

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
