# Parallel business candidate packet — 2026-04-25

## Operator decision

Profit After Fees should stay live, but it should not absorb every run while its highest-leverage acquisition lane is owner-side.

Current classification: **blocked-but-live**.

Why:
- The site is live at https://profitafterfees.com/ with a polished calculator-first homepage, strong standalone calculator pages, comparison pages, and paid-search-ready disclosure.
- The approved Google Ads test now has campaign/ad group/keyword/negative/ad CSVs at `artifacts/paid-search-launch-assets/` plus a manual build packet at `artifacts/2026-04-25-google-ads-launch-assets.md`.
- No fresh owner-side campaign launch, spend, click, search-term, disapproval, or Indie Hackers evidence was visible in the Discord control thread at the start of this run.
- Continuing to add generic pages would be lower leverage than opening one additional shot on goal.

Recommended next track: **start one parallel utility experiment while preserving Profit After Fees as the live asset.**

## What would change priority back to Profit After Fees

Return to Profit After Fees immediately if any of this arrives:
- Google Ads customer ID, campaign name, first clicks, CPC, CTR, spend, search terms, or disapproval messages.
- A live Indie Hackers post URL and early reactions.
- Any real user feedback, bug report, or conversion signal from the live site.
- Owner approval for a specific monetization step such as payment setup, analytics spend, or a paid distribution test beyond the existing Google Ads approval.

## Candidate scoring

Scoring: 1 = weak, 3 = workable, 5 = strong.

| Candidate | Pain / user | 50 likely users identifiable without paid ads | Reach without new account gates | MVP in 1-3 days | Repeated specific pain | Demand test before build | Avoids current PAF blockers | Revenue path | Total |
|---|---|---:|---:|---:|---:|---:|---:|---:|---:|
| AI API cost calculator for small SaaS apps | Indie hackers shipping AI features need to estimate OpenAI/Anthropic token cost, gross margin, and plan pricing before launch. | 5 | 3 | 5 | 5 | 4 | 4 | 4 | 30 |
| DMARC/SPF record checker for solo founders | Domain owners need email deliverability records checked before sending product emails. | 4 | 3 | 3 | 5 | 4 | 5 | 3 | 27 |
| Refund reserve calculator for digital-product sellers | Creators need to decide how much sale cash to reserve for refunds, disputes, and taxes. | 4 | 3 | 5 | 4 | 3 | 3 | 3 | 25 |
| Micro-SaaS runway calculator | Bootstrappers need to know how many months they can fund hosting, APIs, and contractors. | 4 | 3 | 5 | 4 | 3 | 3 | 4 | 26 |
| Google Ads break-even CPC calculator | Small advertisers need to know max CPC before launching a campaign. | 3 | 3 | 5 | 5 | 3 | 3 | 2 | 24 |

## Chosen candidate

### AI API cost calculator for small SaaS apps

Working product name: **AI Feature Cost Calculator**

Core promise:
> Estimate token cost, gross margin, and plan pricing before you ship an AI feature.

Why this is the best parallel bet now:
- It is a calculator utility, so it fits the same build muscle as Profit After Fees without being just another PAF page.
- The pain is current and specific: builders using AI APIs can underprice plans quickly because token cost varies by model, prompt length, output length, and usage volume.
- It has a clear MVP: inputs for model, calls per user, prompt tokens, output tokens, monthly users, subscription price, and fixed costs; outputs for monthly API cost, cost per user, gross margin, break-even price, and safe price at target margin.
- It can be built in 1-3 days as a single-page utility.
- It has more direct monetization paths than a generic content site: paid templates, a saved scenario pack, affiliate/referral routes for model gateway tools if later approved, or a small paid API-cost audit product if evidence supports it.
- It avoids the current PAF bottleneck because it does not depend on the existing Google Ads account launch or Indie Hackers follow-through to begin validation/build work.

## Domain / naming options

Do **not** buy a domain yet. If Travis wants this as a separate asset, the recommended approval-gated domain check/purchase packet is:

1. `aifeaturecost.com`
   - Clear, short, tied to the exact problem.
   - Best if available under roughly $15/year.
2. `tokenmargin.com`
   - Stronger brand, points at the margin problem.
   - Slightly less obvious for search intent.
3. `aicostcalculator.com`
   - Best exact-match name if available, but likely expensive or taken.
   - Only buy if normal registration price; do not chase premium pricing.

Specific approval needed if this becomes the bottleneck:
> APPROVED: CHECK AND BUY ONE AI COST CALCULATOR DOMAIN, MAX $15

Immediate action after approval:
- Check the three domains in order.
- Buy the first non-premium option at or below $15/year.
- Record the expense in `config/BUDGET.md`.
- Launch the MVP on that domain or use a temporary subdomain if domain setup lags.

## First validation/build action

Next run, if no Profit After Fees traffic evidence arrives first, build a one-page MVP spec and validation page for **AI Feature Cost Calculator**.

Minimum MVP scope:
- Model selector with editable token prices for a few common model tiers.
- Inputs: prompt tokens, output tokens, calls per user per month, monthly active users, subscription price, fixed monthly cost, target margin.
- Outputs: API cost per call, cost per user, total monthly API cost, gross margin, break-even monthly price, suggested price for target margin.
- Shareable scenario URL.
- Customer-facing copy only; no internal experiment labels.

Validation goal:
- Get to a public URL or public-ready preview quickly enough that the next distribution packet can ask AI builders for reactions to a concrete calculator, not an idea.

## Owner gates

No money spent and no permission gate crossed in this run.

Potential future gates:
- Domain purchase: max $15/year approval required.
- Paid traffic: separate approval required.
- Payments: separate approval required.
- Manual outreach at scale: separate approval required.

## Budget

Current cash balance remains **$188.75**.
