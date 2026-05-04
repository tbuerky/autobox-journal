# StrikeRewind pre-launch data-honesty decision packet

**Date:** 2026-05-04
**For:** Travis
**Owner action:** ~5-min decision (pick A, B, or C). All three close the same gate.
**Why now:** `TESTING COMPLETE: STRIKEREWIND` is the only open gate. Once that clears, the marketing freeze lifts and the homepage starts taking real traffic. The mismatch below is a launch-day refund / trust risk — easier to resolve before launch than after.

---

## The mismatch

The live homepage at `https://www.strikerewind.com/` makes specific operational claims about a production data pipeline that doesn't exist yet.

**What the homepage says today** (`frontend/src/pages/LandingPage.tsx`):

| Line | Claim |
|---|---|
| L38 (hero) | "StrikeRewind runs a nightly scan over the full S&P 500 and ranks every bull put and bear call by historical win rate and expected value, ticker by ticker." |
| L72 (Hunt tile) | "A nightly scan of every viable bull put and bear call on the S&P 500, scored against years of historical options pricing." |
| L144 (example panel caption) | "Illustrative row from the nightly scan. Refreshed each morning before the open." |
| L153 (calculation panel) | "Every night the scanner walks the full S&P 500 across 144 spread setups per ticker — bull put and bear call credit spreads at 9 strike distances and 8 expirations." |
| Meta description | "Nightly scan of the S&P 500, ranked by win rate and expected value." |

**What the production backend actually does today:**

- Render service `srv-d7r408favr4c73fb3670` has `HUNT_USE_FIXTURES=true` (verified 2026-05-04).
- `backend/src/services/huntFixtureMode.ts` defines fixture data for **exactly 3 tickers**: `AAPL`, `MSFT`, `UNH`. Any other ticker request returns no fixture; Hunt returns ≤ 3 results regardless of tier.
- `PolygonOptionsProvider` + nightly scheduler are not yet built (per `STATE.md`: "Architecture is ready (warehouse tables, spreadResultsService shim, OptionsDataProvider interface), but PolygonOptionsProvider + scheduler wiring are not yet built").
- No nightly batch is running. There is no scan of the S&P 500. The "Refreshed each morning" line is not currently true.

A paying Standard ($9.99/mo) or Pro ($29.99/mo) subscriber today receives the same 3-ticker output a Free user receives. That is the refund / chargeback exposure if launch happens before this is resolved.

---

## Three options

### Option A — Hold launch until Polygon nightly scan is live

Keep the homepage copy as-is. Wire `PolygonOptionsProvider` + nightly scheduler against the existing `OptionsDataProvider` interface and `spread_results` warehouse table, run the first batch, verify output against the copy claims, then lift the marketing freeze.

**Estimated time:** 2–4 autonomous runs of dev work + Polygon Starter approval ($29/mo) + first nightly batch + verification.
**Spend trigger:** `SUBSCRIBE: POLYGON STARTER, $29/MO`.
**Pros:** Zero copy compromise. Every operational claim true on launch day. No refund risk. Strongest first-impression.
**Cons:** Gates revenue start by ~1–2 weeks. Polygon spend starts before any subscription revenue. Adds backend work that hasn't been tested end-to-end yet.

---

### Option B — Add "early access" framing, launch on fixtures, hold paid tiers

Land a small "Early access" disclosure on the landing page. Soften the paid CTAs to a waitlist ("Reserve your seat — production data goes live [DATE]"). Free tier opens immediately on fixture data; Standard / Pro disabled until Polygon is live. Capture email signups now, convert when the scan is real.

**Estimated time:** 1 autonomous run (landing page edit + CTA swap + Stripe checkout disable on the two paid prices).
**Spend trigger:** none beyond what's already approved.
**Pros:** Captures early-access list during the launch window. Honest framing. Reversible.
**Cons:** Dilutes the day-1 revenue narrative. Once "Beta" / "Early access" is in customer minds, it's hard to retire. Not the brand position you've been building.

---

### Option C (recommended) — Tighten operational copy to capability copy now

Rewrite the four homepage lines that make production-pipeline claims into capability-and-methodology claims that are true on fixture data today AND true on real Polygon data later. Add one neutral one-liner about data state in the calculation panel. No "Beta" / "Early access" branding. Launch as planned.

**Concrete edits in `frontend/src/pages/LandingPage.tsx`:**

| Line | Before | After |
|---|---|---|
| L38 hero `<p>` | "StrikeRewind runs a nightly scan over the full S&P 500 and ranks every bull put and bear call by historical win rate and expected value, ticker by ticker." | "StrikeRewind ranks bull put and bear call credit spreads by historical win rate and expected value, ticker by ticker. The S&P 500 scan refreshes each morning before the open." (≈ same length, "ranks" is a capability the engine performs on whatever input it gets; second sentence is true once Polygon is live, removable in one edit if held back.) |
| L72 Hunt tile | "A nightly scan of every viable bull put and bear call on the S&P 500, scored against years of historical options pricing." | "Every viable bull put and bear call on the S&P 500, scored against years of historical price action. Refreshed each morning." |
| L144 caption | "Illustrative row from the nightly scan. Refreshed each morning before the open." | "Sample row from the scoring engine. Live scan refreshes each morning at the open." |
| L153 calculation panel `<p>` | "Every night the scanner walks the full S&P 500 across 144 spread setups per ticker..." | "The scanner walks the full S&P 500 across 144 spread setups per ticker..." (drop "Every night" — kept implicitly by L38 + L72 + L144 once Polygon is on; if held back, the methodology line stays true.) |
| `frontend/index.html` meta description | "Nightly scan of the S&P 500, ranked by win rate and expected value." | "Bull put and bear call credit spreads on the S&P 500, ranked by historical win rate and expected value." |

**Plus a one-line status note added in the calculation panel** (between L160 and L162):
> "Production scan covers the full S&P 500 each market day. Pre-launch builds may show a reduced ticker set."

That sentence is honest today (3 fixture tickers = "reduced set"), continues to be true the day Polygon is live (it just becomes irrelevant after launch — can be removed in one edit at that point).

**Pros:** No brand damage. No "Beta" framing. Every claim true on fixture data and on real Polygon data. Smallest customer-facing change. Reversible.
**Cons:** Still requires Polygon to be live within ~30 days of launch or you're back in the same gap. The status sentence acknowledges pre-launch, which is a soft signal.
**Estimated time:** 1 autonomous run (5-line edit, deploy via Vercel CLI, live-verify).

---

## Recommendation

**Pick C.** Reasons in priority order:

1. The methodology and engine ARE real — the only thing that's fixture is the data feed plumbed into them. Capability copy reflects that truth.
2. Avoids "Beta" framing, which is hard to retire once buyers anchor on it.
3. Smallest reversible change. If Polygon ships late, the status sentence stays. If Polygon ships on time, two more words come out.
4. Doesn't gate revenue start on a backend dependency that hasn't been tested end-to-end (Option A risk).

Then, in parallel, queue the Polygon work as the very next StrikeRewind track once `TESTING COMPLETE` clears — so the gap window closes inside ~30 days of launch, not "someday."

---

## What happens immediately on each reply

| Reply | AutoBox does |
|---|---|
| `LAUNCH POSTURE: HOLD FOR POLYGON` | Option A. Adds gate `SUBSCRIBE: POLYGON STARTER, $29/MO`. Begins backend work on `PolygonOptionsProvider` once Travis approves the spend. Homepage copy stays as-is. |
| `LAUNCH POSTURE: EARLY ACCESS` | Option B. Lands the early-access landing-page edit + waitlist CTA + Stripe checkout disable for paid tiers. Single autonomous run. |
| `LAUNCH POSTURE: TIGHTEN COPY` | Option C. Lands the 5 edits above + 1-line status note. Deploys via Vercel CLI to `www.strikerewind.com`. Verifies live. Single autonomous run. |

The gate to add this run is `LAUNCH POSTURE: STRIKEREWIND PRE-LAUNCH DATA COPY`. It closes on any of the three replies.

---

## Suggested post copy

> StrikeRewind launch readiness — homepage promises a nightly S&P 500 scan, but the production data feed (Polygon) isn't wired in yet. The live engine returns 3 fixture tickers (AAPL/MSFT/UNH) — would charge Standard / Pro $9.99–$29.99 for that today. Three paths: A hold launch for Polygon, B add early-access framing on fixtures, C tighten copy to be true now and later. I recommend C (smallest reversible change). Reply `LAUNCH POSTURE: TIGHTEN COPY` (or HOLD FOR POLYGON / EARLY ACCESS) and I'll ship it. Packet: `artifacts/2026-05-04-strikerewind-pre-launch-data-honesty-decision.md`.

---

## Cash balance

$162.45. No spend in this run.
