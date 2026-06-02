# Write My Formula Excel TEXTBEFORE / TEXTAFTER Repair Page

## Task

Ship one no-spend buyer-intent repair page for Excel `TEXTBEFORE` and `TEXTAFTER` formulas, without changing ads, payment infrastructure, DNS/account/legal/bank settings, outreach/contact forms, public posts, bulk sends, destructive production settings, or spend.

## Evidence

- Microsoft Support documents `TEXTBEFORE` and `TEXTAFTER` syntax, including `delimiter`, `instance_num`, `match_mode`, `match_end`, and `if_not_found`.
- Microsoft Support documents `#N/A` when the delimiter is not contained in the source text and `#VALUE!` for invalid `instance_num` cases.
- Current search/forum evidence showed demand around delimiter-not-found errors, `#NAME?` / unsupported-version behavior, case-sensitivity, missing fallback handling, and formulas copied between Excel versions.
- The existing Write My Formula site already had adjacent Excel text-function repair pages for `TEXTJOIN` and `TEXTSPLIT`; `excel-textbefore-textafter-not-working` filled the missing text-extraction slot.

Sources:

- Microsoft `TEXTBEFORE`: `https://support.microsoft.com/en-gb/office/textbefore-function-d099c28a-dba8-448e-ac6c-f086d0fa1b29`
- Microsoft `TEXTAFTER`: `https://support.microsoft.com/en-au/office/textafter-function-c8db2546-5b51-416a-9690-c7e6722e90b4`
- Current indexed troubleshooting evidence included Ablebits, ExcelForum, Microsoft Community Hub, and recent Reddit examples around `TEXTBEFORE` / `TEXTAFTER` delimiter, version, and extraction failures.

## Output

- Added `excel-textbefore-textafter-not-working` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/excel-textbefore-textafter-not-working/index.html`.
- Added the homepage card and sitemap entry.
- Added focused regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Captured local and live desktop/mobile screenshots under ignored verification folders:
  - `workspace/sheetpilot-workbench/output/playwright/excel-textbefore-textafter-not-working-local/`
  - `workspace/sheetpilot-workbench/output/playwright/excel-textbefore-textafter-not-working-live/`
- Committed and pushed `52ab584 Add Excel TEXTBEFORE TEXTAFTER repair page`.
- Live page: `https://writemyformula.com/excel-textbefore-textafter-not-working/`

## Verification

- `npm run build:seo` passed.
- `npm test` passed `105/105`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked claims or internal/process language in the new route or homepage card.
- Luke reviewed buyer-facing copy direction; final copy avoided unsupported upload, workbook-audit, guarantee, official-affiliation, Microsoft partner, human-reviewer, browser-local/no-data-leaves, instant, "in seconds", one-click/automatic-fix, pay-before-answer, PDF, same-day, whole-workbook, whole-spreadsheet, exact-cause, `$5`, and unsupported traction claims.
- Local desktop/mobile Chromium checks returned HTTP `200`, expected title, H1, canonical URL, `6` checkout links, required `TEXTBEFORE`/`TEXTAFTER`/`instance_num`/`Missing @` copy, and no horizontal overflow. Local static-server `POST /api/*` `501` console noise was expected.
- Production route/home/sitemap/Stripe checkout returned HTTP `200`.
- Live desktop/mobile Chromium checks returned HTTP `200`, expected title, H1, canonical URL, `6` checkout links, required `TEXTBEFORE`/`TEXTAFTER`/`instance_num`/`Missing @` copy, homepage card text, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow accepted page/home/sitemap submission with HTTP `200`.

## Gates and Budget

`config/OPEN_GATES.md` remains unchanged:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. Current cash balance remains `-$24.07`.
