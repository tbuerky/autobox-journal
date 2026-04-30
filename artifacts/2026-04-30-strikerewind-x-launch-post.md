# StrikeRewind — X launch post, ready to paste on deploy day

**Status:** Pre-deploy. Travis must publish from `@theshepherdstack` the moment `https://strikerewind.com` is live and the signup flow has been smoke-tested end-to-end.

**Routed through:** Luke (subagent), per `RULES.md` rule routing public-facing copy.

**Why pre-write:** The deploy gate `APPROVED: DEPLOY ON VERCEL+RENDER STARTER, $7/MO` is open. The minute it lands and AutoBox ships the deploy, the highest-leverage next move is distribution — and per `PROJECT.md` the documented default lane is a founder-style X post. Having Luke-polished post copy ready collapses one hour of friction off the launch and removes the temptation to ship a hasty post when Travis is mid-deploy.

## Diagnosis (Luke)
The post has to earn the click in the first line by naming the specific mechanic so the skeptic stops scrolling before the URL.

## Why this hits
- Opens with the trader's own frustration in first person (`I got tired of...`) — the skeptic recognizes himself before he recognizes a pitch.
- Names the actual mechanic (rank by historical win rate at every delta × DTE across the S&P 500) instead of generic "we scan options" language — that's the one sentence that separates this from a wrapper.
- Closes on friction removal (free, no card, top 5 daily) so the click feels cheap; URL on its own line for tap-target clarity.

## Pre-publish verification checklist (run in order, do not skip)
1. `https://strikerewind.com` is live and serves the LandingPage hero correctly (Logo wordmark renders as StrikeRewind, OG card preview shows on `https://www.opengraph.xyz/url/strikerewind.com`).
2. `Start free` → `/dashboard` flow works end-to-end with no card prompt and the daily Hunt limit on FREE tier is `>= 1` (the tier-copy + limits gate `APPROVED: STRIKEREWIND TIER COPY + LIMITS PRE-DEPLOY` covers this — do not publish before that lands).
3. Hunt table is populated with same-day results (nightly scan ran successfully the morning of publish — check Supabase `cache_hunt_scans` or whatever table the warehouse migration ends on).
4. Landing page free-tier copy still reads "Top 5 Hunt results per day" verbatim (post and page must not contradict).
5. Travis confirms he is comfortable with `I built` framing under `@theshepherdstack` (founder voice) vs company voice. If founder voice is wrong, swap `I built` → `We built` and `I got tired` → `We got tired` — same mechanic, slightly less personal.

## Post sequencing on launch day
1. Smoke-test the live URL in incognito (signup, run hunt, see top 5).
2. Travis posts the X copy below from `@theshepherdstack`.
3. AutoBox watches Discord for the post URL → captures URL, impressions/clicks/replies (per `TODO.md` `If Travis posts on X, capture URL...`).
4. Reply to skeptical replies in-thread with one specific ticker example pulled from that day's actual scan output (do not pre-script those replies — they need real numbers from the live data).
5. After 24 hrs, capture metrics, AutoBox runs anonymized scenarios from any submitted feedback.

## Suggested post copy:
I got tired of selling 30-delta on every ticker like it's gospel. So I built StrikeRewind. Every night it scans the S&P 500 and ranks each bull put and bear call by historical win rate at every delta and DTE. Free tier, no card. Top 5 setups daily.

https://strikerewind.com

## Character count
276 characters incl. URL (under X's 280 limit). Tested visually — line break between body and URL renders cleanly on web and mobile.

## Forbidden language confirmed absent
- No `AI-powered`, `edge`, `guaranteed`, `proven`, `crushing it` — confirmed.
- No realtime alert claims — confirmed (no claim of alerts at all in this post; daily-digest framing is reserved for the landing page).
- No financial advice / no return promises — confirmed.
- No `Show HN` / Reddit framing — this is X-shaped only.

## What is NOT in this packet
- HN `Show HN` post — deferred. HN audience is dev/builder-shaped; the next packet should target traders, not builders, until Travis is ready to position StrikeRewind as a builder-credibility play.
- r/options post — deferred. r/options moderates self-promotion aggressively; better as a thoughtful "I built this and want feedback on the methodology" post a week after launch once there is real usage data to point at, not a launch-day post.
- Reply scripts — deferred. Replies need real ticker data from the day's scan; pre-writing them would invent specifics that may not exist on launch day.

## State after this run
- Cash balance unchanged: `$162.45`.
- No commit (artifact only; no source-tree changes).
- Both open gates carried forward unchanged: `APPROVED: DEPLOY ON VERCEL+RENDER STARTER, $7/MO`; `APPROVED: STRIKEREWIND TIER COPY + LIMITS PRE-DEPLOY`.
