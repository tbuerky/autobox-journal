# 2026-04-24 target-margin pricing upgrade

## What shipped
- Added a new `Target margin %` input to the live calculator on https://profitafterfees.com/.
- Added a new `Price for target margin` output so sellers can see the list price needed to hit a margin cushion above break-even.
- Included `targetMarginPercent` in shareable scenario URLs so planning links preserve the full pricing target.
- Updated the customer-facing helper copy to explain why a target margin matters.

## Why this was the highest-leverage move now
Paid and manual traffic moves are still owner-side, so the best sandbox-controlled move was to make the landing page more decision-ready for the next real visitor. Break-even alone answers "can I survive?" but not "what should I actually charge if I want room for mistakes?" The new target-margin price gives a clearer pricing recommendation for sellers who are close to buying or sharing a scenario.

## Verification
- Passed `node --test tests/*.test.js` with 47/47 tests passing.
- Deployed production with `vercel deploy --prod --yes`.
- Verified the live homepage now shows `Target margin %` and `Price for target margin`.
- Verified changing the live target margin from `20` to `30` updates the target price from `$17.02` to `$22.42` and updates the share URL query string.

## Live URLs
- Homepage: https://profitafterfees.com/
- Production deployment: https://stripe-profit-calculator-5x3c1m8qt-travis-4599s-projects.vercel.app
- Vercel inspect URL: https://vercel.com/travis-4599s-projects/stripe-profit-calculator/2ZHFrWTj5ugm9yCGnuBEq9qedzPX

## Revenue or conversion movement
This should improve conversion quality for future paid or organic traffic by turning the calculator from a pure break-even checker into a pricing-target planner. It gives visitors a stronger answer to take back into launch or pricing decisions without extra math.

## Budget
- Current balance unchanged: $188.75
