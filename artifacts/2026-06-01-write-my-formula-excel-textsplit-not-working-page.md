# Write My Formula Excel TEXTSPLIT Not Working Page

Run time: 2026-06-01 12:17-12:23 UTC

## Task

Ship one no-spend repair-intent page for Excel `TEXTSPLIT` formulas.

## Gate Reconciliation

`config/OPEN_GATES.md` still contains:

- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`

No owner message, handoff note, budget entry, or state file showed either gate had cleared. `/home/autoproj/.codex/handoffs/latest.md` was older than the latest completed `logs/run_codex_*` directory, so it was not used as override context.

## Choice Rationale

At `2026-06-01 12:17 UTC`, Write My Formula training/resource outreach was wait-locked until `2026-06-04 10:24 UTC`, consulting/support-service was wait-locked until `2026-06-01 16:20 UTC`, add-in-vendor was wait-locked until `2026-06-02 22:20 UTC`, and marketplace/app-template remained in the Someka link-exchange reply wait. The best non-gated revenue motion was another high-intent repair page.

`excel-textsplit-not-working` is adjacent to the existing Excel text/dynamic-array repair cluster and maps to a specific modern Excel failure mode: wrong delimiters, row-versus-column split direction, `#SPILL!`, `#N/A` padding, and `#NAME?` / version support.

## Live Evidence

- Microsoft Support `TEXTSPLIT` docs returned HTTP `200` and documented `TEXTSPLIT`, `row_delimiter`, `match_mode`, and `pad_with`.
- Current search evidence showed repair demand around `TEXTSPLIT` not splitting, `#SPILL!`, `#N/A` padding, delimiter mismatch, and version support.
- Luke reviewed buyer-facing copy direction. Final copy used the specific `TEXTSPLIT` failure framing but avoided unsupported upload, workbook-audit, guarantee, official-affiliation, Microsoft partner, human-reviewer, browser-local/no-data-leaves, instant, one-click, automatic-fix, pay-before-answer, PDF, same-day, and whole-spreadsheet claims.

## Output

Created and shipped:

- `https://writemyformula.com/excel-textsplit-not-working/`
- `workspace/sheetpilot-workbench/excel-textsplit-not-working/index.html`
- `workspace/sheetpilot-workbench/luke-excel-textsplit-not-working-page.md`

Updated:

- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
- `workspace/sheetpilot-workbench/index.html`
- `workspace/sheetpilot-workbench/sitemap.xml`
- `workspace/sheetpilot-workbench/tests/content.test.js`
- regenerated static SEO pages so their homepage-card sections include the new route

Commit: `196cd3e Add Excel TEXTSPLIT repair page`, pushed to `main`.

## Verification

- `npm run build:seo && npm test` passed `98/98`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no blocked overclaims for the new page or homepage card.
- Local Chromium desktop/mobile screenshots captured under `workspace/sheetpilot-workbench/output/playwright/excel-textsplit-not-working-local/`.
- Live route, homepage, sitemap, and Stripe checkout returned HTTP `200`.
- Live homepage and sitemap include `excel-textsplit-not-working`.
- Live Chromium desktop/mobile screenshots captured under `workspace/sheetpilot-workbench/output/playwright/excel-textsplit-not-working-live/`.
- Live browser checks returned expected title, H1, canonical URL, `6` checkout links, required `TEXTSPLIT` and `pad_with` copy, no horizontal overflow, and `0` console/page errors.
- IndexNow accepted page/home/sitemap with HTTP `200`.

## Guardrails

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, public post, bulk send, destructive production change, or spend occurred. The pre-existing uncommitted `workspace/sheetpilot-workbench/README.md` outreach-ledger change was left untouched.

## Next Wait

Respect active waits. Consulting/support-service becomes eligible at `2026-06-01 16:20 UTC`; add-in-vendor remains locked until `2026-06-02 22:20 UTC`; training/resource remains locked until `2026-06-04 10:24 UTC` unless Learn Excel Now, Excel Campus, ProfessionalsExcel, or TrumpExcel replies first.

## Budget

Spend: `$0`. Current cash balance remains `$35.93`.
