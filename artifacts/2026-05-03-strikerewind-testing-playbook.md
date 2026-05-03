# StrikeRewind testing playbook

**For:** Travis
**Purpose:** Systematic 30–45 min sweep of the live app at `https://www.strikerewind.com` to clear `TESTING COMPLETE: STRIKEREWIND` and unblock marketing + Polygon greenlight.
**How to use:** Walk top-to-bottom. Fill `[PASS]` / `[FAIL: <one-line note>]` after each `Test`. Reply with the failures (or `ALL PASS`) — AutoBox handles each fix in a follow-up run.

---

## Setup (2 min)

- Use a regular Chrome window, **not** incognito (anonymous localStorage userId persists across this session — that is the auth model).
- Open DevTools console (Cmd+Opt+J / Ctrl+Shift+J). Leave it open the whole time. Note any red errors next to the relevant test.
- Have phone or DevTools mobile-emulator (Cmd+Shift+M) ready for the mobile pass at the end.

Architecture context, so failures make sense:
- Auth = anonymous localStorage `userId`. No sign-up form, no email, no password. Identity persists per browser per device.
- Anyone hitting the site is FREE tier (3 analyses/day, 1 scan/day, Hunt blocked behind upgrade wall).
- Frontend: Vercel CDN. Backend: `https://strikerewind-api.onrender.com`. Both verified live.

---

## 1. Landing page → Dashboard (5 min)

**Test 1.1.** Open `https://www.strikerewind.com`. Page renders headline, sample table, FAQ, methodology block.
- Expected: clean load, < 3s, no console errors, no missing images.
- Result: ___

**Test 1.2.** Apex `https://strikerewind.com` 307-redirects to `https://www.strikerewind.com`.
- Expected: address bar lands on www.
- Known soft issue: source-tree canonicals were aligned to www earlier today (commit `1dbebb2`).
- Result: ___

**Test 1.3.** Click any in-page CTA that goes to `/dashboard`.
- Expected: `/dashboard` route renders (Layout-wrapped Home page).
- Result: ___

**Test 1.4.** Open `/privacy` and `/terms` from the footer.
- Expected: both render. Effective date shows on each.
- Result: ___

**Test 1.5.** Open `https://www.strikerewind.com/some-bogus-path-xyz`.
- Expected: NotFound page renders (catches `path="*"`), HTTP 200 from Vercel SPA rewrite.
- Result: ___

---

## 2. Analysis flow — single ticker (8 min)

This is the FREE-tier core flow. Each load counts against the 3/day limit on the backend.

**Test 2.1.** From dashboard, type `AAPL` in the ticker input and submit.
- Expected: Analysis page loads at `/analysis/AAPL`. Strategy matrix renders with Win% and EV% values per strategy/DTE cell.
- Watch for: empty cells, `NaN`, infinite spinner, 5xx in Network tab.
- Result: ___

**Test 2.2.** Try `MSFT`, then `SPY`. Each should render its own matrix.
- Expected: 3 distinct results. After the 3rd, hitting a 4th (e.g. `QQQ`) should return 429 "limit exceeded" surfaced in the UI, not a silent fail.
- Result: ___

**Test 2.3.** Try a deliberately broken ticker like `ZZZZZZZ`.
- Expected: friendly error message, not a thrown stack trace or blank screen.
- Result: ___

**Test 2.4.** On any successful analysis page: do values for the same ticker stay consistent across hard refresh (Cmd+Shift+R)?
- Expected: same Win% and EV% for the same ticker on consecutive loads (deterministic over yfinance + fixtures).
- If values jitter ±1–3% on every refresh: **report this**. The IV path is currently `random` (per Polygon readiness packet); jitter on premium-derived numbers is the visible symptom we knew about. Confirms the credibility risk that gates Polygon.
- Result: ___

---

## 3. Hunt — the upgrade wall (3 min)

**Test 3.1.** Click `/hunt` in the nav.
- Expected on FREE tier: page renders but the Hunt button is disabled or surfaces an upgrade-required state. Backend returns `maxHuntsPerDay: 0` for FREE.
- If Hunt actually starts and returns results on a FREE tier user: **report this**. That breaks the upgrade-wall thesis (Hunt is the paid feature).
- Result: ___

**Test 3.2.** Hunt criteria UI (universe selector, sliders, presets) should still be browsable so the user knows what they would get on upgrade.
- Expected: criteria UI renders cleanly.
- Result: ___

---

## 4. Watchlist (3 min)

**Test 4.1.** From Analysis, try to add the ticker to watchlist.
- Expected on FREE tier: blocked with upgrade prompt. `canSaveWatchlist: false` for FREE.
- Result: ___

**Test 4.2.** Open `/watchlist`.
- Expected: empty state with copy that names the upgrade requirement, not a stack trace or blank screen.
- Result: ___

---

## 5. Account / pricing / Stripe (5 min)

This section will fail until `STRIPE LIVE CONFIGURED: STRIKEREWIND` lands. Run it anyway — surfaces what UX looks like in the broken state.

**Test 5.1.** Open `/account`.
- Expected: page renders. Current tier shows FREE.
- Result: ___

**Test 5.2.** Pricing block on `/account` — does it list both Standard and Pro tiers?
- Expected: both tiers visible. Without live Stripe products, the `/api/stripe/prices` call returns `{}` so the prices may be missing or fall back to hardcoded copy.
- If page crashes / renders blank: **report this**. Should degrade gracefully even with no live prices.
- Result: ___

**Test 5.3.** Click the upgrade button on Standard.
- Expected without live Stripe: graceful error message ("checkout temporarily unavailable" or similar), NOT a thrown alert / stack trace.
- Currently the code path is `alert('Failed to start checkout. Please try again.')` (`Account.tsx:90`) — an `alert()` is functional but ugly; flag if the alert fires.
- Result: ___

**Test 5.4.** Don't actually try to complete a Stripe checkout — products aren't created yet, all clicks will dead-end.

---

## 6. Mobile pass (5 min)

DevTools → toggle device toolbar → iPhone 14 Pro (393×852) or your phone.

**Test 6.1.** Landing page on mobile: hero readable, sample table doesn't overflow horizontally, CTA visible without scroll past the fold.
- Result: ___

**Test 6.2.** Dashboard on mobile: ticker input usable thumb-distance, no clipped buttons.
- Result: ___

**Test 6.3.** Analysis page on mobile: Strategy matrix is the most layout-fragile component. Horizontal scroll inside the matrix is acceptable; whole-page horizontal scroll is not.
- Result: ___

**Test 6.4.** Footer / nav links reachable.
- Result: ___

---

## 7. Browser pass (3 min)

**Test 7.1.** Open `https://www.strikerewind.com` in Safari (Mac or iPhone).
- Expected: same as Chrome. Safari is stricter about same-site cookies and fetch quirks.
- Result: ___

**Test 7.2.** If you have access, Firefox quick check: landing + one analysis run.
- Result: ___

---

## 8. Performance (2 min, optional)

**Test 8.1.** Open DevTools → Network tab → hard-reload the dashboard.
- Watch: any single request > 2s, any 5xx.
- The first `/api/usage` call after a long idle is the most-likely-slow one (Render starter doesn't spin down, but if it ever does the cold start is here).
- Result: ___

**Test 8.2.** Open `/api/health` directly: `https://strikerewind-api.onrender.com/api/health`.
- Expected: `{"status":"ok",...}` in < 300ms.
- Result: ___

---

## How to report

Reply in Discord with one of:

**Option A — all clean:**
> `TESTING COMPLETE: STRIKEREWIND — all pass`

**Option B — issues found:**
> `TESTING COMPLETE: STRIKEREWIND — fix list:`
> `- 2.4: AAPL EV% jitters ±2% on refresh`
> `- 5.2: account page crashes with no prices`
> `- 6.3: matrix overflows page on iPhone`
> `(rest pass)`

AutoBox treats either reply as the gate-clearing signal. Option B kicks off bounded fix runs, one per item. Option A clears the freeze and unblocks the marketing post + Polygon greenlight.

Known issues already on the docket — **do not** report these:
- `api.strikerewind.com` → 404 (DNS not set; SPA bypasses via direct Render URL).
- Stripe upgrade buttons dead-end (covered by `STRIPE LIVE CONFIGURED` gate).
- Random-noise IV under the hood (covered by `artifacts/2026-05-03-strikerewind-polygon-readiness-packet.md`).

---

## Time budget

| Section | Minutes |
|---|---|
| Setup | 2 |
| 1. Landing → Dashboard | 5 |
| 2. Analysis flow | 8 |
| 3. Hunt upgrade wall | 3 |
| 4. Watchlist | 3 |
| 5. Account / pricing | 5 |
| 6. Mobile | 5 |
| 7. Browser | 3 |
| 8. Performance | 2 |
| **Total** | **~36 min** |

If you have less than 36 min, skip 7 and 8 first, then 6. Sections 1–5 are the load-bearing ones.
