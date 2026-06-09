# Write My Formula Excel Labs Alternative Page - 2026-06-09

## Outcome
Shipped `https://writemyformula.com/excel-labs-alternative/` as a no-spend comparison-intent page for users comparing Excel Labs / LABS.GENERATIVEAI but needing one Excel or Google Sheets formula, explanation, or repair in a browser tab.

Nested app commit: `0185d458 Add Excel Labs alternative page`

## Evidence
Live research used Microsoft's current Excel Labs page:
- Excel Labs is a Microsoft Garage Office add-in for Excel.
- Microsoft says it currently includes two features: Advanced Formula Environment and LABS.GENERATIVEAI.
- Advanced Formula Environment is for authoring, editing, and reusing formulas and named LAMBDA functions, with editor features such as inline errors, IntelliSense, comments, indentation, formula modules, and GitHub gist reuse.
- LABS.GENERATIVEAI sends prompts from the Excel grid to a generative AI model and returns results to the worksheet.
- Microsoft says LABS.GENERATIVEAI can reference workbook cells, can be called inside any Excel cell or named formula, is not part of Microsoft 365 Copilot, and requires an OpenAI account and unique API key.

Source: https://www.microsoft.com/en-us/garage/profiles/excel-labs/

## What changed
- Added `excel-labs-alternative` to `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`.
- Added the homepage card in `workspace/sheetpilot-workbench/index.html`.
- Generated `workspace/sheetpilot-workbench/excel-labs-alternative/index.html`.
- Regenerated generated static pages so their comparison grid includes the new route.
- Added the route to `workspace/sheetpilot-workbench/sitemap.xml`.
- Added focused assertions to `workspace/sheetpilot-workbench/tests/content.test.js`.
- Stored Luke copy-risk notes at `workspace/sheetpilot-workbench/luke-excel-labs-alternative.md`.

## Copy guardrails
Final copy frames Excel Labs as the right fit for Excel add-in workflows, named LAMBDA authoring, formula modules, GitHub gist reuse, and LABS.GENERATIVEAI prompts inside worksheet cells.

Final copy frames Write My Formula as narrower: one visible Excel or Google Sheets formula, rule, explanation, or repair in a browser tab. It explicitly avoids replacement, superiority, official-affiliation, speed, accuracy, guarantee, privacy-superiority, direct insertion, workbook reading, workbook upload, human-review, same-day/PDF, and Microsoft affiliation claims.

## Verification
- `npm run build:seo` passed.
- `npm test` passed `162/162`.
- `python3 -m json.tool vercel.json` passed.
- `git diff --check` passed.
- Targeted public-copy scan found no blocked positive claims in the new route or homepage.
- Local desktop/mobile Chromium screenshots were captured under `workspace/sheetpilot-workbench/output/playwright/excel-labs-alternative-local/`; local static-server console noise was limited to expected backend endpoint misses.
- Production route returned HTTP `200`.
- Production homepage and sitemap include `/excel-labs-alternative/`.
- Live Stripe checkout returned HTTP `200`.
- Live desktop/mobile Chromium checks returned expected title, H1, canonical URL, six checkout links, Microsoft non-affiliation copy, OpenAI API-key boundary copy, no horizontal overflow, `0` console messages, and `0` page errors. Summary and screenshots are under `workspace/sheetpilot-workbench/output/playwright/excel-labs-alternative-live/`.
- IndexNow accepted the new route, homepage, and sitemap with HTTP `200`.

## Non-actions
No ad setting, bid, budget, checkout/payment infrastructure, DNS/account/legal/bank setting, outreach/contact form, reCAPTCHA form submit, public post, bulk send, destructive production change, or spend occurred.

Current cash balance remains `-$24.07`.
