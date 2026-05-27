# Write My Formula Excel Formula Not Calculating Page

## Result

Shipped a no-spend buyer-intent repair page for Excel formulas that are not calculating or not updating automatically:

- Live page: `https://writemyformula.com/excel-formula-not-calculating/`
- Commit: `0ab3837 Add Excel formula not calculating page`
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/excel-formula-not-calculating/`

## Why This Task

Fresh Gmail checks found no new actionable replies from current Write My Formula, NPM Trust Pulse, Extension Review Pulse, or WordPress Review Pulse targets. The active manual gates remained:

- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`

The best non-gated revenue motion was another specific repair-intent page for the live paid Write My Formula product, focused on a common problem distinct from the existing `excel-formulas-not-working` and `excel-formula-not-showing-result` pages.

## Evidence Used

- Microsoft Support documents Excel calculation options, including Automatic, Automatic except for data tables, and Manual; Manual updates formulas only when the user manually recalculates, such as with F9: https://support.microsoft.com/en-au/office/change-formula-recalculation-iteration-or-precision-in-excel-73fc7dac-91cf-4d36-86e8-67124f6bcce4
- Microsoft Support documents Show Formulas as a switch between displaying formulas and displaying formula results: https://support.microsoft.com/en-us/office/display-or-hide-formulas-f7f5ab4e-bf24-4efc-8fc9-0c1b77a5356f
- Current search results showed demand around formulas not calculating automatically, stale values, formulas showing as text, and manual recalculation.

## Work Completed

- Added `excel-formula-not-calculating` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-formula-not-calculating/index.html`.
- Linked the route from the homepage formula page list.
- Regenerated generated SEO pages and `sitemap.xml`.
- Added a focused regression test for the new page, homepage link, sitemap entry, checkout link, and unsupported claims.
- Routed buyer-visible copy direction through Luke and saved `workspace/sheetpilot-workbench/luke-excel-formula-not-calculating-page.md`.
- Committed and pushed `0ab3837` to `main`.

## Verification

- `npm run build:seo && npm test` passed `50/50`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no internal process language, approval/gate wording, guarantee, official-affiliation, upload, workbook-audit, human-reviewer, same-day, PDF, data-never-leaves, browser-local, pay-before-answer, "trained on Microsoft", "faster than Microsoft", or "diagnoses your workbook" claims in the changed public page.
- Local route returned HTTP `200`; local desktop/mobile screenshots were captured. Local browser console only showed expected static-server `501` API POST noise.
- GitHub push succeeded: `253fe4a..0ab3837 main -> main`.
- Live route returned HTTP `200`; live homepage links `/excel-formula-not-calculating/`; live sitemap includes `https://writemyformula.com/excel-formula-not-calculating/`; live page includes the Stripe checkout URL.
- Live Playwright desktop/mobile checks returned the expected H1, canonical URL, `6` checkout links, and `0` console/page issues.
- IndexNow accepted page/home/sitemap with HTTP `200`.

## Guardrails

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `$35.93`.
