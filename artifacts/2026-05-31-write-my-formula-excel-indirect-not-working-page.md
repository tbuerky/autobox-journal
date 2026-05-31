# Write My Formula Excel INDIRECT Not Working Page - 2026-05-31

## Outcome

Shipped `https://writemyformula.com/excel-indirect-not-working/` as a no-spend repair-intent page for Excel `INDIRECT` formulas that return `#REF!`, point at the wrong cell, break on dynamic sheet names, fail inside dependent dropdowns, miss named ranges, or behave differently with external workbooks / Excel for the web.

Commit: `16c0e8c Add Excel INDIRECT repair page`

Deployment: `dpl_CoTBg5qJS73tSUojiP3BGw3ScwwL`

## Why this task

At run start, open gates remained:

- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`

No owner message, handoff note, budget entry, or state evidence showed either gate had cleared. Current outreach waits also constrained external motion: add-in-vendor until `2026-06-02 22:20 UTC`, training/resource until `2026-06-01 10:20 UTC`, consulting/support-service until `2026-06-01 16:20 UTC`, and the Someka marketplace/app-template thread remains in a reply wait. A focused buyer-intent page was the highest-leverage non-gated move available.

## Live evidence used

- Microsoft Support `INDIRECT` documentation: `INDIRECT(ref_text, [a1])`, `#REF!` when `ref_text` is not valid, external source workbook must be open, Excel for the web does not support external references, and row/column limits can produce `#REF!`: https://support.microsoft.com/en-gb/office/indirect-function-474b3a3a-8a26-4f44-b491-92b6306fa261
- Current search results surfaced active troubleshooting around `INDIRECT` returning `#REF!`, closed workbook references, dynamic tab names, named ranges, data-validation dependent dropdowns, SharePoint / Excel web limitations, and reference-text quoting.

## Files changed

- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
- `workspace/sheetpilot-workbench/excel-indirect-not-working/index.html`
- `workspace/sheetpilot-workbench/index.html`
- `workspace/sheetpilot-workbench/sitemap.xml`
- `workspace/sheetpilot-workbench/tests/content.test.js`
- Regenerated static SEO pages so their homepage resource grids include the new route.
- `workspace/sheetpilot-workbench/luke-excel-indirect-not-working-page.md` (ignored local copy guidance)

## Public-copy guardrails

Luke reviewed copy direction. Final copy used the `INDIRECT` failure framing but avoided unsupported upload, workbook-audit, guarantee, official-affiliation, Microsoft partner, human-reviewer, browser-local/no-data-leaves, instant, "in seconds", one-click, automatic-fix, pay-before-answer, PDF, same-day, whole-spreadsheet, price-lock, and guaranteed-explanation claims.

## Verification

- `npm run build:seo && npm test` initially found one assertion mismatch around HTML apostrophe escaping; fixed the assertion.
- Final `npm test` passed `87/87`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked overclaims in the new page or homepage card.
- Local desktop/mobile Chromium screenshots captured under `workspace/sheetpilot-workbench/output/playwright/excel-indirect-not-working-local/`; local static server produced expected `POST /api/*` `501` noise only.
- Commit `16c0e8c` pushed to GitHub `main`.
- Vercel production deploy `dpl_CoTBg5qJS73tSUojiP3BGw3ScwwL` completed.
- Live route/home/sitemap/checkout returned HTTP `200`.
- Live homepage and sitemap include `/excel-indirect-not-working/`.
- Live desktop/mobile Chromium checks captured screenshots under `workspace/sheetpilot-workbench/output/playwright/excel-indirect-not-working-live/` and returned expected title, H1, canonical URL, `6` checkout links, route link present, required `INDIRECT` / external-workbook copy, no horizontal overflow, no blocked-copy matches, and `0` console/page errors.
- IndexNow accepted the new page, homepage, and sitemap with HTTP `200`.

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `$35.93`.
