# Write My Formula Equals Alternative Page

## Task

Shipped one non-gated revenue motion for Write My Formula: a buyer-intent comparison page at `https://writemyformula.com/equals-alternative/`.

## Why this task

The active owner-facing gates remain:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

Marketplace/app-template outreach remains wait-locked until `2026-06-10 08:17 UTC`, and consulting/support-service outreach remains wait-locked until `2026-06-11 02:20 UTC` unless a relevant prospect replies first. The best non-gated revenue move was another distinct comparison-intent page against a proven connected-spreadsheet / AI analytics product.

## Live Research

Sources used:

- Equals homepage: `https://equals.com/`
- Equals pricing: `https://equals.com/pricing/`
- Equals Google Sheets docs: `https://docs.equals.com/docs/google-sheets`
- Equals getting-started docs: `https://docs.equals.com/docs/getting-started`

Current Equals evidence:

- Equals positions around trusted AI analytics, a BI spreadsheet connected directly to data, dashboards, Slack pushes, live Notion/Coda/wiki embeds, AI report-building and question-answering, CRM writeback, and GTM data synced into a managed Snowflake warehouse.
- The current pricing page lists Essential at `$24k/year`, Business at `$36k/year`, and Enterprise at `$60k/year`, with included monthly AI spend and connector/warehouse differences.
- Listed connectors include Stripe, HubSpot, Salesforce, Postgres, BigQuery, Snowflake, and other accounting, analytics, billing, CRM, database, support, and warehouse systems.
- Equals Google Sheets docs say only raw values carry over, not formulas or formats.
- Equals docs say AI Assist can help write, edit, and fix SQL queries, formulas, charts, and more directly from an Equals workbook.

## Public Copy Boundary

Luke reviewed the comparison direction. Final copy frames the page as a scope choice:

- Use Write My Formula when the job is one Excel or Google Sheets formula, explanation, or repair in a browser tab.
- Use Equals or another BI spreadsheet when the user needs connected company data, dashboards, AI analytics, Slack/wiki publishing, warehouse sync, live connectors, CRM writeback, or managed analytics implementation.

The final page avoids claiming Write My Formula replaces Equals, is better/faster/cheaper/more accurate than Equals, is officially affiliated with Equals, has privacy superiority, uploads or audits workbooks, guarantees output, provides human review, provides same-day/PDF work, or attacks Equals as bloated/overpriced/overkill.

## Files Changed

- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
- `workspace/sheetpilot-workbench/index.html`
- `workspace/sheetpilot-workbench/equals-alternative/index.html`
- `workspace/sheetpilot-workbench/sitemap.xml`
- `workspace/sheetpilot-workbench/tests/content.test.js`
- Local Luke note: `workspace/sheetpilot-workbench/luke-equals-alternative-copy.md` (ignored, not committed)

Nested app commit:

- `7bb73764 Add Equals alternative page`

## Verification

- `npm run build:seo && npm test` passed `154/154`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Targeted public-copy scan found no internal/process copy or blocked Equals comparison claims in the homepage or new route.
- Local desktop/mobile Chromium checks returned expected title, H1, canonical route copy, six checkout links, Equals detail/pricing/import copy, no blocked copy, no horizontal overflow, and no non-local-static-server console/page errors.
- Live route, homepage, sitemap, and actual Stripe checkout returned HTTP `200`.
- Live homepage and sitemap include the new route.
- Live desktop/mobile Chromium checks returned expected title, H1, six checkout links, Equals detail/pricing/import copy, no blocked copy, no horizontal overflow, `0` console messages, and `0` page errors.
- IndexNow submission for the new route, homepage, and sitemap returned HTTP `200`.

## Permission And Budget

No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current budget balance remains `-$24.07`.
