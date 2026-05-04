# StrikeRewind data-honesty packet — scope correction

**Date:** 2026-05-04 (run 7, addendum to the earlier same-day packet)
**For:** Travis
**Extends:** `artifacts/2026-05-04-strikerewind-pre-launch-data-honesty-decision.md`
**Action options unchanged:** A (HOLD FOR POLYGON) / B (EARLY ACCESS) / C (TIGHTEN COPY). The same single approval line closes the gate.

---

## Why this addendum exists

The original packet scoped the audit to the public landing page and identified 5 lines that make production-pipeline claims with `HUNT_USE_FIXTURES=true`. A second pass against the rest of the customer-visible surface found 6 more operational claims, including one that is structurally different and meaningfully changes the analysis — the PRO plan's "Full S&P 500 scans (no cap)" benefit on `Account.tsx`, which is a direct contractual feature promise tied to a $29.99/mo charge.

Picking C and shipping only the original 5 fixes leaves these surfaces saying the same false thing the original 5 lines said. The trust mismatch the packet was raised to prevent quietly persists on social shares, on the dashboard, in the Hunt UI, and — most importantly — in the pricing card the buyer reads before clicking Upgrade.

---

## Six additional customer-visible claims

| File:line | Surface | Claim today | Same shape? |
|---|---|---|---|
| `frontend/index.html:18` | Social-share preview (og:description) — every X / LinkedIn / Slack share | "Stop selling 30-delta on every ticker. StrikeRewind ranks every bull put and bear call on the S&P 500 by historical win rate and expected value, ticker by ticker." | Yes — mirrors the false "every ... on the S&P 500" implication of completeness. |
| `frontend/index.html:26` | Social-share preview (twitter:description) | Same content as L18. | Same fix. |
| `frontend/src/pages/LandingPage.tsx:207` | FAQ "Why only bull put and bear call?" | "...The scan covers the S&P 500 every night so you can see which delta and DTE has paid on the names you trade — narrow on purpose." | Yes — operational "covers the S&P 500 every night" with no scan running today. |
| `frontend/src/pages/Home.tsx:143` | Dashboard ticker-search hero subhead | "Enter any S&P 500 ticker to see its full delta × DTE spread matrix and top historical setups." | Yes — "any S&P 500 ticker" is true under Polygon, false today (only AAPL / MSFT / UNH return data; everything else fails). |
| `frontend/src/pages/Home.tsx:248` | Dashboard "Top setup of the day" empty-state | "Run a hunt to see the spread that scored highest on win rate and expected value across the S&P 500." | Yes — "across the S&P 500" implies index-wide coverage. |
| `frontend/src/pages/Hunt.tsx:79` | Hunt universe filter chip | `{ value: 'SP500', label: 'S&P 500', description: '500 largest US companies', count: '500+ stocks' }` | Yes — UI explicitly tells the buyer the SP500 filter covers 500 stocks. |
| `frontend/src/pages/Account.tsx:37` | STANDARD plan "not included" list | `'Full S&P 500 scans'` — STANDARD specifically does not get this; PRO does. | Different shape — pricing-card cross-reference to L44. |
| `frontend/src/pages/Account.tsx:44` | PRO plan benefits | `'Full S&P 500 scans (no cap)'` — direct contractual feature promise tied to $29.99/mo billing. | **Different shape — pricing claim, highest chargeback-exposure surface.** |

---

## Why the Account.tsx pricing benefit is different

Marketing copy ("nightly scan over the full S&P 500") is a positioning claim — false today, but rewritable to capability copy that's true on fixtures and on Polygon ("ranks bull put and bear call credit spreads ... ticker by ticker").

The PRO plan benefit "Full S&P 500 scans (no cap)" is structurally different. A buyer reads that line, clicks Upgrade, and pays $29.99/mo against it. There is no rewording that simultaneously (a) keeps the buyer informed about what they are paying for and (b) is true on the current 3-fixture-ticker output.

That puts the chargeback exposure on Account.tsx higher than on any other surface in this audit. The fix has to be one of:

1. **Disable the upgrade button until production data is live** — keeps the pricing copy as-is for buyers seeing what's coming, removes the ability to actually pay against the false promise. One env-flag flip on the day Polygon goes live.
2. **Soften the pricing copy to non-operational wording** — e.g., "Maximum-coverage scans" — still vague, slightly lossy, and arguably more confusing to evaluate against the FREE/STANDARD comparison.
3. **Hold launch entirely** (Option A) — sidesteps the issue.

---

## Revised Option C — concrete edit list

If Travis picks C, the full edit list is:

**Original 5 lines (unchanged from the first packet):**
- `LandingPage.tsx:38` hero rewrite
- `LandingPage.tsx:72` Hunt tile rewrite
- `LandingPage.tsx:144` example-row caption rewrite
- `LandingPage.tsx:153` calculation panel "Every night the scanner walks..." rewrite
- `index.html` `<meta name="description">` rewrite
- Plus the 1-line status note in the calculation panel

**Added by this scope correction:**

| Line | Before | After |
|---|---|---|
| `index.html:18` og:description | "Stop selling 30-delta on every ticker. StrikeRewind ranks every bull put and bear call on the S&P 500 by historical win rate and expected value, ticker by ticker." | "Stop selling 30-delta on every ticker. StrikeRewind ranks bull put and bear call credit spreads by historical win rate and expected value, ticker by ticker." |
| `index.html:26` twitter:description | Same as L18 today. | Same fix as L18. |
| `LandingPage.tsx:207` FAQ | "...The scan covers the S&P 500 every night so you can see which delta and DTE has paid on the names you trade — narrow on purpose." | "...The S&P 500 scan refreshes each market day so you can see which delta and DTE has paid on the names you trade — narrow on purpose." |
| `Home.tsx:143` dashboard subhead | "Enter any S&P 500 ticker to see its full delta × DTE spread matrix and top historical setups." | "Enter an S&P 500 ticker to see its full delta × DTE spread matrix and top historical setups." (drops "any" — true once Polygon is live; pre-launch the ticker set is whatever's plumbed in.) |
| `Home.tsx:248` Top-setup empty state | "Run a hunt to see the spread that scored highest on win rate and expected value across the S&P 500." | "Run a hunt to see the spread that scored highest on win rate and expected value." (drops "across the S&P 500" — implicit by the universe filter once it's restored to 500+ stocks; true on whatever universe the scan currently covers.) |
| `Hunt.tsx:79` SP500 filter | `{ value: 'SP500', label: 'S&P 500', description: '500 largest US companies', count: '500+ stocks' }` | `{ value: 'SP500', label: 'S&P 500', description: '500 largest US companies' }` (drop the `count` field; the chip stops claiming a specific stock count until production data is live). Restore `count: '500+ stocks'` the day Polygon goes live. |

**Account.tsx pricing-benefit hardening (the load-bearing addition):**

Recommended sub-step: keep the pricing copy as-is in `Account.tsx` (so buyers see what's coming) but disable the PRO + STANDARD upgrade buttons until Polygon is live. Two implementation paths:

- **Env-flag:** Vercel env var `VITE_ENABLE_PAYMENTS=false` on the `strikerewind` project. `Account.tsx:77 handleUpgrade(...)` is already short-circuited by the `prices` object being missing; explicitly gating the button render on `import.meta.env.VITE_ENABLE_PAYMENTS === 'true'` with a tooltip ("Paid tiers go live with the production scan") is one Edit + one Vercel env flip.
- **New flag `VITE_PAID_TIERS_LIVE`:** clean separation from the existing `VITE_ENABLE_PAYMENTS` flag (which is currently `true` and was set during deploy). Adding a second flag is more code but keeps the existing flag's semantics.

Either way, the day Polygon's first nightly batch verifies clean, one env flip turns paid tiers back on, and one revert pulls out the "pre-launch" copy hedges from the dashboard / Hunt filter. ~15-minute reversal.

**No "Beta" or "Early access" framing anywhere on customer-visible surfaces.** That preserves Option C's spirit — the only difference from the first packet is that the upgrade buttons go quiet for ~30 days while the production scan ships.

---

## How this changes the recommendation

Original recommendation: pick C (smallest reversible change).
Revised recommendation: **still C, with the Account.tsx upgrade-button gate as a required sub-step.**

If the upgrade-button gate feels too close to Option B in spirit, here's the actual difference:

- **Option B** brands the product as "Early access" customer-facing — buyers see a "Beta" / "Waitlist" label, and that label is hard to retire post-launch.
- **Revised Option C** keeps every customer-visible word brand-clean. Buyers see normal pricing copy and a normal-looking upgrade button. The button is just disabled with a quiet tooltip until production data is live. No "Beta" badge, no "Early access" headline.

If even the disabled-upgrade approach feels like too much hedging, the honest fall-through is Option A (hold launch). At that point the only thing distinguishing C from B is brand-label preference, and the operational fix on the buying surface is identical.

---

## Updated action table

| Reply | AutoBox does |
|---|---|
| `LAUNCH POSTURE: HOLD FOR POLYGON` | Option A. Adds gate `SUBSCRIBE: POLYGON STARTER, $29/MO`. Begins backend work on `PolygonOptionsProvider` once Travis approves the spend. All copy stays as-is. |
| `LAUNCH POSTURE: EARLY ACCESS` | Option B. Lands the early-access landing-page edit + waitlist CTA + Stripe checkout disable for paid tiers. Single autonomous run. |
| `LAUNCH POSTURE: TIGHTEN COPY` | Revised Option C: 11 file:line copy edits across 4 files + 1-line status note in the calc panel + flip `VITE_ENABLE_PAYMENTS=false` on Vercel until Polygon is live. Single autonomous run + Vercel env flip. |

---

## Estimated time (revised)

Single autonomous run for the revised Option C path:
- 11 surgical file:line edits
- 1 status-line addition in `LandingPage.tsx` calc panel
- `Account.tsx` upgrade button gate (one render-conditional + tooltip)
- `vercel env rm VITE_ENABLE_PAYMENTS production --yes && vercel env add VITE_ENABLE_PAYMENTS production` with value `false`
- Build + deploy + live-verify

No additional Travis time beyond picking the option. No additional Polygon-spend approval needed for the C path itself (still required separately if/when the production scan ships).

---

## Suggested post copy

> StrikeRewind launch readiness — second pass on the data-honesty packet found 6 more operational claims beyond the 5 in the first packet (social previews, FAQ, dashboard, Hunt filter, AND the Pro plan's "Full S&P 500 scans (no cap)" pricing benefit — direct $29.99/mo chargeback risk that no rewording fixes). Three paths still: A hold for Polygon, B early access on fixtures, C tighten copy to be true now and later. C now ships with a sub-step that disables the paid-tier upgrade buttons until Polygon is live (no "Beta" branding). I still recommend C. Reply `LAUNCH POSTURE: TIGHTEN COPY` (or HOLD FOR POLYGON / EARLY ACCESS) and I'll ship it. Updated packet: `artifacts/2026-05-04-strikerewind-data-honesty-scope-correction.md`.

---

## Cash balance

$162.45. No spend in this run. Render starter still accruing ≈ $0.23/day toward end-of-cycle invoice.
