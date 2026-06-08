# Write My Formula Excel Formulas AI Alternative Page

## Task

Shipped one non-gated revenue motion for Write My Formula: a buyer-intent comparison page at `https://writemyformula.com/excel-formulas-ai-alternative/`.

## Why this task

The active owner-facing gates remain:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

Write My Formula marketplace/app-template and consulting/support-service outreach windows are still wait-locked after the latest sends, and paid search/reCAPTCHA remain gated. The best non-gated revenue move was a new comparison-intent page for an active formula-generator product not already covered.

## Live research

Sources used:

- `https://excelformulasai.com/`
- Current AI formula-generator category search results that surfaced Rows, AI Formula Generator, ExpressSheet, GenieSheet, ExcelFormula Pro, SheetGPT, Musely Excel Formula Bot, Formulr, and adjacent formula-generator tools as active demand.

Current Excel Formulas AI evidence:

- Excel Formulas AI presents itself as a free Excel formula generator that converts descriptions into formulas.
- Its homepage says it is trusted by `500K+` users.
- It shows `500K+` conversions and a `4.9/5` rating.
- It includes examples for `SUM`, `AVERAGE`, `VLOOKUP`, `IF`, `COUNTIF`, `SUMIF`, `CONCATENATE`, `INDEX/MATCH`, and `TODAY`.
- It describes `100% free`, no-registration, unlimited formula generation.

## Public copy boundary

Luke reviewed the buyer-facing copy direction. Final copy frames the page as a fit comparison:

- Use Excel Formulas AI or a similar free generator when constant Excel formula generation and examples are enough.
- Use Write My Formula when the task is one formula, explanation, or repair in a browser tab with range notes and paste checks.

The final page avoids claiming Write My Formula replaces Excel Formulas AI, is better/faster/cheaper/more accurate/smarter/more powerful, has official affiliation, provides privacy superiority, uploads workbooks, audits whole spreadsheets, automatically fixes formulas, guarantees output, provides human review, or delivers same-day/PDF work.

## Files changed

- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
- `workspace/sheetpilot-workbench/index.html`
- `workspace/sheetpilot-workbench/excel-formulas-ai-alternative/index.html`
- `workspace/sheetpilot-workbench/sitemap.xml`
- Generated static pages updated with the new homepage comparison card.
- `workspace/sheetpilot-workbench/tests/content.test.js`
- Local Luke note: `workspace/sheetpilot-workbench/luke-excel-formulas-ai-alternative.md`

Nested app commit:

- `500447d Add Excel Formulas AI alternative page`

## Verification

- `npm run build:seo && npm test` passed `150/150`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Targeted public-copy scan found no internal/process copy or blocked Excel Formulas AI comparison claims.
- Live route `https://writemyformula.com/excel-formulas-ai-alternative/` returned HTTP `200`.
- Live homepage returned HTTP `200` and includes the new route.
- Live sitemap returned HTTP `200` and includes the new route.
- Existing Stripe checkout URL returned HTTP `200`.
- Live desktop/mobile Chromium checks returned expected title, H1, canonical URL, six checkout links, Excel Formulas AI detail copy, no blocked copy, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow submission for the new route, homepage, and sitemap returned HTTP `200`.

## Permission and budget

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current budget balance remains `-$24.07`.
