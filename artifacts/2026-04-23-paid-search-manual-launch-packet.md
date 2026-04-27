# Paid search manual launch packet

Date: 2026-04-23 14:20 UTC
Project: Profit After Fees
Current cash balance: $188.75
Approved spend cap: $50.00
Balance after full spend cap: $138.75

## What should happen now
Use the approval that already landed and get one Google Search campaign live without waiting for more back-and-forth.

Fastest safe path: the owner launches the first campaign manually outside the sandbox using the exact build spec below.

## Why this matters now
The approval bottleneck is no longer the problem.

Fresh evidence:
- The owner already replied `APPROVED PAID SEARCH TEST.` in the Discord control thread.
- The public X post at https://x.com/profitafterfees/status/2047017470582509661 still shows only `3 Views`, `0 Replies`, `0 reposts`, `0 Likes`, and `0 Bookmarks`.
- The homepage at https://profitafterfees.com/ is live, customer-facing, and ready to receive paid clicks right now.
- Workspace checks found no stored Google Ads credentials or existing Google Ads account access for AutoBox, so manual launch is the fastest path that does not require unsafe credential handling.

That means the sharpest move is not another approval packet. It is converting the existing approval into a launched campaign.

## Recommended path
Recommended choice: owner manual launch now.

Why this beats waiting:
- no new credential sharing is needed
- no payment-card handling is pushed into the sandbox
- the campaign can go live as soon as billing is attached
- AutoBox can still monitor and optimize after the first screenshots or metrics arrive

## Exact campaign build
### Campaign settings
- Campaign type: Search only
- Goal: Website traffic
- Landing page: https://profitafterfees.com/?utm_source=google&utm_medium=cpc&utm_campaign=paid-search-test-1
- Networks: Google Search only
- Turn OFF: Display Network
- Turn OFF if shown: Search Partners for the first test
- Location: United States
- Language: English
- Daily budget: $10.00
- Total run length: 5 days maximum
- Total spend cap approved: $50.00
- Bidding: Maximize clicks

### Ad group 1: Stripe fee calculator
Keywords:
- "stripe fee calculator"
- [stripe fee calculator]
- "stripe pricing calculator"
- [stripe pricing calculator]
- "how much does stripe take"
- [how much does stripe take]

### Ad group 2: Profit and margin calculator
Keywords:
- "stripe profit calculator"
- [stripe profit calculator]
- "calculate profit after stripe fees"
- [calculate profit after stripe fees]
- "stripe fee calculator digital products"
- [stripe fee calculator digital products]
- "stripe fee calculator course sales"
- [stripe fee calculator course sales]

### Negative keywords
Add at campaign level:
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

## Suggested ad copy
### Responsive search ad headlines
Use up to 15. Start with these:
- Stripe Fee Calculator
- Calculate Profit After Stripe
- Stripe Margin Calculator
- Stripe Fee + VAT Calculator
- Break-Even Price Calculator
- Profit After Fees for Digital Sales
- Model Coupons, VAT, Affiliates
- Free Digital Product Calculator
- Stripe Profit Calculator
- Calculate Real Net Profit

### Descriptions
Use up to 4. Start with these:
- See Stripe fees, VAT, coupons, affiliates, refunds, and break-even price in one free calculator.
- Free calculator for digital products, courses, templates, and micro-SaaS pricing.
- Stop guessing margin. Model your real net profit after Stripe and other sales costs.
- Share a pricing scenario with a link and compare break-even price instantly.

## Manual launch checklist
1. Log into Google Ads in a normal browser.
2. Create a new Search campaign.
3. Use the landing page URL with the UTM string above.
4. Set budget to `$10.00/day`.
5. Restrict to United States and English.
6. Turn off Display Network.
7. Add the two ad groups above.
8. Paste the headlines and descriptions above.
9. Add the negative keywords above.
10. Launch.

## What to send back immediately after launch
Reply with all of these if possible:
- Google Ads customer ID
- campaign name
- screenshot of campaign settings summary
- screenshot of keyword list
- screenshot of the first ad preview
- confirmation that billing is attached and campaign is enabled

## If manual launch is not possible today
Use this fallback only if needed:
- create the Google Ads account and attach billing outside the sandbox
- then send back either the screenshots above or a fresh instruction that AutoBox should prepare the next optimization packet before launch

## Optional later path if direct AutoBox optimization is wanted
If the owner wants AutoBox to directly tune bids/keywords later, provision a dedicated experiment Google login after the first campaign exists instead of sending personal payment details through chat.

## Decision
Approval already exists. The current bottleneck is campaign creation, not permission. The fastest revenue-oriented move now is one manual Google Search launch using this exact build spec.