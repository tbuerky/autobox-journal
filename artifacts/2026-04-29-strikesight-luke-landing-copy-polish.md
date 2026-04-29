# StrikeSight Luke landing-copy polish (step #5 of locked HANDOFF build queue)

## Summary
Routed the new public LandingPage (`frontend/src/pages/LandingPage.tsx`, shipped last run as commit `abf66d9`) through Luke for the customer-facing copy pass on the credit-spread-optimization story Travis named in the priority-shift session as the conversion lever ("scans the whole S&P, returns exact strikes and expirations that have been consistently profitable over time"). Luke owned the rewrite; AutoBox-Hermes owned the integration: ran factual checks against the backend code, corrected two claims that didn't match the implementation, applied the polished copy, verified builds + tests, committed, pushed.

This is step #5 of the build queue locked into HANDOFF on 2026-04-28. Steps #2 (Cove tokens, `e8b805d`), #3 (Hunt as data table, `e8a3572`), and #4 (routing restructure + LandingPage shell, `abf66d9`) shipped earlier. Step #1 (Supabase `spread_results` warehouse SQL) is gated on Travis applying SQL via the dashboard.

## Why this was the right autonomous move
- The locked HANDOFF queue says step #5 next.
- LandingPage shell exists (step #4 shipped) — there was a real surface for Luke to polish.
- Travis priority-shift quote explicitly ties revenue to "telling the story": "If you can correctly tell the story (scans whole S&P, returns tickers and exact strikes and exps that have been consistently profitable over time) that is something people would pay a subscription for."
- Public-facing copy on a paid SaaS landing page is exactly Luke's lane per RULES.md.
- Step #1 (warehouse SQL) and the Polygon subscribe gate are both owner-action gates — autonomous run cannot unblock them.

## Luke's diagnosis
> The hero subhead promises "consistently profitable" spreads, which a skeptical trader reads as a guarantee — and the rest of the page never names what the scanner is measuring against, so the claim floats. The fix is to ground the promise in the actual mechanic (historical win rate and EV per ticker, beaten against the 30-delta/45-DTE baseline) and let the reader judge it.

## What changed (final shipped copy)

### Hero
- **H1**: `Credit spreads, optimized per ticker.` → `Stop selling 30-delta on every ticker.`
  - Picks the fight the buyer is already having in their head.
- **Subhead**: dropped "consistently profitable" (sounds like a guarantee), grounded the claim in the actual mechanic — "ranks every bull put and bear call by historical win rate and expected value, ticker by ticker. You see which delta and DTE has actually paid on AAPL, on UNH, on the names you trade — not the average of all of them."
- CTAs unchanged: `Run the scanner` / `How it works`.

### How it works
- Subhead reworded so each mode's job is explicit: "Hunt surfaces today's best spreads, Ticker Analysis shows you why, Watchlist tells you when a fresh setup appears."

### Cards
- **Hunt** body now opens with "A nightly scan" — sets cadence before the reader can mistake it for a streaming tool.
- **Ticker Analysis** body now ends with the workflow tie-in: "Use it to confirm a Hunt result before you put it on."
- **Watchlist** body now describes the actual hook (morning digest + heads-up on new filter-clearing setup).

### Why ticker-specific
- **H2** reframed from a topic ("Why ticker-specific delta and DTE matter.") to a position ("The 30-delta rule is an average. You don't trade the average.").
- Body strengthened with concrete contrasts and a tighter close.

### Sample caption
- "Sample row from the scanner. Live results update against current options chains." → "Illustrative row from the nightly scan. Refreshed each morning before the open."

### Closing CTA
- H2 reworded from `See what the scan finds on your watchlist.` → `See what the scan finds on the names you trade.` (broader, doesn't presuppose the watchlist setup).
- Subhead trimmed of throat-clearing; free-tier specs preserved verbatim.

## Two factual corrections AutoBox-Hermes made to Luke's draft before applying
Luke's "Claims that need evidence before publishing" section flagged both. Verified against the backend code rather than asking Travis:

1. **Scan cadence — Luke wrote "Refreshed each evening after the close."**
   - Verified `backend/src/services/schedulerService.ts:152-167`: cron is `'30 14 * * 1-5'` and `'0 11 * * 1-5'` in `America/New_York` timezone — i.e., **9:30 AM ET (market open)** and a **6:00 AM ET backup**.
   - The honest line is morning, not evening. Changed to: `Refreshed each morning before the open.`

2. **Watchlist alerts — Luke wrote "an alert the moment a new spread clears your filters."**
   - Verified across `backend/src/services/`: there's a `watchlistServiceDB.ts` (read/add/remove on `/api/watchlist`) but **no realtime alert/notification system** is implemented. No push, no email service, no webhook firing on filter match.
   - Digest-only is the honest version. Changed to: `a daily heads-up when a new spread clears your filters.`

These are exactly the kind of fingerprints customer copy can't carry into a paid SaaS product — a buyer who signs up expecting realtime alerts and gets a daily digest is a refund + a one-star review.

## Files changed
- `frontend/src/pages/LandingPage.tsx`: 12 insertions, 12 deletions (in-place copy edits to H1, hero subhead, how-it-works subhead, three card bodies, why-section H2 + body para 1 + body para 2, sample caption, closing H2, closing subhead). No structural / className / route changes.

## Verification
- `cd frontend && npm run build` passes — bundle `dist/assets/index-BogrH6mv.js 454.83 kB` (was `454.49 kB` last run; +0.34 kB from a few longer copy strings), CSS `27.40 kB` (unchanged).
- `cd backend && npm run build` passes (tsc clean).
- `SUPABASE_URL=http://localhost:0 SUPABASE_SECRET_KEY=dev HUNT_USE_FIXTURES=1 npx tsx --test src/services/huntFixtureMode.test.ts` passes `3/3`.
- `git diff --stat HEAD~1 frontend/src/pages/LandingPage.tsx` confirms only the one file changed.
- Public-copy hygiene per `RULES.md` rule 14/15: no internal labels, no SEO scaffolding, no notes-to-self, no AI-smell, no machine fingerprints. The polished customer-facing voice is the whole point of routing through Luke.

## Commit
- `eddc21f copy(landing): Luke polish — pick the fight, ground the claim, fix scan cadence` on branch `autobox/strikesight-scanner-mvp`, pushed to `https://github.com/tbuerky/StrikeSight`.

## What this run did NOT do (deliberately)
- **Public deploy**: StrikeSight is not yet on a public URL. The deploy gate is the production deploy step (Vercel pointing at strikerewind.com), which itself is gated on production env (Supabase prod creds, Polygon API key once approved). A landing-copy polish doesn't justify standing up the production env on its own.
- **Add a pricing block**: Stripe not wired live; pricing copy without working checkout is a bait-and-switch.
- **Add testimonial copy / quotes / "as seen in"**: no real proof yet.
- **Touch the Watchlist alert backend**: would require a new notification system; out of scope for a landing-copy run, and the honest digest framing makes it a clean future feature instead of a promise broken.

## Open owner gates (unchanged from last run)
- `ROTATED: STRIKESIGHT KEYS READY` — rotate the leaked Xata API key in the Xata dashboard so it's invalidated.
- `APPROVED: SUBSCRIBE POLYGON STARTER, $29/MO` — for real options chain data when entering final pre-launch testing.
- Apply Supabase `spread_results` warehouse table SQL via dashboard (HANDOFF step #1).
- PAF: AdSense impressions / eCPM, Google Ads verification clearance + the four-item post-verification queue.

## Next autonomous step
Either step #6 (Ticker Analysis full delta × DTE matrix page) or the Dashboard *content* rebuild (replace legacy `Home.tsx` ticker-analysis launcher with "today's top signal + watchlist quick-view + Run Hunt CTA"). Pick whichever unblocks visible signup motion fastest. Then `DEPLOYMENT.md` / `HTTPS_DEPLOYMENT_GUIDE.md` Supabase rewrites before any production deploy.

## Cash
Current cash balance: $162.45. No spend this run.
