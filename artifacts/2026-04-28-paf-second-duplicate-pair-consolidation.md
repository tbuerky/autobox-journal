# PAF second duplicate calculator-pair consolidation

## What shipped
Two more pairs of duplicate calculator pages on `profitafterfees.com` were consolidated via permanent redirects to canonicals. The prior consolidation pass (2026-04-28 18:35) addressed three pairs but missed these two, both of which were exact-template SEO variants of canonical calculators.

| Loser (deleted, now 308) | Canonical (kept, 200) |
|---|---|
| `/stripe-processing-fee-calculator/` | `/transaction-fee-calculator/` |
| `/llm-cost-calculator/` | `/ai-feature-cost-calculator/` |

The first pair is the exact same per-transaction fee calculator with Stripe-specific keyword framing on the loser. The second pair is the exact same per-user AI cost calculator; the AI utility brand, social preview cards, AI model pricing index, distribution post, and standalone-domain packet all already point at `/ai-feature-cost-calculator/`, so `/llm-cost-calculator/` was a duplicate SEO stub competing with its own canonical.

The homepage related-grid still had a stale "Per-user LLM cost" link to the loser page — replaced with a customer-facing card for the AI feature cost calculator.

## Why now
The prior consolidation pass declared three pairs as the full set, but a sitewide audit found two more identical-template duplicates the prior pass missed. Each duplicate URL splits Google's relevance signal across two pages competing for the same intent and adds an AdSense thin-content risk on the loser. While Travis is currently spending paid Google Ads dollars on the canonical calculator and waiting on AdSense approval, every duplicate adjacent to that path is leaving signal on the table.

This is the same pruning theme as the prior pass (and the launch/home prune before it): one less internal-duplication pattern, no new public surface area, no new copy to maintain.

## Changes
- `vercel.json` — added 4 new permanent (308/301) redirects: `/stripe-processing-fee-calculator(/)` → `/transaction-fee-calculator/`, `/llm-cost-calculator(/)` → `/ai-feature-cost-calculator/`.
- Deleted `stripe-processing-fee-calculator/` and `llm-cost-calculator/` directories from the deployed tree.
- `sitemap.xml` — removed both loser entries.
- `index.html` — replaced the related-grid card pointing at `/llm-cost-calculator/` with a card pointing at `/ai-feature-cost-calculator/` (label "AI feature cost & margin", sub "Token cost per active user, gross margin, and break-even price").
- `transaction-fee-calculator/index.html` — removed the internal link to the loser slug.
- `tests/content.test.js` — updated the consolidated-redirects test to assert the two new losers are gone and the two new redirect destinations exist in `vercel.json`; updated the surfaced/demoted homepage link arrays; removed loser-specific tests; removed deleted path constants and metadata-list entries.

## Verification
- `node --test tests/*.test.js` → `106/106` passing.
- `vercel deploy --prod --yes` → `dpl_9TBqzT2t1x1nknMcyyGQ7ZCRmvwW`; aliased to `profitafterfees.com` and `www.profitafterfees.com` under team `travis-4599s-projects`.
- Live HTTP checks:
  - `/stripe-processing-fee-calculator/` → `308` `Location: /transaction-fee-calculator/`
  - `/llm-cost-calculator/` → `308` `Location: /ai-feature-cost-calculator/`
  - `/`, `/transaction-fee-calculator/`, `/ai-feature-cost-calculator/`, `/privacy/`, `/ads.txt`, `/sitemap.xml` → all `200`
- Live homepage HTML contains `href="./ai-feature-cost-calculator/"` with the new card label and no remaining `llm-cost-calculator` reference.
- IndexNow POST for the three canonicals returned `HTTP 200`.

## Out of scope
- AdSense approval / Auto Ads / impressions / eCPM (Travis-side evidence).
- StrikeSight `ROTATED:` confirmation, options-data subscription approval, `getstrikesight.com` purchase approval (all Travis-side).
- AI Feature Margin Check post URL and submitted scenarios (Travis-side).
- `break-even-price-calculator.bak/` (root-owned in sandbox; already 404 on production).

## Approval
None required. No spend.

## Cash balance
$188.75
