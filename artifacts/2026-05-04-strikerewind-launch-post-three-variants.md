# StrikeRewind launch post — three variants matched to the open LAUNCH POSTURE gate

**Date:** 2026-05-04
**For:** Travis
**Owner action:** when the `LAUNCH POSTURE: STRIKEREWIND PRE-LAUNCH DATA COPY` gate clears, paste the variant matching your reply (`HOLD FOR POLYGON` → A, `EARLY ACCESS` → B, `TIGHTEN COPY` → C). All three meet X's 280-char limit, founder voice from `@theshepherdstack`, URL on its own line.
**Why now:** the existing pre-baked launch post at `artifacts/2026-04-30-strikerewind-x-launch-post.md` claims `"Every night it scans the S&P 500"` and `"Top 5 setups daily"` — both false under the current fixture-only data state surfaced by the 2026-05-04 data-honesty packet. Posting it as-is the moment `TESTING COMPLETE` clears would re-create the same trust mismatch the homepage decision packet was raised to resolve. These three replacement variants close the gap so the launch post is honest and on-brand on day one regardless of which posture Travis picks.
**Routed through:** Luke (subagent), per `RULES.md` rule routing public-facing copy.

---

## Variant A — HOLD FOR POLYGON

**Diagnosis:** Post can finally make the original claim land, because under A the nightly full-index scan is actually running — so lead with the concrete behavior the reader doubts is possible, not the methodology.

**Final post copy:**

> I got tired of selling 30-delta on every ticker like it's gospel. So I built StrikeRewind. Every night it scans the S&P 500 and ranks every bull put and bear call by historical win rate at each delta and DTE. Free tier, no card.
>
> https://strikerewind.com

**Character count:** 274 / 280

**What changed and why:**
- Kept the original opener — the 30-delta line is the sharpest hook in the draft and survives the rewrite.
- Cut "Top 5 setups daily" — the ranked-by-win-rate claim already does that work, and "Top 5" reads like a marketing tic.
- Tightened "ranks each" to "ranks every" so the sentence reads cleanly aloud.
- Held "Free tier, no card" because that's the lowest-friction CTA for a skeptical scroller and it's true today.
- Left the URL on its own line per constraint.

**Claim needing evidence before publish:** Polygon Starter must be live and the nightly cron must have completed at least one successful full S&P 500 scan before this posts. Otherwise the first sentence under the hook is false.

---

## Variant B — EARLY ACCESS

**Diagnosis:** Honest pre-launch — the post should sell the methodology and the waitlist seat, not pretend the scan is running; the goal is an email, not a $9.99 charge.

**Final post copy:**

> I got tired of selling 30-delta like it's gospel. So I built StrikeRewind: a win-rate + EV engine that scores bull puts and bear calls across every delta and DTE. Early access on a 3-ticker preview. Full S&P 500 scan ships next. No card.
>
> https://strikerewind.com

**Character count:** 263 / 280

**What changed and why:**
- Dropped "on every ticker" from the opener to buy room — the line still reads.
- Replaced "scans the S&P 500" with what's actually live: the engine and the 3-ticker preview.
- Named the gap directly ("Full S&P 500 scan ships next") so a skeptical reader sees the missing piece called out before they find it.
- "No card" stays because that's the real free-tier promise and it lowers the bar to the waitlist.
- Cut "daily setups" language entirely — there is no daily digest under fixtures.

**Claim needing evidence before publish:** The free signup flow must capture email in a way that maps onto a paid-tier waitlist when Polygon is live, otherwise "early access" is a word with no follow-through.

---

## Variant C — TIGHTEN COPY

**Diagnosis:** Sell the engine, not the operation — describe the methodology that's true today and will still be true after Polygon ships, and let the reader find out what's scanned by signing up.

**Final post copy:**

> I got tired of selling 30-delta on every ticker like it's gospel. So I built StrikeRewind. It scores bull puts and bear calls by historical win rate and EV across every delta and DTE, so you stop guessing which strike on which name. Free tier, no card.
>
> https://strikerewind.com

**Character count:** 278 / 280

**What changed and why:**
- Removed "Every night it scans the S&P 500" — false today, would publicly burn the launch.
- Removed "Top 5 setups daily" — same reason; no daily digest exists yet.
- Replaced the operational claim with the methodology claim ("scores by historical win rate and EV across every delta and DTE") which is true on fixtures and on Polygon.
- Added the buyer's actual decision in plain language: "stop guessing which strike on which name." That's the pain a 30-delta-by-default seller feels.
- Kept the founder hook untouched and "Free tier, no card" as the CTA.

**Claim needing evidence before publish:** The Free tier must actually run a scoring pass against the 10-ticker subset on signup, or the post promises an engine that the new user doesn't see fire. Confirm the 1 scan/day path completes for a fresh free account before posting.

---

## Luke's recommendation

Variant C reads strongest as a launch post — the 30-delta hook lands, the methodology is sharp and falsifiable, and nothing in it goes stale or false the day Polygon ships. Variant A is a stronger post only if the nightly S&P 500 scan is genuinely running by post time; otherwise it's the current draft's same data-honesty problem with a new date on it.

---

## Pre-publish verification checklist (run in order, do not skip)

Carried over from `artifacts/2026-04-30-strikerewind-x-launch-post.md`, plus one new step (3) for the variants above:

1. `https://strikerewind.com` is live and serves the LandingPage hero correctly (StrikeRewind wordmark renders, OG card preview shows on `https://www.opengraph.xyz/url/strikerewind.com`).
2. `Start free` → `/dashboard` flow works end-to-end with no card prompt and the daily Hunt limit on FREE tier is `≥ 1`.
3. **Landing-page copy matches the chosen post variant.** Each posture has a corresponding 5-line landing-page edit set documented in `artifacts/2026-05-04-strikerewind-pre-launch-data-honesty-decision.md`. AutoBox lands those edits at the same time as the posture decision so the post and the page never disagree on launch day.
4. (Variant A only) Hunt table is populated with same-day results from the first nightly Polygon scan.
5. Travis confirms he is comfortable with `I built` framing under `@theshepherdstack` (founder voice). If not, swap `I built` → `We built` and `I got tired` → `We got tired`.

## Post sequencing on launch day

1. Smoke-test the live URL in incognito (signup, run hunt, see the engine fire).
2. Travis posts the chosen variant from `@theshepherdstack`.
3. AutoBox watches Discord for the post URL → captures URL, impressions/clicks/replies.
4. Reply to skeptical replies in-thread with one specific ticker example pulled from real scan output (pre-scripted replies forbidden — they need real numbers).
5. After 24 hrs, capture metrics; AutoBox runs anonymized scenarios from any submitted feedback.

## Forbidden language confirmed absent (all three variants)

- No `AI-powered`, `edge`, `guaranteed`, `proven`, `crushing it`.
- No realtime alert claims.
- No financial advice / no return promises.
- No `Show HN` / Reddit framing — these are X-shaped only.

## What this packet supersedes

- `artifacts/2026-04-30-strikerewind-x-launch-post.md` — the single-version pre-baked post is now superseded. Treat that file as historical reference only; do not paste from it.

## State after this run

- Cash balance unchanged: `$162.45`. No spend.
- No source-tree changes; artifact only.
- Both open gates carried forward unchanged: `TESTING COMPLETE: STRIKEREWIND`; `LAUNCH POSTURE: STRIKEREWIND PRE-LAUNCH DATA COPY`.
- No new gate raised this run — these variants are deliverables under the existing `LAUNCH POSTURE` gate.

## Suggested post copy

(Discord-side context-only sentence, NOT the public X post.)

> Updated launch-post packet up: three variants matched 1:1 to the LAUNCH POSTURE options (HOLD FOR POLYGON / EARLY ACCESS / TIGHTEN COPY) so paste-ready copy is waiting whichever you pick. Luke's pick is C; Variant A only if Polygon is actually running by post time. Packet: `artifacts/2026-05-04-strikerewind-launch-post-three-variants.md`. Supersedes `2026-04-30-strikerewind-x-launch-post.md`.
