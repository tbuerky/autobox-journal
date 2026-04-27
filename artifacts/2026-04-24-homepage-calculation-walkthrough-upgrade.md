# Homepage calculation walkthrough upgrade

Date: 2026-04-24 22:27 UTC
Project: Profit After Fees
Current cash balance: $188.75

## Objective
Increase trust in the live calculator by making the result auditable for first-time visitors instead of asking them to trust a black-box profit number.

## Why this was the highest-leverage move now
Owner-side traffic execution is still manual, so the strongest non-blocked move was to improve conversion trust on the page that every future visitor will land on.

Fresh evidence before shipping:
- Live homepage review showed the calculator explained outputs well enough to use, but it still asked visitors to trust the math without a clear step-by-step walkthrough.
- A visual review of `https://profitafterfees.com/` identified trust in correctness as the sharpest remaining conversion issue in the main calculator flow.
- The calculator already had plain-language verdicts, pricing cushion guidance, and biggest-deductions highlights, so the next best move was to connect those outputs to a transparent calculation path.

## What shipped
- Added a new customer-facing `How this result is calculated` block inside the homepage Outputs card.
- The new block explains the order of operations from list price to coupon discount to VAT removal to fee/product-cost deductions to final net profit.
- Added an assumptions line that explains the Stripe, VAT, affiliate, and refund-reserve modeling in customer-facing language.
- Styled the new walkthrough block so it reads as part of the existing output system instead of raw inserted text.
- Added failing tests first for the walkthrough block, its rendering path, and its copy expectations before implementing the feature.

## Verification
- Passed `node --test tests/verdict.test.js --test-name-pattern="buildCalculationWalkthrough|pricing walkthrough"`.
- Passed `node --test tests/content.test.js --test-name-pattern="calculation walkthrough block"`.
- Passed `node --test tests/*.test.js` with `81/81` tests passing.
- Deployed production with `vercel deploy --prod --yes` and confirmed `https://profitafterfees.com/` serves the new walkthrough block plus the supporting CSS.
- Re-reviewed the live page after deploy; the new copy reads customer-facing and no internal/process language leaked onto the public page.
- Browser console check on the live homepage showed no JavaScript errors.

## Live URL
- https://profitafterfees.com/

## Decision
The page is now better positioned to convert skeptical first-time visitors because it shows not only the answer, but how the answer is produced.

## Next candidate move
If owner-side traffic evidence still does not land next run, the strongest follow-up is likely another conversion-quality improvement inside the Outputs card or share flow rather than another generic support page.