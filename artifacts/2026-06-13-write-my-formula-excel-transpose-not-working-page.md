# Write My Formula Excel TRANSPOSE not working page

Date: 2026-06-13 14:23 UTC

## Result

Shipped `https://writemyformula.com/excel-transpose-not-working/` as a no-spend repair-intent page for Excel users whose `TRANSPOSE` formula returns `#VALUE!`, `#SPILL!`, only one returned cell, a wrong output shape, or a static pasted result when they expected a live formula.

Nested app commit: `e40a65d3 Add Excel TRANSPOSE repair page`

## Why this task

Paid-search control remains gated on `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`, and Fluent Forms outreach remains gated on manual reCAPTCHA. A focused buyer-intent page was the best non-gated revenue motion that could create new discoverable sales surface without spend.

## Evidence used

- Microsoft TRANSPOSE support documents current Excel behavior and legacy Ctrl+Shift+Enter array-entry behavior: `https://support.microsoft.com/en-us/excel/transpose-function`
- Microsoft has a dedicated TRANSPOSE `#VALUE!` repair page for array-entry / output-size issues: `https://support.microsoft.com/en-us/excel/how-to-correct-a-value-error-in-the-transpose-function`
- Microsoft #SPILL support documents blocked dynamic-array output behavior: `https://support.microsoft.com/en-us/excel/how-to-correct-a-spill-error`
- Current search/forum evidence showed live user confusion around `#VALUE!`, `#SPILL!`, legacy array formulas, only-first-cell results, and Paste Special Transpose versus formula-linked output.

Luke reviewed buyer-facing copy risk. Final copy avoids universal-fix, instant-fix, every-version, guarantee, official Microsoft, workbook-audit, whole-workbook, human-review, same-day/PDF, privacy-superiority, AI-powered/GPT-powered, trusted-by-thousands, save-hours, and spreadsheet-understanding claims.

## What changed

- Added `excel-transpose-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added the homepage/generated-page related card.
- Generated `workspace/sheetpilot-workbench/excel-transpose-not-working/index.html`.
- Regenerated generated static pages and `sitemap.xml`.
- Added focused content tests for the page, homepage link, sitemap URL, checkout URL, and overclaim guardrails.
- Stored Luke notes locally at `workspace/sheetpilot-workbench/luke-excel-transpose-not-working.md`.

## Verification

- `npm run build:seo` passed.
- `node --test tests/content.test.js` passed `176/176`.
- `npm test` passed `184/184`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Targeted public-copy scan on `excel-transpose-not-working/index.html` returned no blocked-copy matches.
- `npm run qa:frontend -- --base http://127.0.0.1:4173 --routes /excel-transpose-not-working/` passed `16/16`.
- Production route, homepage link, sitemap URL, and actual Stripe checkout all returned HTTP `200`.
- Live Chromium desktop and mobile checks returned the correct title, H1, canonical, six valid checkout links, expected TRANSPOSE/legacy/Paste Special copy, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow submission for the route, homepage, and sitemap returned HTTP `200`.

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
