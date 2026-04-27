# 2026-04-21 search/indexing and first-signal baseline

Date: 2026-04-21 22:17 UTC
Project: Profit After Fees
Live site: https://profitafterfees.com/

## Task executed
Check whether the live site already shows any measurable indexing pickup or first user signals before creating more pages.

## Evidence gathered
1. Live production status is healthy.
   - `https://profitafterfees.com/` returned HTTP 200.
   - `https://profitafterfees.com/robots.txt` returned HTTP 200.
   - `https://profitafterfees.com/sitemap.xml` returned HTTP 200.
   - `vercel inspect profitafterfees.com` showed the current production deployment is ready with aliases on `profitafterfees.com` and `www.profitafterfees.com`.

2. Search-engine visibility is still effectively zero from the checks available in this sandbox.
   - Yahoo Search for `site:profitafterfees.com` returned "We did not find results for: site:profitafterfees.com".
   - Google search was blocked by an anti-bot interstitial instead of returning usable result data.
   - Bing search presented a challenge page instead of usable results.
   - DuckDuckGo and Brave also challenged the browser session, so they did not produce trustworthy index counts.

3. First traffic/user-signal observability is not available from the current Vercel plan/tooling in this environment.
   - `vercel logs --environment production --source static --limit 20 --no-follow` returned `No logs found`.
   - `vercel metrics vercel.request.count --since 24h --group-by request_path --format json` failed with `payment_required` and the message `A subscription to Observability Plus is required`.

## Decision
Do not create more pages based on guesswork.

Current evidence says:
- the site is live and crawlable
- there is no visible proof of indexing yet from accessible public checks
- there is no measurable first-user traffic signal available in the current sandbox without either a real distribution event or additional approved analytics access

That means the business still does not need another internal content sprint. The highest-leverage next move remains the already-prepared founder-style X launch post, because it can generate the first real click and reaction signal at $0.00 cash cost.

## Approval-gated note
A secondary measurement bottleneck is now visible:
- Vercel request metrics are behind Observability Plus in this environment
- enabling a better analytics path would require either spend, a new third-party analytics account, or new private credentials

Do not request that approval first. It is lower leverage than simply getting the first real launch post out.

## Recommended immediate next step
1. Get approval to publish the prepared X launch post from `artifacts/2026-04-21-launch-distribution-approval-packet.md`.
2. After the post is live, rerun monitoring with:
   - the public post URL
   - any reply/repost activity
   - any available click or visit data
3. Only if traffic actually begins and measurement is still blind should the next approval packet be for analytics/observability setup.

## Budget
- Current experiment cash balance: $188.75
- Cash spent this run: $0.00
