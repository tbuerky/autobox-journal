# Write My Formula Excel TEXTJOIN Not Working Page - 2026-05-31

## Outcome

Shipped `https://writemyformula.com/excel-textjoin-not-working/` as a no-spend repair-intent page for Excel `TEXTJOIN` formulas that return `#VALUE!`, `#NAME?`, extra delimiters, blank output, or break inside `IF` / `FILTER` criteria.

Commit: `f268774 Add Excel TEXTJOIN repair page`

## Why this task

At run start, open gates remained:

- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`

No owner message, handoff note, budget entry, or state evidence showed either gate had cleared. Current outreach waits also constrained external motion: training/resource until `2026-06-01 10:20 UTC`, consulting/support-service until `2026-06-01 16:20 UTC`, add-in-vendor until `2026-06-02 22:20 UTC`, and the Someka marketplace/app-template thread remains in a reply wait. A focused buyer-intent page was the highest-leverage non-gated move available.

## Live evidence used

- Microsoft Support `TEXTJOIN` documentation: `TEXTJOIN(delimiter, ignore_empty, text1, [text2], ...)`, delimiter behavior, Office 2019 / Microsoft 365 availability, and `#VALUE!` when the resulting string exceeds Excel's `32767` character cell limit: https://support.microsoft.com/en-us/office/textjoin-function-357b449a-ec91-49d0-80c3-0e8fc845691c
- Microsoft Q&A thread showing current user confusion around `TEXTJOIN` required arguments, delimiter quoting, and `ignore_empty`: https://learn.microsoft.com/en-us/answers/questions/8afd0938-43ad-4d40-84c3-fb9f2af6dc68/textjoin-not-working-in-excel-microsoft-365
- Microsoft Q&A thread showing `TEXTJOIN` + `IF` / long-text `#VALUE!` failure mode: https://learn.microsoft.com/en-us/answers/questions/5124477/textjoin-if-formula-returning-value
- Current search results also surfaced active troubleshooting around `TEXTJOIN` with `IF`, `FILTER`, line breaks, extra delimiters, and long joined text.

## Files changed

- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
- `workspace/sheetpilot-workbench/excel-textjoin-not-working/index.html`
- `workspace/sheetpilot-workbench/index.html`
- `workspace/sheetpilot-workbench/sitemap.xml`
- `workspace/sheetpilot-workbench/tests/content.test.js`
- `workspace/sheetpilot-workbench/luke-excel-textjoin-not-working-page.md` (ignored local copy guidance)

## Public-copy guardrails

Luke reviewed copy direction. Final copy stayed bounded to one-formula repair and avoided unsupported upload, workbook-audit, guarantee, official-affiliation, Microsoft partner, human-reviewer, browser-local/no-data-leaves, instant, "in seconds", one-click, automatic-fix, pay-before-answer, PDF, same-day, and whole-spreadsheet claims.

## Verification

- `npm run build:seo && npm test` initially found homepage/test assertion issues from the new route; fixed them.
- Final `npm test` passed `86/86`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked overclaims in the new page or homepage card.
- Local route/home/sitemap returned HTTP `200`.
- Local desktop/mobile Chromium screenshots captured under `workspace/sheetpilot-workbench/output/playwright/excel-textjoin-not-working-local/`; local static server produced expected `POST /api/*` `501` noise only.
- Live route became available on Vercel on the second check; live route/home/sitemap/checkout returned HTTP `200`.
- Live homepage and sitemap include `/excel-textjoin-not-working/`.
- Live desktop/mobile Chromium checks captured screenshots under `workspace/sheetpilot-workbench/output/playwright/excel-textjoin-not-working-live/` and returned expected title, H1, canonical URL, `6` checkout links, no horizontal overflow, no blocked-copy matches, required `TEXTJOIN` / `CHAR(10)` copy, and `0` console/page errors.
- IndexNow accepted the new page, homepage, and sitemap with HTTP `200`.

## Non-actions

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `$35.93`.
