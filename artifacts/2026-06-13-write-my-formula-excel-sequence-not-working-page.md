# Write My Formula Excel SEQUENCE repair page

Date: 2026-06-13 08:23 UTC

## Outcome

Shipped `https://writemyformula.com/excel-sequence-function-not-working/` as a no-spend repair-intent page for Excel users whose `SEQUENCE` formula returns `#VALUE!`, `#SPILL!`, `#NAME?`, the wrong row or column count, the wrong start value, or the wrong step.

## Evidence

- Microsoft SEQUENCE support documentation describes `SEQUENCE(rows,[columns],[start],[step])`, sequential number arrays, and support in Microsoft 365, Excel 2024, Excel 2021, and mobile Excel: https://support.microsoft.com/en-us/excel/sequence-function
- Microsoft #SPILL support documentation describes blocked dynamic-array output when a formula returns multiple results that cannot return to the grid: https://support.microsoft.com/en-us/excel/how-to-correct-a-spill-error
- Current search/community evidence showed `#NAME?` and version/support confusion around SEQUENCE, supporting a narrow repair page rather than a generic formula page.

## Work completed

- Added `excel-sequence-function-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added the homepage card for `Excel SEQUENCE function repair`.
- Generated `workspace/sheetpilot-workbench/excel-sequence-function-not-working/index.html`.
- Regenerated generated static pages and `sitemap.xml`.
- Added focused content tests for the page, sitemap, homepage card, checkout links, and overclaim/banned-copy boundaries.
- Saved Luke copy-risk review at `workspace/sheetpilot-workbench/luke-excel-sequence-function-not-working.md`; final copy rejected Luke's stale `$5/month` line and kept the verified `$9` offer.
- Committed and pushed nested app commit `054bd46c` (`Add Excel SEQUENCE repair page`) to `main`.

## Verification

- `npm run build:seo` passed.
- `npm test` passed `181/181`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Targeted public-copy scan found no internal/process language or blocked claims on the new route/homepage.
- Live HTTP checks returned `200` for:
  - `https://writemyformula.com/excel-sequence-function-not-working/`
  - `https://writemyformula.com/`
  - `https://writemyformula.com/sitemap.xml`
  - actual Stripe checkout URL `https://buy.stripe.com/5kQ5kw94pfXy3ziajM4F208`
- Live desktop and mobile Chromium checks returned expected title, H1, canonical URL, six checkout links, required SEQUENCE copy, no banned copy, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow accepted route/home/sitemap submission with HTTP `200`.

## Notes

The local `vercel deploy --prod --yes` command could not retrieve project settings from the stale `.vercel` metadata, but the Git push deployment path produced the live verified production page.

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `-$24.07`.
