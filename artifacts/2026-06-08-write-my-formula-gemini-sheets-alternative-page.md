# Write My Formula Gemini In Sheets Alternative Page

## Task

Shipped one non-gated revenue motion for Write My Formula: a buyer-intent comparison page at `https://writemyformula.com/gemini-sheets-alternative/`.

## Why this task

The active owner-facing gates remain:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

Marketplace/app-template outreach remains wait-locked until `2026-06-10 08:17 UTC`, and consulting/support-service outreach remains wait-locked until `2026-06-11 02:20 UTC` unless a relevant prospect replies first. The best non-gated revenue move was a fresh comparison-intent page against a high-awareness spreadsheet AI workflow with live official evidence: Gemini in Google Sheets.

## Live Research

Sources used:

- Google Docs Editors Help: `https://support.google.com/docs/answer/14218565`
- Google Workspace blog, March 10, 2026: `https://blog.google/products-and-platforms/products/workspace/gemini-google-sheets-state-of-the-art/`
- Google Workspace Updates, September 2025: `https://workspaceupdates.googleblog.com/2025/09/smarter-natural-formula-generation-gemini-sheets.html`
- Google Workspace Gemini in Sheets resource page: `https://workspace.google.com/resources/spreadsheet-ai/`

Current Gemini in Sheets evidence:

- Google Help says Gemini in Sheets can create formulas and tables, generate data analysis and insights, build charts and graphs, summarize files from Drive and emails from Gmail, and perform sheet actions including conditional formatting, pivot tables, dropdowns/checkboxes, sorting/filtering, find-and-replace, number formats, row/column operations, fill ranges, and table formatting.
- Google's 2026 Workspace blog says newer Gemini in Sheets beta features help users create, organize, and edit entire sheets from natural-language instructions, and cites SpreadsheetBench performance context.
- Google Workspace Updates says Gemini formula generation became more conversational, with formula failure explanations and corrected-formula generation.

## Public Copy Boundary

Luke reviewed the comparison direction. Final copy frames the page as a scope and workflow choice:

- Use Write My Formula when the job is one Excel or Google Sheets formula, explanation, or repair in a browser tab.
- Use Gemini in Sheets or another Workspace AI workflow when the user wants AI inside Google Sheets for tables, charts, formatting, pivots, filters, Drive/Gmail context, whole-sheet organization, or broader spreadsheet edits.

The final page avoids claiming Write My Formula replaces Gemini, is better/faster/cheaper/more accurate than Gemini, is officially affiliated with Google or Gemini, reads the user's sheet automatically, inserts formulas directly, works inside Google Sheets, summarizes Drive/Gmail, uploads workbooks, audits whole spreadsheets, guarantees output, provides human review, gives exact root-cause diagnosis, provides same-day/PDF work, or has privacy superiority.

## Files Changed

- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
- `workspace/sheetpilot-workbench/index.html`
- `workspace/sheetpilot-workbench/gemini-sheets-alternative/index.html`
- `workspace/sheetpilot-workbench/sitemap.xml`
- `workspace/sheetpilot-workbench/tests/content.test.js`
- Local Luke note: `workspace/sheetpilot-workbench/luke-gemini-sheets-alternative.md` (ignored, not committed)

Nested app commit:

- `916cae55 Add Gemini in Sheets alternative page`

## Verification

- `npm run build:seo` passed.
- `npm test` passed `153/153`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Targeted public-copy scan found no internal/process copy or blocked Gemini comparison claims in the homepage or new route.
- Local desktop/mobile Chromium checks returned expected title, H1, canonical URL, six checkout links, Gemini detail copy, boundary copy, no blocked copy, no horizontal overflow, and no non-local-static-server console/page errors.
- Live route, homepage, sitemap, and actual Stripe checkout returned HTTP `200`.
- Live homepage and sitemap include the new route.
- Live desktop/mobile Chromium checks returned expected title, H1, canonical URL, six checkout links, Gemini detail copy, boundary copy, no blocked copy, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow submission for the new route, homepage, and sitemap returned HTTP `200`.

## Permission And Budget

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current budget balance remains `-$24.07`.
