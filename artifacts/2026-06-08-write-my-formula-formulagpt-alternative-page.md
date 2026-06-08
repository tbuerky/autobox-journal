# Write My Formula FormulaGPT Alternative Page

## Task

Shipped one non-gated revenue motion for Write My Formula: a buyer-intent comparison page at `https://writemyformula.com/formulagpt-alternative/`.

## Why this task

The active owner-facing gates remain:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

Write My Formula consulting/support outreach is wait-locked after the ExcelHelp send until `2026-06-11 02:20 UTC` unless a relevant prospect replies, marketplace/app-template outreach remains wait-locked until `2026-06-10 08:17 UTC`, and paid search/reCAPTCHA remain gated. The best non-gated revenue move was a new comparison-intent page for an active product not already covered.

## Live research

Sources used:

- `https://www.formulagpt.app/`
- `https://www.formulagpt.app/upgrade`
- Current AI formula-generator category search results that surfaced FormulaGPT, ExcelFormula Pro, SheetSolver AI, Sheeter, Formulr, SheetGPT, Excelly-AI, and FormulaZa as active adjacent demand.

Current FormulaGPT evidence:

- FormulaGPT presents itself as a formula generator that transforms simple English into spreadsheet formulas.
- Its homepage says it is trusted by `10,000+` spreadsheet users.
- It describes natural-language input, spreadsheet upload support for tailoring formulas to data structure, immediate results, detailed explanations, and formula verification.
- Its upgrade page lists a Free plan at `$0/month` with `10` formula generations per month and basic support.
- Its upgrade page lists a Pro plan at `$5/month` with `500` formula generations per month, priority support, and spreadsheet upload.

## Public copy boundary

Luke reviewed the buyer-facing copy direction. Final copy frames the page as a fit comparison:

- Use Write My Formula when the task is one formula, explanation, or repair in a browser tab with two guest tries.
- Use FormulaGPT or a similar account-based formula generator when the user wants monthly formula quotas, priority support, spreadsheet upload, or a natural-language generation workflow built around an account.

The final page avoids claiming Write My Formula replaces FormulaGPT, is better/faster/cheaper/more accurate, has official affiliation, provides privacy superiority, uploads workbooks, audits whole spreadsheets, automatically fixes formulas, guarantees output, provides human review, or delivers same-day/PDF work.

## Files changed

- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
- `workspace/sheetpilot-workbench/index.html`
- `workspace/sheetpilot-workbench/formulagpt-alternative/index.html`
- `workspace/sheetpilot-workbench/sitemap.xml`
- Generated static pages updated with the new homepage comparison card.
- `workspace/sheetpilot-workbench/tests/content.test.js`
- Local Luke note: `workspace/sheetpilot-workbench/luke-formulagpt-alternative.md`

Nested app commit:

- `056a4a6 Add FormulaGPT alternative page`

## Verification

- `npm run build:seo && npm test` passed `149/149`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Targeted public-copy scan found no unsupported FormulaGPT comparison claims or internal/process copy in the new route or homepage card. The only scan hits were expected existing generic formula-directory phrases such as `runs` and dynamic-array copy, not blocked FormulaGPT claims.
- Local desktop/mobile Chromium checks returned expected title, H1, canonical URL, six checkout links, FormulaGPT pricing/details, no horizontal overflow, and only expected local static-server analytics `POST` 501 console messages.
- Live route `https://writemyformula.com/formulagpt-alternative/` returned HTTP `200`.
- Live homepage returned HTTP `200` and includes the new route.
- Live sitemap returned HTTP `200` and includes the new route.
- Existing Stripe checkout URL returned HTTP `200`.
- Live desktop/mobile Chromium checks returned expected title, H1, canonical URL, six checkout links, FormulaGPT pricing/details, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow submission for the new route, homepage, and sitemap returned HTTP `200`.

## Permission and budget

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current budget balance remains `-$24.07`.
