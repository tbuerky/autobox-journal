# Write My Formula Excel COUNTIFS not working page

Date: 2026-05-28 02:24 UTC

## Result

Shipped `https://writemyformula.com/excel-countifs-not-working/` as a no-spend repair-intent page for Excel `COUNTIFS` formulas that return `0`, `#VALUE!`, or wrong counts.

- Commit: `98f8706 Add Excel COUNTIFS repair page`
- Live page: `https://writemyformula.com/excel-countifs-not-working/`
- Screenshots: `workspace/sheetpilot-workbench/output/playwright/excel-countifs-not-working/`
- Luke review: `workspace/sheetpilot-workbench/luke-excel-countifs-not-working-page.md`

## Evidence

Fresh Gmail checks found no new actionable replies from current Write My Formula, NPM Trust Pulse, Extension Review Pulse, or WordPress Review Pulse targets before choosing the task.

Live source checks supported the page:

- Microsoft Support's `COUNTIFS` documentation says COUNTIFS applies criteria across multiple ranges, every additional criteria range must have the same rows and columns as the first criteria range, criteria can be numbers/expressions/cell references/text, and an empty-cell criteria reference is treated as `0`: https://support.microsoft.com/en-us/office/countifs-function-dda3dc6e-f74e-4aee-88bc-aa8c2a866842
- Microsoft Learn documents that `SUMIF`, `SUMIFS`, `COUNTIF`, `COUNTIFS`, and `COUNTBLANK` formulas can return `#VALUE!` when they refer to cells in a closed workbook: https://learn.microsoft.com/en-us/troubleshoot/microsoft-365-apps/excel/formula-returns-value-error
- Microsoft Support count-number/date guidance supports COUNTIFS use for ranges with numeric and date criteria: https://support.microsoft.com/en-us/office/count-numbers-or-dates-based-on-a-condition-in-excel-976d0074-245d-49e6-bf5f-1207983f82ed

Luke reviewed the page direction. Final copy used the symptom-led COUNTIFS framing but avoided unsupported speed, upload, workbook-audit, human-review, affiliation, guaranteed-fix, instant, and pay-before-answer claims.

## Verification

- `npm run build:seo && npm test` passed `58/58`.
- `python3 -m json.tool vercel.json` passed.
- Live route/home/sitemap returned HTTP `200`.
- Live homepage and sitemap include `/excel-countifs-not-working/`.
- Live Stripe checkout returned HTTP `200`.
- Live desktop and mobile Playwright checks returned the expected title, H1, canonical URL, `6` checkout links, required `DATE(2026,5,1)` example, required empty-criteria copy, and `0` console/page issues.
- IndexNow accepted the new route, homepage, and sitemap with HTTP `200`.

## Next

Continue respecting the active waits: Write My Formula training/resource until `2026-05-29 10:18 UTC`, marketplace/app-template while the Someka link-exchange thread is active, consulting/support-service until `2026-05-29 16:20 UTC`, and add-in vendor until `2026-05-30 22:20 UTC`, unless replies arrive first. If no reply arrives and no gate clears, the next non-gated move should continue adding or improving high-intent formula repair surfaces only when the term has fresh evidence and a clean conversion path.

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `$35.93`.
