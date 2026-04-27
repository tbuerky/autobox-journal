# Launch distribution approval packet

Date: 2026-04-21 18:18 UTC
Project: Profit After Fees
Live site: https://profitafterfees.com/

## What should be done
Approve one real human-led founder-style X launch post from an account the owner is willing to use publicly, then publish the prepared launch copy that points to https://profitafterfees.com/.

Recommended first move:
- publish one founder-style launch post on X using the custom domain
- use the short practical copy below
- after posting, save the public post URL and monitor click/user signals before making more pages

Suggested post copy:

If you price digital products with Stripe, the processing fee is only part of the problem.

Coupons, VAT, affiliates, refunds, and fulfillment costs can make a product look profitable when it is not.

I built a free calculator that shows your Stripe fee, total costs, net profit, margin, and break-even price in one pass.

Useful for templates, courses, and micro-SaaS pricing.
https://profitafterfees.com/

## Why it matters now
The site is already live on the approved neutral domain. Search/discovery files are in place. The current bottleneck is not product readiness or domain setup anymore; it is the lack of any real human-led distribution event that can generate first users, first click data, and first qualitative reactions.

Without one real post, the project risks drifting back into internal work without learning whether strangers will click, understand the promise, and use the calculator.

## Evidence gathered this run
- X API posting path is not currently usable in the sandbox:
  - `xurl` was not installed at start
  - after installation, `xurl auth status` returned `No apps registered`
  - `xurl whoami` returned `401 Unauthorized`
- Browser access showed no logged-in session available for common launch venues:
  - `https://x.com/compose/post` redirected to login
  - `https://www.reddit.com/submit` required login and showed a network-security block message
  - `https://news.ycombinator.com/submit` returned `Sorry.`
- A writable authenticated identity is available on GitHub (`gh auth status` showed account `the-shepherd-stack`), but publishing under the owner's real identity is explicitly approval-gated by `config/PROJECT.md`.

## Options considered
1. X launch post from an approved existing account
- Speed: highest
- Direct cash cost now: $0 if posted via browser by the owner or with an already-approved authenticated session
- Upside: fastest path to first clicks and reactions
- Risk: uses a public identity, so approval is required

2. Indie Hackers launch post from an approved existing account
- Speed: high if account access already exists
- Direct cash cost now: $0
- Upside: more relevant founder audience for this tool
- Risk: still identity-linked and may need login access not currently available in the sandbox

3. Show HN / Hacker News post
- Speed: medium
- Direct cash cost now: $0
- Upside: strong upside if it lands
- Risk: requires a logged-in account and usually a stronger novelty bar; current browser session is not authenticated

4. Keep waiting for passive search pickup
- Speed: low
- Direct cash cost now: $0
- Upside: no identity decision needed
- Risk: lowest learning rate; delays first user evidence unnecessarily

## Recommendation
Approve option 1: one founder-style launch post from an account the owner is comfortable using publicly.

Why this option wins now:
- zero direct spend
- fastest path to first strangers visiting the site
- easiest way to validate whether the homepage promise is compelling
- gives immediate signal before more SEO/content expansion

## Exact estimated cost
- Cash required now: $0.00
- Budget impact if approved: none
- Current experiment cash balance: $188.75

## Specific approval needed
Please approve one of these:
- Approval to publish one launch/distribution post under the owner's chosen public account, or
- Approval to provide/log in to one non-real-name brand account inside the environment for the same purpose

If the owner wants agent execution instead of manual posting, the additional approval needed is:
- permission to use that account's authenticated session or credentials in this sandbox

## What happens immediately after approval
1. Publish the approved launch post using the prepared copy and https://profitafterfees.com/.
2. Save the post URL in an artifact.
3. Check for first user signals:
   - clicks/visits
   - any replies or questions
   - which preset/scenario gets referenced
4. Use those signals to decide the next highest-leverage move:
   - one follow-up reply in the same thread
   - one niche forum answer using a preset URL
   - or homepage/conversion copy adjustment based on real feedback

## Blocker status
This run is blocked on an approval gate, not on implementation. The highest-leverage next move is ready, but publishing it would cross the project's explicit rule against posting under the owner's real identity without approval.