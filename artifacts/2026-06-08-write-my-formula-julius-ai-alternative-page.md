# Write My Formula Julius AI Alternative Page

## Task

Shipped one non-gated revenue motion for Write My Formula: a buyer-intent comparison page at `https://writemyformula.com/julius-ai-alternative/`.

## Why this task

The active owner-facing gates remain:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

Marketplace/app-template outreach remains wait-locked until `2026-06-10 08:17 UTC`, and consulting/support-service outreach remains wait-locked until `2026-06-11 02:20 UTC` unless a relevant prospect replies first. The best non-gated revenue move was another distinct comparison-intent page for a live, high-awareness spreadsheet/data-analysis AI product not already covered.

## Live research

Sources used:

- `https://julius.ai/home/excel-ai`
- `https://julius.ai/pricing`

Current Julius AI evidence:

- Julius positions its Excel/Sheets surface around analyzing Excel and Google Sheets, creating charts, generating formulas, and using natural language.
- Its Excel AI page describes formula generation from simple text instructions, charts and graphs, aggregations and insights, advanced analysis, reports, PDF table extraction, data-file assistance, line/pie graphs, spreadsheet preparation, and data cleanup/splitting.
- Its pricing page presents Julius as AI-powered data agents with Free, Plus `$20/month`, Pro `$45/month`, Max `$200/month`, Ultra `$500/month`, Business `$450/month`, and Growth `$750/month` tiers.
- Its pricing page also lists Google Drive, OneDrive, SharePoint, Snowflake, BigQuery, Postgres, file intake formats, exports for slides/HTML/charts/images, custom agents, Slack agent use, scheduled report runs, and dashboard/team controls.

## Public copy boundary

Luke reviewed the buyer-facing copy direction. Final copy frames the page as a task-size choice:

- Use Write My Formula when the job is one Excel or Google Sheets formula, explanation, or repair.
- Use Julius AI or a similar data-agent workspace for workbook, CSV, PDF, database, chart, export, scheduled-report, connector, or broader exploratory data-analysis workflows.

The final page avoids claiming Write My Formula replaces Julius AI, is better/faster/cheaper/more accurate/more private, has official affiliation, uploads workbooks, audits whole spreadsheets, automatically fixes formulas, guarantees output, provides human review, gives exact root-cause diagnosis, or delivers same-day/PDF work.

## Files changed

- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
- `workspace/sheetpilot-workbench/index.html`
- `workspace/sheetpilot-workbench/julius-ai-alternative/index.html`
- `workspace/sheetpilot-workbench/sitemap.xml`
- Generated static pages updated with the new homepage comparison card.
- `workspace/sheetpilot-workbench/tests/content.test.js`
- Local Luke note: `workspace/sheetpilot-workbench/luke-julius-ai-alternative.md`

Nested app commit:

- `f67c54f Add Julius AI alternative page`

## Verification

- `npm run build:seo` passed.
- `npm test` passed `151/151`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Targeted public-copy scan found no internal/process copy or blocked Julius AI comparison claims.
- Live route `https://writemyformula.com/julius-ai-alternative/` returned HTTP `200`.
- Live homepage returned HTTP `200` and includes the new route.
- Live sitemap returned HTTP `200` and includes the new route.
- Existing Stripe checkout URL returned HTTP `200`.
- Live desktop/mobile Chromium checks returned expected title, H1, canonical URL, six checkout links, Julius AI detail copy, no blocked copy, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow submission for the new route, homepage, and sitemap returned HTTP `200`.

## Permission and budget

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current budget balance remains `-$24.07`.
