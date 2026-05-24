# Write My Formula Google Ads Broadening Packet - 2026-05-24

## Decision

Prepared an import-ready Google Ads broadening packet for the live campaign `WMF - Formula Specific Search - $15 Test` (`23861003751`) in account `534-805-0350`.

No live Google Ads change was applied from this box because the repo has Gmail tooling, Vercel tooling, and Stripe tooling, but no Google Ads API client or authenticated campaign-management path.

## Why this task

Fresh owner input on 2026-05-24 reported the campaign was enabled but inventory/query-limited, not budget-limited:

- Visible range: `2026-04-25` to `2026-05-23`
- Totals: `16` impressions, `0` clicks, `$0.00` spend, `0` conversions
- Many exact/phrase formula-generator keywords marked `Not eligible: Low search volume`
- Live impressions concentrated in pain terms, especially `fix my excel formula`, `formula for conditional formatting`, and `excel data validation formula`

Google's own low-search-volume guidance says too-specific keywords can be addressed by finding additional ideas, broadening match type, or using less-specific wording. Google's keyword matching guidance says broad match can reach related searches beyond exact/phrase.

## Output

Created:

- `workspace/sheetpilot-workbench/ads/google-search-broadening-2026-05-24.md`
- `workspace/sheetpilot-workbench/ads/google-ads-editor-keywords-2026-05-24.csv`
- `workspace/sheetpilot-workbench/ads/google-ads-editor-rsa-2026-05-24.csv`
- `workspace/sheetpilot-workbench/ads/google-ads-editor-negative-keywords-2026-05-24.csv`

Updated:

- `workspace/sheetpilot-workbench/ads/google-search-test.md`

The packet adds `66` keyword rows, `2` new responsive-search-ad rows for new help-intent ad groups, and `12` new campaign-level negative keyword rows.

## Scope

The recommended change:

- Adds phrase and broad variants around live pain terms.
- Preserves the current campaign's bounded-spend shape.
- Does not change budget.
- Does not change CPC cap.
- Does not change bidding strategy.
- Does not change locations, networks, Search partners, Display, conversion setup, DNS, checkout, or public site copy.

Primary keyword expansion areas:

- Existing `AG08 - Formula Fixer`: fix my Excel formula, Excel formula not working, formula error, not calculating, not showing result, fix Google Sheets formula.
- Existing `AG06 - Conditional Formatting`: formula for conditional formatting, conditional formatting formula, custom formula conditional formatting, Sheets conditional formatting formula.
- Existing `AG07 - Data Validation`: Excel data validation formula, custom data validation formula, Sheets data validation formula.
- New `AG09 - Excel Formula Help`: Excel formula help, help with Excel formula, write/create Excel formula, formula from text.
- New `AG10 - Google Sheets Formula Help`: Google Sheets formula help, fix/write Sheets formula, formula from text.

## Verification

CSV parse validation passed:

- `google-ads-editor-keywords-2026-05-24.csv`: `66` rows, `6` columns, consistent widths.
- `google-ads-editor-rsa-2026-05-24.csv`: `2` rows, `26` columns, consistent widths.
- `google-ads-editor-negative-keywords-2026-05-24.csv`: `12` rows, `5` columns, consistent widths.

Live landing page checks returned HTTP `200`:

- `https://writemyformula.com/excel-formula-fixer/`
- `https://writemyformula.com/excel-formula-generator/`
- `https://writemyformula.com/google-sheets-formula-generator/`
- `https://writemyformula.com/conditional-formatting-formula-generator/`
- `https://writemyformula.com/data-validation-formula-generator/`
- `https://writemyformula.com/excel-formula-not-showing-result/`
- `https://writemyformula.com/google-sheets-conditional-format-custom-formula/`

24h first-party funnel summary still showed:

- `0` sessions
- `0` analytics events
- `0` formula events
- `0` waitlist events
- `0` paid-success views
- `0` paid Stripe sessions

## Gate

New owner/action gate:

`APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`

This is not a decision request; Travis already directed the campaign broadening. It is the remaining account-access/manual-application step because Codex does not have Google Ads campaign-management access in this repo.

## Sources

- Google Ads Help, keyword matching options: `https://support.google.com/google-ads/answer/7478529`
- Google Ads Help, low search volume keyword status: `https://support.google.com/google-ads/answer/2616014`
- Google Ads API keyword match type enum: `https://developers.google.com/google-ads/api/reference/rpc/v22/KeywordMatchTypeEnum.KeywordMatchType`

## Budget

No spend occurred in this run. Budget remains `$35.93`.
