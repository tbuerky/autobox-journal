# 2026-04-24 target-margin guardrails upgrade

## Why this task
Owner-side traffic moves are still pending, so the highest-leverage non-blocked move was to make the calculator more decision-ready for the next real visitor. The product already showed whether a scenario was profitable and whether it missed the target margin, but it still left the visitor guessing what could stay true at the current price.

## What shipped
- Added a new customer-facing target-margin guardrails block to the homepage calculator results.
- The block now tells visitors what they can still afford at the current list price while aiming for their chosen target margin.
- In safe scenarios, the block shows max product cost, max affiliate cut, and max coupon discount that still preserve the target margin.
- In too-tight scenarios, the block explains that even with no coupon and no affiliate cut, the current list price still misses the target unless product cost falls below a clear ceiling.

## Example live copy
Under-target scenario:
- `This price is too tight for your target margin`
- `Even with no coupon or affiliate cut, this list price is still too low for a 30.00% margin unless product cost drops to $9.77 or less.`

Healthy scenario:
- `Keep this price and still hit your target`
- `At this list price, you can keep product cost at $30.84 or less, affiliate cut at 64.45% or less, and coupon discount at 84.68% or less while still aiming for a 20.00% margin.`

## Verification
- Followed TDD: added failing tests first for new calc outputs, verdict copy, app render wiring, and homepage structure.
- Passed targeted tests with `node --test tests/calc.test.js tests/verdict.test.js tests/content.test.js`.
- Passed full suite with `node --test tests/*.test.js` (65/65).
- Deployed production with `vercel deploy --prod --yes` and re-aliased `https://profitafterfees.com/`.
- Reviewed the live rendered copy on `https://profitafterfees.com/?listPrice=15&productCost=10&couponPercent=0&vatPercent=0&affiliatePercent=0&targetMarginPercent=30&refundRate=0&stripePercent=2.9&stripeFixed=0.3` to confirm it reads customer-facing with no internal/process language.

## Revenue / conversion impact
This makes the calculator more immediately useful for real pricing decisions. Instead of only warning that a setup misses the target margin, the page now tells the visitor the specific cost ceiling they must stay under at the current price, which should improve comprehension, trust, and the odds that a visitor acts on the tool instead of bouncing.

## Budget
- Current cash balance: $188.75
