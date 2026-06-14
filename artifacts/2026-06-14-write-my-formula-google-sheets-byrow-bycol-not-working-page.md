# Write My Formula Google Sheets BYROW / BYCOL Not Working Page - 2026-06-14

## Outcome

Shipped a no-spend buyer-intent repair page:

- `https://writemyformula.com/google-sheets-byrow-bycol-not-working/`

The page targets Google Sheets users whose `BYROW` or `BYCOL` formula fails because of LAMBDA argument count errors, invalid LAMBDA names, named-function placeholder mistakes, nested array results, row-versus-column direction issues, or blocked output cells.

## Why This Task

Fresh owner instruction for this run: act like a revenue operator, avoid defaulting to StrikeRewind or PAF, use live web research to choose/validate a lane, keep the run to one task, and update config state before exit.

Paid-search changes remain gated, Fluent Forms remains blocked by manual reCAPTCHA, and Write My Formula outreach categories are cooling down until 2026-06-17 unless an active prospect replies. A new repair-intent page creates another indexed sales surface without spend or owner permission gates.

## Live Research

Used official current Google Docs Editors Help pages:

- BYROW: `https://support.google.com/docs/answer/12570930?hl=en`
- BYCOL: `https://support.google.com/docs/answer/12571032?hl=en`
- LAMBDA: `https://support.google.com/docs/answer/12508718?hl=en`

Relevant Google-documented constraints used in the copy:

- `BYROW` groups an array by rows using a `LAMBDA`; `BYCOL` groups an array by columns using a `LAMBDA`.
- The LAMBDA passed to `BYROW` or `BYCOL` must have exactly one name argument plus a formula expression.
- A name such as `C1` is invalid because it conflicts with a range reference.
- Each row or column must group to a single value; nested array results are not supported.
- Named functions can be passed as the LAMBDA argument but need exactly one placeholder and should not be followed by parentheses.

## Public Copy Review

Luke reviewed the draft. Accepted changes:

- Tightened the hero lede to lead with a pasted-formula repair pass and one-row/one-column test.
- Reframed detail copy around the user's formula rather than generic examples.
- Added an explicit boundary that Write My Formula does not see the workbook and only uses what the user pastes.
- Removed unsupported generated-copy claims around a free email account tier / `3 runs per week` and first access to account features.

The final target page avoids Google affiliation, upload/workbook audit, guarantees, direct sheet editing, instant/automatic/one-click fixes, human-review, same-day/PDF, privacy-superiority, whole-sheet/workbook audit, and payment-before-answer claims.

## Files Changed

Nested app repo: `workspace/sheetpilot-workbench`

- `scripts/build-seo-pages.mjs`
- `index.html`
- `google-sheets-byrow-bycol-not-working/index.html`
- `sitemap.xml`
- `tests/content.test.js`
- Regenerated static `*/index.html` files to remove stale shared pricing/free-account claims.

Commit pushed to GitHub/Vercel:

- `e3f07845 Add Google Sheets BYROW BYCOL repair page`

## Verification

- `npm run build:seo` passed.
- `npm test` passed `192/192`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Production route returned HTTP `200` after deployment propagated.
- Production homepage returned HTTP `200` and links to `/google-sheets-byrow-bycol-not-working/`.
- Production sitemap returned HTTP `200` and includes the new route.
- Actual Stripe checkout URL `https://buy.stripe.com/5kQ5kw94pfXy3ziajM4F208` returned HTTP `200`.
- Production fetched HTML for the new page/home/sitemap contains no stale `3 runs per week` or `first access to account features` copy.
- IndexNow submission for the new page, homepage, and sitemap returned HTTP `200`.

## Gates, Spend, And State

Open gates remain unchanged:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Budget unchanged: `-$24.07`.
