# Google Ads first-metrics and stop-loss packet

Date: 2026-04-26 20:17 UTC
Project: Profit After Fees
Current cash balance: $188.75
Approved paid-search cap: $50.00 total spend
Active guardrail: Google Ads accepted `$10/day` but no total campaign cap was available, so Travis must manually pause/stop before or at `$50` spend.

## Operator decision
The highest-leverage move now is not another page or another internal plan. The paid-search test is the live/near-live acquisition lane, and the business needs the first real search data without accidentally overrunning the $50 cap.

This packet turns the next owner-side Ads check into a revenue/traffic decision: continue learning, add negatives, fix policy issues, or stop before waste.

## What to do now
Open Google Ads for campaign `PAF - Search - Stripe Profit Calculator - Test 1` and send back one status line plus screenshots.

Use this exact reply format:

```text
ADS STATUS:
Campaign status: <enabled / eligible / learning / under review / limited / disapproved / paused>
Total spend so far: $<amount>
Budget: $10/day
Clicks: <number>
Impressions: <number>
CTR: <percent>
Avg CPC: $<amount>
Conversions shown by Google Ads, if any: <number and conversion name>
Search terms visible yet: <yes/no>
Any policy or asset warnings: <exact text>
Paused? <yes/no>
Screenshots attached: campaign overview, keywords, search terms if visible, ads/assets/policy warning if any
```

## Stop-loss rules
1. Pause immediately at `$50.00` total spend. Do not let the campaign keep running because Google Ads has no total cap in this setup.
2. If spend is `$40+`, pause unless there is a clear reason to continue and Travis explicitly decides to keep spending.
3. If spend reaches `$20+` with zero clicks, pause and send screenshots of keywords, bid/budget warnings, and policy status.
4. If spend reaches `$20+` with clicks but no useful search terms, send the metrics before changing the campaign.
5. If search terms show irrelevant intent, add negatives before continuing. Examples to negate: jobs, careers, developer API, login/support, chargeback/refund disputes, stock/investor terms, PDFs/templates/free downloads.

## First optimization rules after data arrives
- If CTR is below 2% after at least 200 impressions, send the search terms and ad preview before changing copy.
- If average CPC is above `$3.00` before 10 clicks, pause and report; the $50 test will not buy enough learning at that price.
- If one ad group spends 2x another with worse intent, pause the weaker ad group.
- If a policy warning appears, send the exact warning text. Do not rewrite ads blindly; the landing page already includes the independent/estimate disclosure.
- If a relevant term produces clicks, keep exact/phrase variants around that term and cut broad or ambiguous terms.

## Evidence already in place
- Landing page: `https://profitafterfees.com/?utm_source=google&utm_medium=cpc&utm_campaign=paid_search_test_1&utm_content=stripe_profit_calculator`
- Google Ads tag `AW-18121518600` is live on the homepage and all sitemap HTML pages.
- Live check at 2026-04-26 20:17 UTC returned HTTP 200 for `https://profitafterfees.com/` and found the Ads tag in the page HTML.
- Google Ads logo/image assets are live under `/google-ads/` if asset review needs them.
- Import/manual-launch assets remain available under `artifacts/paid-search-launch-assets/`.

## Next decision after Travis replies
- Under review with no spend: wait for review, but capture warning text if shown.
- Disapproved: fix only the policy reason and resubmit.
- Spending with irrelevant terms: add negatives and continue only if still below the cap.
- Spending with relevant clicks: evaluate CPC/CTR/search terms, then decide whether a second $50 test is worth requesting.
- Spend near cap: pause first, then analyze.

No sandbox spend occurred in this run. Budget ledger stays at `$188.75` until Travis reports actual Google Ads spend or revenue.
