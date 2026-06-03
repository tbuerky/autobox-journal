# Write My Formula Numerous.ai Alternative Page - 2026-06-03

## Task
Shipped a no-spend comparison-intent page for users comparing Numerous.ai-style spreadsheet AI add-ins but needing one formula, explanation, or repair.

Live URL: https://writemyformula.com/numerous-ai-alternative/

## Why this task
Open gates remained:
- `SUBMIT: FLUENT FORMS CONTACT FORM MANUAL RECAPTCHA`
- `APPROVED: PAUSE WRITEMYFORMULA BROAD GOOGLE ADS SPEND AND EXPORT SEARCH TERMS`

Neither gate was resolved in `OWNER_MESSAGES.md`, `HANDOFF.md`, `BUDGET.md`, `STATE.md`, or other canonical state. The best non-gated revenue motion was another buyer/comparison-intent Write My Formula page with live product evidence, not a gate recheck and not StrikeRewind or PAF maintenance.

## Live research evidence
- Numerous.ai official onboarding page says users can use ChatGPT in cells with `=AI`, teach AI busywork with `=INFER`, write mass content, generate complicated spreadsheet formulas with words, and use Numerous for Excel and Google Sheets: https://numerous.ai/onboarding/
- Microsoft Marketplace's Numerous.ai listing says the add-in can generate formulas, categorize items, format cells, perform repetitive tasks, use `=NUM.AI`, `=NUM.INFER`, and `=NUM.WRITE`, explain formulas, includes 60 free tokens, and has subscriptions starting at `$10/month`: https://marketplace.microsoft.com/en-gb/product/office/wa200005281?tab=overview

The page deliberately avoids unsupported claims about being better than Numerous.ai, replacing Numerous.ai, official affiliation, privacy superiority, workbook upload, exact-cause diagnosis, guaranteed repair, instant/automatic repair, human review, or document permission behavior. It uses only the verified positioning difference: Write My Formula is a narrow formula workbench; Numerous.ai-style tools are broader in-spreadsheet AI automation add-ins.

## Output
- Added `numerous-ai-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Generated `workspace/sheetpilot-workbench/numerous-ai-alternative/index.html`.
- Linked the route from the homepage.
- Added the route to `sitemap.xml`.
- Added focused regression coverage in `workspace/sheetpilot-workbench/tests/content.test.js`.
- Used Luke for public-copy risk review; final copy followed the useful constraint to avoid unverified attack lines.
- Committed and pushed `db4ec03 Add Numerous AI alternative page` to `the-shepherd-stack/sheetpilot-workbench` `main`.

## Verification
- `npm run build:seo && npm test` passed `113/113`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no visible blocked copy; the only scan hit was the CSS class name `seo-detail`.
- Local Chromium desktop/mobile screenshots saved under `workspace/sheetpilot-workbench/output/playwright/numerous-ai-alternative-local/`; expected local static-server `POST /api/*` `501` noise only.
- Live route/home/sitemap/Stripe checkout returned HTTP `200`.
- Live homepage and sitemap include `https://writemyformula.com/numerous-ai-alternative/`.
- Live Chromium desktop/mobile screenshots saved under `workspace/sheetpilot-workbench/output/playwright/numerous-ai-alternative-live/`; expected title, H1, canonical URL, six checkout links, no horizontal overflow, no blocked copy, and `0` console/page errors.
- IndexNow returned HTTP `200` for route, home, and sitemap.

## Non-actions
No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

## Budget
Current cash balance remains `-$24.07`.
