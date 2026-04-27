# Google Ads launch assets packet

Date: 2026-04-25 20:18 UTC
Project: Profit After Fees
Current cash balance: $188.75
Approved spend cap: $50.00
Projected balance after full cap: $138.75

## Operator decision
Do not add another generic SEO/support page this run. The sharper move is to reduce the owner-side Google Ads launch friction because the test is already approved, the site is live, and the first X post did not create meaningful traffic.

## What changed this run
1. Created import-ready/manual-build Google Ads CSV assets under `artifacts/paid-search-launch-assets/`.
2. Routed public-facing ad copy through Luke before using it.
3. Added a small homepage disclosure for paid-traffic compliance: `Independent calculator. Not affiliated with Stripe. Results are estimates, not tax or financial advice.`
4. Added a regression test for that disclosure.

## Asset files
- `artifacts/paid-search-launch-assets/campaign.csv`
- `artifacts/paid-search-launch-assets/ad_groups.csv`
- `artifacts/paid-search-launch-assets/keywords.csv`
- `artifacts/paid-search-launch-assets/negative_keywords.csv`
- `artifacts/paid-search-launch-assets/responsive_search_ads.csv`
- Luke copy pass: `workspace/luke_google_ads_launch_assets.md`
- Build script: `workspace/google_ads_launch_assets.py`

## Campaign settings
- Campaign name: `PAF - Search - Stripe Profit Calculator - Test 1`
- Type: Search
- Goal: Website traffic
- Network: Google Search only
- Turn off: Display Network
- Turn off if shown: Search partners
- Location: United States
- Language: English
- Budget: `$10/day`
- Hard cap: stop at `$50 total spend`
- Bid strategy: Maximize clicks
- Landing URL: `https://profitafterfees.com/?utm_source=google&utm_medium=cpc&utm_campaign=paid_search_test_1&utm_content=stripe_profit_calculator`

## Ad groups
1. `Stripe fee calculator`
2. `Profit margin calculator`
3. `Digital product pricing`

## Keywords
- `[stripe fee calculator]`
- `"stripe fee calculator"`
- `[stripe pricing calculator]`
- `"how much does stripe take"`
- `[stripe profit calculator]`
- `"stripe profit calculator"`
- `"calculate profit after stripe fees"`
- `"stripe margin calculator"`
- `"digital product pricing calculator"`
- `"course pricing calculator"`
- `"template pricing calculator"`
- `"saas pricing calculator"`

## Campaign-level negatives
- jobs
- stock
- api
- developer
- github
- code
- pdf
- template free download
- stripe login
- support phone number
- refund policy
- chargeback dispute
- stripe careers
- stripe dashboard

## Suggested post copy:
Use this as the owner-facing Google Ads build text, or import the CSV files above in Google Ads Editor.

Campaign: `PAF - Search - Stripe Profit Calculator - Test 1`
Landing URL: `https://profitafterfees.com/?utm_source=google&utm_medium=cpc&utm_campaign=paid_search_test_1&utm_content=stripe_profit_calculator`
Budget: `$10/day`, stop at `$50 total spend`.
Network: Google Search only. Display off. Search partners off if available.
Location: United States. Language: English.

Responsive search ad headlines:
1. See What You Actually Keep
2. Profit After Stripe Fees
3. Free Stripe Fee Calculator
4. What's Left After Fees?
5. Net Profit, Not Gross
6. Stripe + VAT + Coupons
7. Know Your Real Margin
8. Price It Before You Launch
9. Digital Product Math, Done
10. Break-Even In One Screen
11. Course & Template Margins
12. Fees, Tax, Affiliates, Net
13. Run The Number In Seconds
14. No Signup. No Spreadsheet.
15. Share The Scenario, Free

Descriptions:
1. Enter your price. See net profit after Stripe, VAT, coupons, affiliates, and refunds.
2. Free calculator for course, template, ebook, and SaaS sellers. No signup. Shareable.
3. Stop guessing your margin. Plug in the numbers and see what hits your account.
4. Fees, tax, payouts, delivery costs — all in one quick calculation. Free to use.

## What the owner should send back after launch
- Google Ads customer ID
- Campaign name
- Screenshot of settings summary
- Screenshot of keywords
- Screenshot of ad preview
- Confirmation that billing is attached and the campaign is enabled
- First metrics after traffic starts: clicks, impressions, CTR, average CPC, spend, search terms

## Verification
- Luke generated/reviewed the public ad copy and flagged trademark/tax-estimate risks.
- Homepage now includes the independent / estimate disclosure recommended for paid traffic.
- Google Ads copy length constraints passed: 15 headlines at <=30 chars and 4 descriptions at <=90 chars.
- CSV generation completed successfully.
- Focused content test for the new disclosure passed.
- Full site test suite passed.
- Production deploy completed and live browser QA confirmed the footer disclosure renders with no JavaScript console errors.
- Discord control-channel update delivered as message `1497695049616720082`.

## Remaining blocker
The campaign still cannot be launched inside the sandbox because Google Ads account and billing access remain owner-side. No spend was made in this run.
