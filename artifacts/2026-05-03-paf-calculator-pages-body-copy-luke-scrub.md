# PAF calculator pages — body-copy AI-smell scrub (Luke route)

**Date**: 2026-05-03 (run 9)
**Why now**: Only one open gate remains (`TESTING COMPLETE: STRIKEREWIND`, owner-side). PAF Search ads were extended through 2026-05-18 in the prior interactive session, so the 5 calculator pages are receiving paid Google Search Ads traffic right now. Body copy was last touched 2026-04-25 (8 days ago) and had drifted into AI-flat phrasing in several spots. Wakeup prompt explicitly endorses "stronger product copy" over more audits when the gates stall on owner side.
**Routing**: Luke per `RULES.md` — public-facing copy on pages real buyers see.

## What shipped

10 surgical find-and-replace edits across 4 calculator pages. No rewrites, no new sections, no tone shifts. The voice was already good (concrete, no signup, your-numbers-stay-yours); only the AI-smell pockets were touched. Break-even-price-calculator was clean — no edits.

| File | Old | New |
|------|-----|-----|
| transaction-fee-calculator | "Keep pressure-testing the payout before you publish the price" | "See the full payout before you set the price" |
| transaction-fee-calculator | "Compare the transaction fee to the rest of your margin leaks." | "Compare the transaction fee to every other deduction on the same sale." |
| transaction-fee-calculator | "The transaction fee is rarely the whole story." | "The transaction fee is one line in the stack." |
| selling-price-calculator | "Stripe fees, done right" (H3) | "Stripe fee on what the customer pays" |
| selling-price-calculator | "Keep checking the price before you publish it" (H2) | "Run the numbers before you publish the price" |
| profit-margin-calculator | "See your real margin after the checkout stack takes its cut" (H1) | "See your real margin after fees, VAT, affiliates, and refunds" |
| profit-margin-calculator | "Margin gets distorted fast when" | "Margin shrinks fast when" |
| profit-margin-calculator | "leaves behind" | "actually keep" |
| profit-margin-calculator | "fragile offer" | "price that barely covers cost" |
| digital-product-pricing-calculator | "all take their turn" | "each come out" |

## What I cut and why

- AI personification (stack "takes its cut", deductions "take their turn", fees "rarely the whole story") → concrete language about specific deductions
- AI-pride clichés ("done right") → specific descriptors ("on what the customer pays")
- AI-vague nouns ("margin leaks", "fragile offer") → concrete ones ("every other deduction", "barely covers cost")
- AI-fancy verbs ("distorted") → plain ones ("shrinks")
- Repeated metaphor on transaction-fee-calculator ("pressure-test the payout" appearing twice) → kept once in hero, cut from H2
- Inconsistent "More tools" H2 pattern across pages → unified to "before-you-publish-the-price" frame

## Deploy + verification

- Vercel project `stripe-profit-calculator` (PAF), org `team_EGsm5UDqHv7Y9FKIhCOaILSK`. Auth via `VERCEL_TOKEN_TSS`.
- Deploy: `vercel deploy --prod --yes` from `workspace/stripe-profit-calculator/`.
- Deployment `dpl_Bon4ErAfe9eNf55zULXYeNvfx9WP`, status `READY`, target `production`, ready immediately.
- Verified all 10 edits live on `profitafterfees.com` via curl + grep.

## Deliberately did NOT

- Touch the homepage `/` — already reviewed, voice is clean
- Touch break-even-price-calculator — Luke confirmed clean, no edits needed
- Add sections, links, or trust signals — out of scope for an AI-smell scrub
- Re-run a Cove pass — design unchanged, only inline copy nudged
- Raise a new gate — no owner action required

## Cash balance

Unchanged. $162.45. No spend this run. (Render starter still accruing ≈$0.23/day toward end-of-cycle invoice, unchanged from prior runs.)
