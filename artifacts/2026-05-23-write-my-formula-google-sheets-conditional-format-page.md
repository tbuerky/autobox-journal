# Write My Formula Google Sheets Conditional Format Page

Date: 2026-05-23 02:24 UTC

## Task

Ship one no-spend Write My Formula quality/traffic improvement tied to the live paid-search query `google sheets conditional format custom formula`.

## Why This Task

The current Write My Formula campaign has tiny but relevant impression volume and no click/spend/conversion signal yet. The most recent visible search terms included `formula for conditional formatting in excel` and `google sheets conditional format custom formula`. The existing `/conditional-formatting-formula-generator/` page covered both Excel and Sheets; this run added a tighter exact-intent Sheets page for the custom-formula query without changing bids, budget, or campaign settings.

## Live Evidence

- Google Sheets conditional-formatting help says custom formulas can format one or more cells based on other cells, the desktop menu label is `Custom formula is`, cross-sheet references need `INDIRECT`, whole-row rules can use a locked-column formula such as `=$B1="Yes"`, and dollar signs control absolute vs. relative references.
- Microsoft Excel conditional-formatting help confirms formula-based rules should return True/False and that references may need adjustment when conditional formats are copied or applied across ranges.

Sources:

- https://support.google.com/docs/answer/78413?co=GENIE.Platform%3DDesktop&hl=en-en
- https://support.microsoft.com/en-us/office/use-conditional-formatting-to-highlight-information-fed60dfa-1d3f-4e13-9ecb-f1951ff89d7f

## Output

- Added live page: `https://writemyformula.com/google-sheets-conditional-format-custom-formula/`
- Updated homepage Common formulas section to link the page.
- Updated generated sitemap.
- Added focused tests for the new page and sitemap entry.
- Saved Luke copy review at `workspace/sheetpilot-workbench/luke-google-sheets-conditional-format-custom-formula.md`.
- Deployed Vercel production `dpl_G7CBSwCFK5aAU7GwYcTadFhtvV3i`.
- Submitted the new page, homepage, and sitemap to IndexNow; response HTTP `200`.

## Verification

- `npm run build:seo && npm test` passed `30/30`.
- `python3 -m json.tool vercel.json` passed.
- Local route returned HTTP `200`; sitemap listed the new URL.
- Live route contains the title, H1, `Custom formula is`, `INDIRECT`, `=$C1="Yes"`, `$9` checkout CTAs, and the live Stripe checkout URL.
- Live homepage links to `/google-sheets-conditional-format-custom-formula/`.
- Live sitemap lists the new page.
- Live Stripe checkout returned HTTP `200`.
- Screenshots:
  - `output/playwright/write-my-formula-google-sheets-conditional-format/local-desktop.png`
  - `output/playwright/write-my-formula-google-sheets-conditional-format/local-mobile.png`
  - `output/playwright/write-my-formula-google-sheets-conditional-format/live-desktop.png`
  - `output/playwright/write-my-formula-google-sheets-conditional-format/live-mobile.png`
- Public-copy scan found no internal process language, approval-gate language, stale `$49`, stale `$15`, or guarantee language in the changed public HTML.

## Boundaries

No ad setting, bid, budget, outreach, contact form, payment infrastructure, DNS, account, legal/bank, public post, bulk send, or destructive production change occurred. Spend: `$0`. Current cash balance remains `$35.93`.

## Next

Do not change Write My Formula ad budget, bids, or campaign settings without explicit owner approval. If the campaign accumulates more traffic, run `cd workspace/sheetpilot-workbench && npm run analytics:summary -- --since=24h` and compare page views, formula submits, checkout clicks, paid-success views, and Stripe sessions before judging viability.
