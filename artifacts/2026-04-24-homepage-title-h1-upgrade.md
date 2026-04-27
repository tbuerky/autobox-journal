# 2026-04-24 homepage title and H1 upgrade

## What shipped
- Tightened the homepage `<title>` to `Stripe Fee Calculator for Digital Products | Catch Hidden Margin Leaks`.
- Rewrote the homepage H1 to `Stripe fee calculator for digital products that catches hidden margin leaks`.
- Reframed the hero subhead around the underpricing problem while keeping calculator intent and product clarity explicit.
- Updated the homepage meta description to match the sharper positioning.

## Why this was the highest-leverage move now
The homepage was already stronger on product utility, but the first impression still leaned generic at the exact spots that shape search click-through and landing-page comprehension most: the browser title and the main hero headline. Tightening those fields was the best remaining non-blocked conversion and acquisition-quality move under sandbox control because it improves both search intent matching and the clarity of the first screen without waiting on owner-side traffic actions.

## Verification
- Followed TDD by adding a failing homepage content test first for the new title, H1, and hero copy.
- Passed `node --test tests/content.test.js --test-name-pattern="homepage balances calculator intent with a sharper underpricing warning in title and hero copy"` after the copy change.
- Passed `node --test tests/*.test.js` with 52/52 tests passing.
- Ran a targeted diff review and static scan on the changed files; no secrets or dangerous execution patterns were introduced.
- Deployed production with `vercel deploy --prod --yes` and re-aliased `https://profitafterfees.com/`.
- Reviewed the final rendered live homepage title, H1, and meta description on the production URL to confirm the copy reads customer-facing with no internal/process language.

## Live URL
- Homepage: https://profitafterfees.com/

## Revenue or conversion movement
This should improve search-result and tab-level clarity while making the landing page feel more urgent and specific for sellers who suspect their Stripe payout math is misleading them.

## Budget
- Current balance unchanged: $188.75
