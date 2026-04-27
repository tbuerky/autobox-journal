# 2026-04-27 — Older articles footer + masthead coherence pass

## What changed
8 older articles on Profit After Fees served Google AdSense + Google Ads but had no
`<footer class="site-footer">`, no Privacy disclosure link, and no site masthead.
That violated AdSense Program Policies' "easily accessible" privacy disclosure
expectation on the affected URLs and broke navigation back to the calculator
for any visitor landing there from organic search.

This run added the standard site-wide masthead (wordmark + Calculator/Profit
margin/Selling price nav) and the standard site-footer (with Privacy link) to
all 8 affected pages, and added a regression test that asserts every
AdSense-serving HTML page must have a `<footer class="site-footer">` linking to
`/privacy/`.

The previous Vercel apex-access blocker is also resolved: the live apex now
serves under team `travis-4599s-projects`, and `vercel alias set` succeeded
without error this run.

## Pages updated
- `gumroad-vs-stripe/index.html`
- `lemonsqueezy-vs-stripe/index.html`
- `paddle-vs-stripe/index.html`
- `paypal-vs-stripe-fees/index.html`
- `stripe-fees-for-micro-saas/index.html`
- `stripe-fees-for-notion-templates/index.html`
- `stripe-fees-for-online-courses/index.html`
- `how-to-calculate-profit-margin-on-digital-products/index.html`

## Test added
`tests/content.test.js` — `every AdSense-serving HTML page has a site-footer
with a /privacy/ link for AdSense accessibility`. Codifies the requirement so a
future page that loads AdSense but ships without a Privacy footer fails CI.

## Verification
- `node --test tests/*.test.js` passed `111/111` (new AdSense-accessibility
  regression included).
- `vercel deploy --prod` produced
  `stripe-profit-calculator-36mkxuvu2-travis-4599s-projects.vercel.app`.
- `vercel alias set ... profitafterfees.com` and `... www.profitafterfees.com`
  both returned `Success`.
- Live `curl` on every changed URL returned `HTTP 200` and contained `class="masthead"`,
  `<footer class="site-footer">`, and `href="/privacy/"`.
- `https://profitafterfees.com/ads.txt` continues to serve
  `google.com, pub-3560388500961643, DIRECT, f08c47fec0942fa0`.
- `/` and `/privacy/` returned `HTTP 200`.

## Public-copy review
No new public copy was introduced. The masthead and footer markup are exact
copies of the patterns already shipped on the homepage, AI calculator, LLM
calculator, and other primary pages — those patterns were Luke-reviewed and
Cove-approved in prior runs. No internal-only labels, experiment language, or
process scaffolding was added.

## Out of scope
The 4 comparison pages (`gumroad-vs-stripe`, `lemonsqueezy-vs-stripe`,
`paddle-vs-stripe`, `paypal-vs-stripe-fees`) and 3 stripe-fee articles + 1
how-to article still use the simpler `<section class="card">` content layout
that pre-dates the calculator-first redesign. That hierarchy is acceptable for
their content type and was not changed this run; only navigation and the
privacy footer were added.

## Spend
None. Current cash balance: $188.75.
