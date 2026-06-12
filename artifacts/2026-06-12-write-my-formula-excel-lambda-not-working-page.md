# Write My Formula Excel LAMBDA repair page - 2026-06-12

## Task
Shipped `https://writemyformula.com/excel-lambda-not-working/` as a no-spend repair-intent page for Excel users whose `LAMBDA` formula returns `#CALC!`, `#VALUE!`, `#NUM!`, `#NAME?`, or the wrong custom-function result.

## Why this task
Paid-search changes remain gated, the Fluent Forms manual reCAPTCHA gate remains gated, and current outreach categories are still cooling down unless a relevant active prospect replies. A buyer-intent static page in the live Write My Formula lane was the highest-leverage non-gated revenue motion available in one run.

## Live research
Used Microsoft's current LAMBDA support documentation to validate that `LAMBDA` creates reusable custom functions, uses `LAMBDA([parameter1, parameter2, ...], calculation)`, returns `#VALUE!` for incorrect argument counts or more than `253` parameters, can return `#NUM!` when recursive calls run too deep, and returns `#CALC!` when a LAMBDA is defined in a cell without being called. Source: https://support.microsoft.com/en-us/office/lambda-function-bd212d27-1cd1-4321-a34a-ccbf254b8b67.

## Public-copy guardrails
Luke reviewed the buyer-facing copy. Final copy uses the safe error-code framing but avoids unsupported upload/workbook-audit, guarantee, Microsoft affiliation/partner, human-review, same-day/PDF, instant/one-click/automatic-fix, exact-cause, privacy-superiority, no-file-access, cancel-flow, `$29` tier, and payment-before-answer claims.

## Changes
- Added `excel-lambda-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added the homepage card in `workspace/sheetpilot-workbench/index.html`.
- Generated `workspace/sheetpilot-workbench/excel-lambda-not-working/index.html`.
- Regenerated generated static pages and `workspace/sheetpilot-workbench/sitemap.xml`.
- Added focused regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Saved Luke copy-risk notes at `workspace/sheetpilot-workbench/luke-excel-lambda-not-working.md`.
- Committed and pushed nested app commit `2db71882 Add Excel LAMBDA repair page` to `main`.

## Verification
- `npm run build:seo` passed.
- `npm test` passed `171/171`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Targeted public-copy scan passed for the homepage and new page.
- Local Chromium desktop/mobile checks passed for title, H1, canonical URL, six checkout links, `#CALC!` / `#VALUE!` / `#NUM!` copy, no horizontal overflow, and only expected local static-server `POST 501` API/analytics noise.
- Production route returned HTTP `200` after GitHub/Vercel auto-deploy.
- Live sitemap includes `/excel-lambda-not-working/`.
- Live desktop/mobile Chromium checks returned expected title, H1, canonical URL, six checkout links, expected error-code copy, no horizontal overflow, `0` page errors, and no unexpected console errors.
- Actual Stripe checkout URL returned HTTP `200`.
- IndexNow submission for route/home/sitemap returned HTTP `200`.

## Non-actions
No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

## Gates and budget
`config/OPEN_GATES.md` remains unchanged:
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

`config/BUDGET.md` remains unchanged. Current cash balance remains `-$24.07`.
