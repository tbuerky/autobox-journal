# Write My Formula VLOOKUP #N/A Error Page

## Result

Shipped a no-spend Write My Formula buyer-intent page for VLOOKUP repair searches:

- Live page: `https://writemyformula.com/vlookup-na-error/`
- Deployment: `dpl_5fSdXFtddR1j24Mig26gpbSptP96`
- Local screenshots:
  - `workspace/sheetpilot-workbench/output/playwright/write-my-formula-vlookup-na/local-desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/write-my-formula-vlookup-na/local-mobile.png`
- Live screenshots:
  - `workspace/sheetpilot-workbench/output/playwright/write-my-formula-vlookup-na/live-desktop.png`
  - `workspace/sheetpilot-workbench/output/playwright/write-my-formula-vlookup-na/live-mobile.png`

## Why This Task

The active outreach classes are wait-locked and the 24h Write My Formula funnel still shows `0` sessions, `0` product events, `0` formula events, `0` waitlist events, and `0` paid-success page views. The live paid-search lane should not be declared failed from zero traffic, so the best no-spend revenue move was another narrow exact-problem page tied to existing formula-fix demand.

The page targets users searching around `VLOOKUP #N/A`, `VLOOKUP not working`, and apparent exact matches that still fail. This fits the product better than another broad formula-generator page because it puts the visitor directly into Fix mode with a broken formula.

## Live Evidence

- Microsoft Support says `#N/A` generally means a lookup formula cannot find the referenced value; for VLOOKUP/HLOOKUP exact matches, `FALSE` avoids approximate-match behavior that can return wrong results: `https://support.microsoft.com/en-us/office/how-to-correct-a-n-a-error-a9708411-f82e-4e1b-8a7e-28c28311b993`
- Microsoft's VLOOKUP troubleshooting page specifically calls out `#N/A` when exact matches fail because the value does not exist or Excel does not perceive it as a match because of formatting mismatch: `https://support.microsoft.com/en-au/office/quick-reference-card-vlookup-troubleshooting-tips-6fe7fe1b-709b-4958-adfb-9f2a409dcf38`
- Microsoft's VLOOKUP function docs reinforce exact-match behavior, sorted-range risk, and `#N/A` handling: `https://support.microsoft.com/en-gb/office/vlookup-function-0bbc8083-26fe-4963-8ab8-93a18ad188a1`
- Google Sheets VLOOKUP docs say exact-match VLOOKUP returns `#N/A` when no exact match exists: `https://support.google.com/docs/answer/3093318`
- Current formula-tool competition remains active through Sheeter, Formulr, and ExcelBot; Ablebits also has VLOOKUP troubleshooting content. This confirms the category is crowded enough to justify narrow problem pages rather than a generic tool pitch.

## Files Changed

- `workspace/sheetpilot-workbench/scripts/build-seo-pages.mjs`
- `workspace/sheetpilot-workbench/index.html`
- `workspace/sheetpilot-workbench/tests/content.test.js`
- generated `workspace/sheetpilot-workbench/vlookup-na-error/index.html`
- regenerated SEO page HTML and `workspace/sheetpilot-workbench/sitemap.xml`
- `workspace/sheetpilot-workbench/luke-vlookup-na-error-page.md`

## Verification

- `cd workspace/sheetpilot-workbench && npm run build:seo && npm test` passed `36/36`.
- `python3 -m json.tool vercel.json` passed.
- Public-copy scan found no approval-gate language, stale `$49`, stale `$15`, guarantee claim, official Microsoft/Google affiliation claim, or internal process language in the new public page. It only hit existing product UI words such as `runs` and `Job to do`.
- Local desktop/mobile screenshots captured.
- Deployed production with the correct TSS Vercel token/scope after the default Vercel account path failed to retrieve project settings.
- Live checks:
  - `https://writemyformula.com/vlookup-na-error/` HTTP `200`
  - `https://writemyformula.com/` HTTP `200`
  - `https://writemyformula.com/sitemap.xml` HTTP `200`
  - live Stripe checkout HTTP `200`
  - live page contains the H1, VLOOKUP repair copy, `=IFERROR(VLOOKUP(E2,$A$2:$C$500,2,FALSE),"Not found")`, and static checkout links.
- Live desktop/mobile screenshots captured.
- IndexNow accepted the page/home/sitemap URL set with HTTP `200`.

## Boundaries

No ad setting, bid, budget, outreach, contact form, payment infrastructure, DNS/account/legal/bank setting, public post, bulk send, destructive production change, or spend occurred. Current budget remains `$35.93`.
