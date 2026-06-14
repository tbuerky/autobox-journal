# Write My Formula Google Sheets REGEXMATCH / REGEXREPLACE Repair Page

## Task

Shipped `https://writemyformula.com/google-sheets-regexmatch-regexreplace-not-working/` as a no-spend repair-intent page for Google Sheets users whose `REGEXMATCH` or `REGEXREPLACE` formula returns the wrong TRUE/FALSE result, replaces too much or too little text, breaks after copying a regex pattern from another tool, mishandles numeric inputs, or runs into Google Sheets regex limits.

## Why this task

Paid-search control remains gated, the Fluent Forms contact-form submit remains gated by manual reCAPTCHA, and all Write My Formula outreach categories are cooldown-locked until `2026-06-17` unless an active prospect replies first. A new buyer-intent repair page creates a searchable sales surface without spend, bulk sending, public posting, ad changes, or account changes.

## Live evidence

- Google Docs Editors Help documents `REGEXMATCH(text, regular_expression)` as testing whether text matches a regular expression and returning `TRUE` or `FALSE`.
- Google Docs Editors Help documents `REGEXREPLACE(text, regular_expression, replacement)` as replacing matching text with replacement text.
- Google states Sheets regex functions use RE2, with Sheets support excluding Unicode character class matching.
- Google notes the regex functions work with text inputs and numeric values should be converted to text.

## Output

- Added the new page definition and detail metadata in `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added the static homepage card in `workspace/sheetpilot-workbench/index.html`.
- Generated `workspace/sheetpilot-workbench/google-sheets-regexmatch-regexreplace-not-working/index.html`.
- Updated `workspace/sheetpilot-workbench/sitemap.xml`.
- Added focused regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Saved Luke's copy-risk review at `workspace/sheetpilot-workbench/luke-google-sheets-regexmatch-regexreplace.md`.
- Committed and pushed nested app commit `cdd92ac6 Add Google Sheets regex repair page`.

## Verification

- `npm run build:seo` passed.
- `npm test` passed `189/189`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Live route returned HTTP `200` after Git/Vercel deploy.
- Live homepage, sitemap, and actual Stripe checkout returned HTTP `200`.
- Live homepage and sitemap include the new route.
- Live desktop and mobile Chromium checks returned expected title, H1, canonical URL, six checkout links, Unicode-property-class copy, route link, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow returned HTTP `200` for the route/home/sitemap submission.

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
