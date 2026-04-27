# Owner afternoon priority list

Date: 2026-04-26 12:16 UTC
Current cash balance: $188.75

## Why this packet exists
Travis said he has dedicated time this afternoon and asked for the tightest list of direct interactions that would move the projects forward. The highest-leverage use of that time is not more internal site work. It is getting live traffic, external feedback, or a clean approval decision on the current bottlenecks.

## Priority 1 — Launch the already-approved Google Ads test for Profit After Fees

Time needed: 20-35 minutes.
Spend gate: already approved previously up to $50 total. Stop at $50 total spend.
Primary asset: `https://profitafterfees.com/`
Prepared files: `artifacts/paid-search-launch-assets/`

Why this is first: Profit After Fees is polished enough for first paid intent traffic, but the sandbox does not have Google Ads account/billing access. This is the fastest route to real searchers, CPC data, click-through data, and search-term learning.

Use these exact settings:

- Campaign name: `PAF - Search - Stripe Profit Calculator - Test 1`
- Type: Search
- Goal: Website traffic
- Network: Google Search only
- Turn off Display Network
- Turn off Search partners if the option appears
- Location: United States
- Language: English
- Budget: `$10/day`
- Hard cap: stop at `$50 total spend`
- Bid strategy: Maximize clicks
- Landing URL: `https://profitafterfees.com/?utm_source=google&utm_medium=cpc&utm_campaign=paid_search_test_1&utm_content=stripe_profit_calculator`

Ad groups:
1. `Stripe fee calculator`
2. `Profit margin calculator`
3. `Digital product pricing`

Keywords:
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

Campaign-level negatives:
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

Send back after launch:
- Google Ads customer ID
- Campaign name
- screenshot of settings summary
- screenshot of keywords
- screenshot of ad preview
- confirmation billing is attached and campaign is enabled
- first metrics when available: clicks, impressions, CTR, average CPC, spend, search terms, disapprovals if any

## Priority 2 — Decide the AI utility standalone-domain gate

Time needed: 1 minute for approval/decline, 5-10 minutes if Travis buys it manually.
Spend gate: requires explicit approval before any purchase.
Recommended domain: `aifeaturecost.com`
Estimated price checked: Porkbun `.com` at `$11.08`; approval cap requested at `$15`.

Why this is second: The AI Feature Cost Calculator and AI Model Pricing Index are live and useful, but `profitafterfees.com` is a mismatch for AI/SaaS builder distribution. A clean standalone domain should improve trust before a serious AI-builder feedback push.

Reply with exactly one:

- `APPROVED: BUY AIFEATURECOST.COM, MAX $15`
- `DECLINED: KEEP AI TOOL ON PROFITAFTERFEES.COM FOR NOW`

If approved, AutoBox will buy only that domain if checkout is `$15` or less, connect it to Vercel, route the AI calculator/index under it, update canonical/sitemap/share metadata, deploy, and submit IndexNow.

If declined, no problem: use Priority 3's no-spend feedback post under the current URL.

## Priority 3 — Publish the AI Feature Cost Calculator feedback post

Time needed: 2-5 minutes.
Spend gate: none.
Best channel: X or LinkedIn from whichever public account Travis is comfortable using.
Current URL: `https://profitafterfees.com/ai-feature-cost-calculator/`

Why this is third: The AI utility needs builder feedback before more buildout. One public post can tell us whether anyone recognizes the pain around token cost, margin, break-even, and pricing for AI features.

Suggested post copy:
Free calculator to sanity-check AI feature margins before token costs surprise you.

Enter model rates, tokens, usage, and price. See cost per user, gross margin, break-even, and target-margin price.

https://profitafterfees.com/ai-feature-cost-calculator/

After posting, send back:
- public post URL
- any replies or DMs with concrete feedback
- if possible, one screenshot after a few hours showing views/replies/likes

## Priority 4 — If Google Ads is blocked, publish one zero-spend Profit After Fees post instead

Time needed: 2-5 minutes.
Spend gate: none.
Use only if Google Ads account/billing setup is blocked or too slow today.

Post copy:

If you sell templates, courses, ebooks, or small SaaS plans, your list price is not your take-home.

I built a free calculator that shows what you keep after Stripe fees, refunds, discounts, VAT, affiliate cuts, and product costs.

https://profitafterfees.com/

Send back:
- public post URL
- any early replies or metrics

## What I would not spend Travis time on today

- More generic SEO pages.
- More internal planning docs.
- Indie Hackers unless Travis strongly wants to use it; previous evidence made it a poor default because of subscription/community-warmup friction.
- More visual polishing before traffic. The bottleneck is now distribution/evidence.

## Best possible afternoon outcome

1. Google Ads test is live or screenshots show the exact blocker.
2. AI domain decision is resolved.
3. At least one public feedback post is live for the AI calculator if the domain is declined or not handled today.

That gives the next AutoBox run real traffic data, a concrete blocker, or builder feedback instead of another guess.
