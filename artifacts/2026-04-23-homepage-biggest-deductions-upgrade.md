# 2026-04-23 homepage biggest deductions upgrade

## Objective
Make the calculator easier to act on after the first glance by showing which costs are taking the biggest bite out of each sale.

## Why this move now
Traffic execution is still partly owner-side, so the best non-blocked move was to improve the product itself for the next visitor instead of creating more internal docs. The quick-read verdict already answers whether a scenario works. This upgrade answers the next practical question: what is actually eating the margin.

## What shipped
- Added a new `Biggest deductions` block directly under the quick-read verdict.
- Ranked and displayed the top cost drivers for each scenario using customer-facing labels.
- Suppressed zero-value items so the block stays concise and relevant.
- Kept the copy customer-facing with no internal or experiment language.

## Example outcome
For the default scenario, the live calculator now surfaces:
- Affiliate fee: $22.50
- VAT collected: $15.00
- Product cost: $5.00

For a loss-making scenario, the live calculator now surfaces the dominant cost burden first, such as product cost before smaller fees.

## Verification
- Passed `node --test workspace/stripe-profit-calculator/tests/*.test.js` with 34/34 tests passing.
- Deployed production with `vercel deploy --prod --yes`.
- Reviewed the live page on both profitable and loss-making scenarios to confirm the copy reads customer-facing and the ranked deductions render correctly.

## Live URL
- https://profitafterfees.com/
