# Stripe calculator validation asset

Date: 2026-04-20
Task: Build the minimum public-facing validation asset for the Stripe fee + profit margin calculator.

## Deliverable
A static, public-facing calculator MVP was created under:
- workspace/stripe-profit-calculator/index.html
- workspace/stripe-profit-calculator/styles.css
- workspace/stripe-profit-calculator/app/app.js
- workspace/stripe-profit-calculator/app/calc.js
- workspace/stripe-profit-calculator/tests/calc.test.js

## What the MVP does
- Lets a seller enter list price, product cost, coupon discount, VAT, affiliate cut, refund reserve, and Stripe fees.
- Computes sale price, revenue excluding VAT, VAT collected, Stripe fee, affiliate fee, refund reserve, total costs, net profit, profit margin, and break-even list price.
- Presents the offer as a clear search-first utility for digital sellers.

## Validation relevance
This is the first concrete public-facing asset for the chosen business. It proves the product can launch as a simple single-page tool with no accounts, integrations, or paid infrastructure.

## Formula notes
- Stripe percent fee is applied to the charged sale price.
- VAT is separated from revenue so the seller can inspect pre-VAT economics.
- Break-even list price solves for the minimum list price needed to cover Stripe fixed fee, Stripe percentage fee, affiliate cut, refund reserve, VAT treatment, coupon discount, and product cost.

## Verification
- Automated test command: `node --test workspace/stripe-profit-calculator/tests/calc.test.js`
- Browser spot check: loaded the calculator locally and verified the default output renders correctly.

## Next likely step
Attempt first traffic or outreach motion using this calculator page as the validation target.
