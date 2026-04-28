# PAF Lemon Squeezy vs Stripe SEO-scaffolding leak fix

Date: 2026-04-29
Page: https://profitafterfees.com/lemonsqueezy-vs-stripe/

## What was wrong

The hero subhead ended with this sentence:

> Some buyers search lemonsqueezy vs stripe without the space, but the real choice is still convenience versus control.

This is SEO-scaffolding language — internal process talk about how visitors type the search query. It signals to a skeptical buyer that the page was written for Google, not for them. Direct violation of `RULES.md` rule 14 ("Never ship internal-facing copy, experiment notes, SEO scaffolding labels, or process language on a public page") on a page already serving Google Ads + AdSense paid traffic.

A site-wide audit confirmed this was the only occurrence of search-query / spelling-variant / SEO-process leak language across all HTML pages.

## What changed

`workspace/stripe-profit-calculator/lemonsqueezy-vs-stripe/index.html` — subhead replaced via the Luke route with a customer-facing rewrite that names the actual decision (merchant-of-record convenience vs billing control) and ends in a way that makes opening the calculator the obvious next step:

> The real question is whether merchant-of-record convenience is worth more to you than control over your billing — Lemon Squeezy absorbs VAT, refunds, and checkout plumbing for a higher cut, while Stripe leaves you with deeper subscription, pricing, and lifecycle control for a thinner one. If you are comparing them on headline fees alone, your margin math is missing what actually happens to a software sale after VAT, refunds, coupons, license keys, and partner payouts come out. Open the calculator with your own price and see which one leaves more in your pocket.

Two factual flags Luke raised were handled before applying:
- "affiliate structure" (in the original) is a stretch for native Stripe — swapped to "lifecycle control" in the rewrite.
- "the calculator below" was inaccurate — this page only links to the homepage calculator via a CTA button, so the rewrite uses "Open the calculator with your own price" instead.

`workspace/stripe-profit-calculator/tests/content.test.js` — added a new regression `no HTML page references how visitors search, type, or spell their query (SEO scaffolding)` that walks every HTML page and asserts none of these patterns can drift back:

- `/without the space/i`
- `/(some|other|many) (buyers|readers|shoppers|founders|users|visitors) search/i`
- `/search [a-z][a-z-]+ vs [a-z][a-z-]+/i`

The Lemon Squeezy comparison-page existence test was loosened from `/your margin math is wrong/i` to `/your margin math is (wrong|missing)/i` to allow Luke's stronger rewrite without weakening the customer-facing-claim assertion.

## Verification

- `node --test tests/*.test.js` → `110/110` passed (was `109/109` net `+1` from the new regression; existing comparison-page test still passes against the rewritten subhead).
- `vercel deploy --prod --yes` → `dpl_F1qZWYQWBQQz6UBcfwV4jmYBo5M1`; aliased to `https://profitafterfees.com`.
- Live HTTP: `/`, `/lemonsqueezy-vs-stripe/`, `/paddle-vs-stripe/`, `/gumroad-vs-stripe/`, `/paypal-vs-stripe-fees/`, `/privacy/`, `/ads.txt`, `/sitemap.xml` all `HTTP 200`.
- `curl https://profitafterfees.com/lemonsqueezy-vs-stripe/ | grep -ic "without the space|some buyers search|search lemonsqueezy"` → `0`.
- `curl https://profitafterfees.com/lemonsqueezy-vs-stripe/ | grep -c "your margin math is missing"` → `1`.
- IndexNow POST for `/lemonsqueezy-vs-stripe/` → `HTTP 200`.

## Why now

Owner-side gates remain open across PAF AdSense, Smart Bidding strategy + spend, StrikeSight rotation/provider/domain, and the AI margin post URL. Per the wakeup brief, the highest-leverage no-spend operator move is still public-copy quality control on the live paid-traffic surface rather than another internal doc or another SEO page. Today's prior runs fixed the conversion-tracking signal and rewrote meta self-justification copy on three other AdSense-serving older articles; this run closes the next adjacent rule-14 violation found in audit on a fourth.

Cash balance: $188.75. No spend.
