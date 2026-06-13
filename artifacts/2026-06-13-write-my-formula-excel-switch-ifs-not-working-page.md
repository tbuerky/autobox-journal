# Write My Formula Excel SWITCH / IFS not working page

Date: 2026-06-13 10:25 UTC

## Result

Shipped `https://writemyformula.com/excel-switch-ifs-not-working/` as a no-spend repair-intent page for Excel users whose `SWITCH` or `IFS` formula returns `#N/A`, `#VALUE!`, `#NAME?`, the wrong branch, or a missing default result.

## Why This Task

Current owner instruction was to think like a revenue operator, keep the run to one task, use live web research, and avoid StrikeRewind / PAF as default work queues. Write My Formula remains the active business lane. The paid-search rollback/export action is gated, Fluent Forms submission is gated by manual reCAPTCHA, and outreach categories remain cooldown-limited until 2026-06-14 unless a relevant reply arrives. A focused buyer-intent repair page created a new public sales surface without spend or permission-gated action.

## Live Evidence

Live research used Microsoft Support evidence:

- `SWITCH` returns `#N/A` when no match exists and no default argument is supplied.
- `IFS` is documented for Excel 2019 and newer plus Microsoft 365; Microsoft documents a final `TRUE` logical test as the default result pattern.
- `IFS` returns `#VALUE!` when a logical test does not resolve to TRUE or FALSE, and `#N/A` when no TRUE condition is found.
- Microsoft's current functions category page continues to list these functions in the Excel function reference.

Additional current search evidence showed real user confusion around `SWITCH` / `IFS` `#N/A`, `#NAME?`, and no-match behavior.

## What Changed

- Added `excel-switch-ifs-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added the homepage/shared page-grid card.
- Generated `workspace/sheetpilot-workbench/excel-switch-ifs-not-working/index.html`.
- Regenerated static SEO pages and `sitemap.xml`.
- Added a focused `tests/content.test.js` regression for page copy, sitemap inclusion, checkout wiring, homepage link, and banned claims.
- Ran Luke copy-risk review and integrated the substantive changes: clearer error-first H1/title, shorter lede, explicit "revised formula with explanation and copy checks" promise, and more precise version-support wording.
- Committed and pushed nested app commit `71ac32ea Add Excel SWITCH IFS repair page`.

## Verification

- `npm run build:seo` passed.
- `node --test tests/content.test.js` passed `174/174`.
- `npm test` passed `182/182`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- `npm run qa:frontend -- --base http://127.0.0.1:4173 --routes /excel-switch-ifs-not-working/` passed `16/16`.
- Production route returned HTTP `200` after Git/Vercel deployment.
- Production homepage, sitemap, and actual Stripe checkout returned HTTP `200`.
- Live desktop/mobile Chromium checks returned correct title, H1, canonical URL, six checkout links, no blocked copy, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow submission for the new route, homepage, and sitemap returned HTTP `200`.

## Non-Actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA submission, public post, bulk send, destructive production change, or spend occurred.

## State

Open gates remain unchanged:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

Current budget balance remains `-$24.07`.
