# 2026-04-21 domain recommendation packet

Task: identify the next approval-gated move most likely to improve trust and conversion before broader manual distribution.

## Decision
Recommendation: approve the purchase of one neutral .com domain before any serious human-led launch posting.

Primary recommendation:
1. profitafterfees.com

Backup options:
2. digitalproductmargin.com
3. feeprofitcalculator.com

## Why this matters now
The product is already live at `https://stripe-profit-calculator.vercel.app`, has three search-entry pages, and has completed one external indexing motion via IndexNow. The next sharp move is broader distribution, but the current `vercel.app` hostname creates a trust and memorability drag exactly when the site needs first clicks from strangers.

A custom domain matters now because it:
- looks less temporary in launch posts and forum replies
- is easier to remember and paste into replies
- reduces dependence on a third-party subdomain for credibility
- gives room to move away from a trademark-heavy product name before bigger promotion

## Important naming constraint
Avoid buying a domain that contains `stripe`.

Reason: the current site title uses Stripe descriptively, but paying for a trademark-heavy domain would increase brand and platform risk when a neutral domain can still rank for the same intent through on-page copy. A neutral domain is the safer operator move.

## Evidence gathered
- Current production URL in the launch packet: `https://stripe-profit-calculator.vercel.app`
- Current live pages ready for promotion:
  - homepage
  - `/stripe-fees-for-notion-templates/`
  - `/stripe-fees-for-online-courses/`
  - `/stripe-fees-for-micro-saas/`
- External discovery motion already completed: crawler files plus IndexNow submission artifact at `artifacts/2026-04-21-indexnow-distribution.md`
- `.com` availability check via Verisign RDAP returned 404 (unregistered) for:
  - `profitafterfees.com`
  - `digitalproductmargin.com`
  - `feeprofitcalculator.com`
- Current published `.com` price evidence from Porkbun pricing page: `.COM from $11.08`

## Options considered
### Option A — profitafterfees.com
Why it won:
- shortest of the safe options
- communicates the actual outcome users want
- works even if the tool later expands beyond one payment processor

Tradeoff:
- slightly less explicit for search than a longer calculator-style domain

### Option B — digitalproductmargin.com
Why it is strong:
- tightly aligned with the current audience and promise
- descriptive without trademark risk

Tradeoff:
- longer and less conversational

### Option C — feeprofitcalculator.com
Why it is viable:
- closest to the current utility framing
- still neutral and descriptive

Tradeoff:
- slightly clunky wording

### Rejected direction — any domain containing `stripe`
Why rejected:
- higher trademark dependence
- unnecessary when search intent can be captured in page copy, titles, and URLs instead of the domain itself

## Exact estimated cost
Using Porkbun's published current `.COM from $11.08` pricing:
- buy 1 domain: $11.08
- buy 2 domains: $22.16
- buy all 3 domains: $33.24

Recommended spend:
- approve 1 primary domain only: $11.08

Current experiment cash balance before approval: $200.00
Cash balance after one approved domain purchase: $188.92

## Specific approval needed
Approve one of the following:
- `profitafterfees.com` for up to $11.08
- `digitalproductmargin.com` for up to $11.08
- `feeprofitcalculator.com` for up to $11.08

Best operator choice if approving now:
- approve `profitafterfees.com` up to $11.08

## What happens immediately after approval
1. Buy the approved domain.
2. Point it to the existing Vercel project.
3. Update canonical URLs, sitemap, robots.txt, and on-page links.
4. Re-deploy and verify the custom domain is live.
5. Refresh the launch packet so every future distribution post uses the custom domain.
6. Then do the next human-led distribution motion with a cleaner, more credible URL.

## Why this beats another internal-only content task right now
Another support page would add inventory, but the site already has enough surface area for first real outreach. The bottleneck is now trust and launch-readiness, not one more page.
