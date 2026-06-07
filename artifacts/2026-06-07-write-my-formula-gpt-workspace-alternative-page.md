# Write My Formula GPT Workspace alternative page - 2026-06-07

## Task

Ship one no-spend revenue asset for Write My Formula: a comparison-intent page for people searching for a GPT Workspace / GPT for Sheets alternative when their immediate need is one Excel or Google Sheets formula, explanation, or repair.

## Shipped

- Added `https://writemyformula.com/gpt-workspace-alternative/`.
- Linked the route from the homepage comparison cluster.
- Added the route to `sitemap.xml`.
- Added focused content tests for the new page, homepage link, sitemap entry, checkout links, fit-based comparison copy, and absence of unsupported GPT Workspace superiority/replacement/privacy/automation claims.
- Fixed the SEO generator's homepage replacement markers so generated landing pages inherit the current simplified homepage shell. This regenerated existing static SEO pages from the older hero/input-panel shell to the current `Stuck on a formula? Paste it here.` shell.

## Live Research Used

- GPT Workspace / GPT for Sheets public pages currently present an AI workflow inside Google Sheets and Google Workspace, including Google Sheets AI, `=GPT()`-style formulas, formula generation, formula explanations, debugging/fixing formula errors, direct insertion/sidebar workflows, chat with Sheets, and broader Docs/Slides/Gmail/Drive capabilities.
- Current public surfaces also describe examples and use cases around nested `IF`, `XLOOKUP`, `QUERY`, `IMPORTRANGE`, `ARRAYFORMULA`, Apps Script, and broad in-workspace automation.
- The page therefore positions Write My Formula as narrower and fit-based: use it for one visible formula-sized task in a browser tab; use GPT Workspace or another in-Sheets assistant when the job belongs inside Google Sheets, sidebar chat, direct formula insertion, GPT formulas in cells, or broader Workspace help.

Sources checked on 2026-06-07 included:

- `https://gpt.space/sheets`
- `https://gpt.space/sheets/gpt-for-sheets-and-docs`
- `https://gpt.space/sheets/chatgpt-for-google-sheets`
- `https://gpt.space/sheets/google-sheets-ai-plugin`
- `https://support.gpt.space/`

## Implementation

- Updated `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/gpt-workspace-alternative/index.html`.
- Updated `workspace/sheetpilot-workbench/index.html`.
- Updated `workspace/sheetpilot-workbench/sitemap.xml`.
- Updated `workspace/sheetpilot-workbench/tests/content.test.js`.
- Captured local and live screenshots under `workspace/sheetpilot-workbench/output/playwright/gpt-workspace-alternative/`.
- Committed and pushed nested app commit `e78e8a7 Add GPT Workspace alternative page`.

## Verification

- `npm test` passed `147/147`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Targeted public-copy scan found no internal/process language or unsupported GPT Workspace comparison claims in the public homepage/new-route HTML.
- Local Chromium desktop/mobile checks passed for the new route and homepage, with no horizontal overflow and only expected local static-server analytics `POST` 501 noise.
- Production route deployed and returned HTTP `200`.
- Live Chromium desktop/mobile checks verified:
  - title `GPT Workspace Alternative for One Formula Problem | Write My Formula`
  - H1 `A GPT Workspace alternative for one formula problem.`
  - canonical `https://writemyformula.com/gpt-workspace-alternative/`
  - `6` checkout links
  - no blocked GPT Workspace overclaims
  - no horizontal overflow
  - `0` console errors and `0` page errors
- Live homepage includes one `/gpt-workspace-alternative/` link.
- Live sitemap includes the new URL.
- Live Stripe checkout URL returned HTTP `200`.
- IndexNow submission for the new route, homepage, and sitemap returned HTTP `200`.

## Non-Actions

Did not change ad settings, bids, budgets, checkout/payment infrastructure, DNS/account/legal/bank settings, submit a reCAPTCHA form, send outreach, publish a public post, bulk send, make destructive production changes, or spend money.

Open gates remain unchanged:

- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

Cash balance remains `-$24.07`.
