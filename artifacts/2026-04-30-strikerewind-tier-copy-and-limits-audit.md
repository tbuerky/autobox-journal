# StrikeRewind — Tier copy + tier limits pre-deploy audit (2026-04-30)

## Why this matters now

The deploy gate `APPROVED: DEPLOY ON VERCEL+RENDER STARTER, $7/MO` is open. The moment Travis approves it, `strikerewind.com` goes live with the current `LandingPage.tsx` / `Account.tsx` / `usageServiceDB.ts` exactly as they sit on `autobox/strikerewind-rename`.

This audit caught two pre-deploy customer-facing-promise-vs-built-reality mismatches and one buyer-credibility risk on the conversion-to-paid surface. They are the same shape as the PAF "no tracking" claim Travis flagged 2026-04-27 — public copy says X, the system does not-X. Cleaner to lock the corrections in one Discord turn than to ship live and patch.

Stripe stays in test mode for the first deploy per the deploy-architecture packet, so no real revenue is at stake yet — but the live URL still surfaces the broken promises to the very first buyer who lands on it from any source.

---

## Issue 1 — FREE Hunt promise vs FREE Hunt block (functional bug)

**Customer-facing promise (multiple surfaces):**
- `frontend/src/pages/LandingPage.tsx:38` (hero subhead): "...runs a nightly scan over the full S&P 500 and ranks every bull put and bear call by historical win rate and expected value..."
- `frontend/src/pages/LandingPage.tsx:156` (bottom CTA): "Free tier gets you the top 5 Hunt results per day, 2 ticker lookups per day, and 1 year of history. No card required."
- `frontend/src/pages/Account.tsx:20` (FREE tier feature list): `"Top 5 Hunt results per day (S&P 500)"`
- `config/HANDOFF.md` 2026-04-28 product-defining session (locked spec): "Free: top 5 Hunt results/day (S&P 500 only), 2 ticker lookups/day (1yr history only)"

**Backend reality:** `backend/src/services/usageServiceDB.ts:25`
```ts
FREE: {
  ...
  maxHuntsPerDay: 0, // Hunt is premium only
  ...
}
```

`backend/src/services/usageServiceDB.ts:181-188` is the enforcement path called from `backend/src/index.ts:559`:
```ts
if (limits.maxHuntsPerDay === 0) {
  return {
    allowed: false,
    remaining: 0,
    limit: 0,
    reason: 'Hunt feature requires STANDARD or PRO subscription'
  };
}
```

When the hardcoded dev override (`usageServiceDB.ts:18 DEV_MODE = true`) is removed for production, every signup through the landing page CTA → `/dashboard` → `Run Hunt` clicks straight into a hard "STANDARD or PRO subscription required" block on the headline feature the landing page just sold them.

**Recommended fix:** `FREE.maxHuntsPerDay: 0` → `FREE.maxHuntsPerDay: 1`. Free tier runs one Hunt per day, the result set is then truncated to the top 5 elsewhere (the result-truncation policy is a separate decision and is not currently wired — flagged as Issue 4 below). One Hunt/day matches the landing page's daily framing ("top 5 Hunt results per day") and the locked spec; it does not give free users unlimited Hunt access.

---

## Issue 2 — `DEV_MODE = true` hardcoded in tier-enforcement service

`backend/src/services/usageServiceDB.ts:18`:
```ts
private readonly DEV_MODE = true; // Force unlimited access
```

Used at `usageServiceDB.ts:171-173` (and equivalents for analysis/scan limits) to bypass tier enforcement entirely. There is no env-driven escape — the flag is hardcoded.

If the production deploy ships with this flag still `true`, every tier limit is silently disabled. FREE users get unlimited everything. Free → paid conversion never has a paywall to convert against. Anyone who finds the live URL is on the implicit "Pro for free, indefinitely" plan. This bricks the entire freemium business model the moment the production URL is shared anywhere.

If the deploy ships with this flag manually flipped to `false`, Issue 1 fires immediately for every free signup.

**Recommended fix:** make it env-driven, default-safe-for-prod:
```ts
private readonly DEV_MODE = process.env.NODE_ENV !== 'production';
```

This way `vercel deploy --prod` / Render production runtime gives `NODE_ENV=production` automatically, which sets `DEV_MODE = false` automatically, which then enforces the Issue-1-corrected `FREE.maxHuntsPerDay: 1`. Local dev stays unchanged (no `NODE_ENV` set → defaults to dev → DEV_MODE on). Same default-safe pattern Travis approved for the PAF conversion-fire dedupe (`conversionFired` boolean default to `false`, no env override needed for the conservative path).

---

## Issue 3 — `Account.tsx` Pro tier features advertise capabilities not built

`frontend/src/pages/Account.tsx:40-50`:
```ts
{
  name: 'PRO',
  price: 29.99,
  features: [
    'Everything in Standard',
    'Real-time options data',
    'Price + IV alerts',
    'CSV exports',
    'API access',
  ],
  notIncluded: [],
},
```

Capability check (greps + file reads on `backend/src` and `frontend/src`):

| Pro feature claim | Built? | Evidence |
|---|---|---|
| Real-time options data | NO | Architecture is EOD nightly batch (locked HANDOFF 2026-04-28: "Polygon API called once/night in batch job, never at user request time"). Travis 2026-04-28: "EOD is sufficient — no real-time needed." No real-time pipeline exists. Direct contradiction of locked architecture. |
| Price + IV alerts | NO | Project-wide grep for `alertService\|sendAlert\|priceAlert\|notify` returns 0 backend matches (only `Privacy.tsx` mentions the word). No alerting code path. The landing page Watchlist copy correctly says "daily heads-up when..." (digest-style, Luke verified 2026-04-29) — but Account.tsx still claims "alerts" as a Pro feature. |
| CSV exports | NO | Project-wide grep for `csv\|exportToCsv\|toCsv\|writeCSV` returns 0 implementation matches. |
| API access | NO | Project-wide grep for `apiKey\|api_key\|x-api-key` returns one match in `stripeServiceDB.ts` (Stripe SDK auth, not customer-facing API). No public API surface. |

`Account.tsx:37` STANDARD `notIncluded` list also lists three of these — meaning STANDARD's "you're missing this" pitch points users at features that don't actually exist on PRO either.

**Recommended pre-deploy correction (PRO features list):** replace the four false claims with capability-honest claims tied to what is actually built:
```ts
features: [
  'Everything in Standard',
  'Watchlist daily digest (unlimited tickers)',
  'Earnings-aware filters',
  'Weekly curated spread report',
],
```

Mapping:
- "Watchlist daily digest" — matches the landing-page Watchlist promise Luke wrote ("daily heads-up when a new spread clears your filters")
- "Earnings-aware filters" — flagged in HANDOFF Pro/Ultra tier spec ("earnings-aware filters")
- "Weekly curated spread report" — flagged in HANDOFF Pro/Ultra tier spec ("weekly curated spread report (AutoBox's own scan = premium product feature)")

These three are roadmap items the system can credibly deliver on (digest is a scheduled job over the existing scheduler; earnings-aware is a filter on existing analysis data; curated report is AutoBox's own scan output). They land closer to what's actually built or near-buildable, vs. real-time / alerts / CSV / API which are entirely separate engineering tracks.

`Account.tsx:37` STANDARD `notIncluded` list should mirror the corrected PRO claims. Current STANDARD `notIncluded`: `['Real-time options data', 'Price + IV alerts', 'API access']` — should become `['Daily digest', 'Earnings-aware filters', 'Weekly curated report']`.

If Travis instead wants to keep "Real-time options data" as a true future Pro feature (would require subscribing to MarketData.app Trader plan or Polygon Developer plan, not the recommended Polygon Starter $29/mo), that's a separate gate and a separate paragraph on the landing page.

---

## Issue 4 (advisory only — not blocking deploy) — Free Hunt result truncation policy not implemented

The landing page promises "top 5 Hunt results per day". The Hunt API does not currently truncate results by tier. A fix to Issue 1 (FREE.maxHuntsPerDay: 1) lets a free user run one Hunt and see all results from that scan — which on the S&P 500 is hundreds of rows, not 5.

This is acceptable for first deploy if Travis wants — free users see the full power of the product on day one, which can drive conversion. But it does not match the landing page's "top 5" framing exactly.

**Two paths:**
- (A) Drop "top 5" framing on the landing page bottom CTA — say "one daily Hunt, S&P 500, 1 year of history" instead. Honest, no truncation engineering needed.
- (B) Keep "top 5" framing, add server-side truncation in Hunt API by tier. Engineering: ~10 lines in `index.ts` after the result set is built.

Recommended: (A) for first deploy (less code, cleaner signal). (B) later if conversion data shows free users pulling huge result sets and not converting.

---

## Recommended Travis decision (single approval line)

Approve all three Issue-1/2/3 corrections as packaged above. AutoBox lands the changes on `autobox/strikerewind-rename` in one bounded run and pushes; deploy gate stays open for Travis's separate approval of the deploy itself.

**Approval line:** `APPROVED: STRIKEREWIND TIER COPY + LIMITS PRE-DEPLOY`

Post-approval AutoBox follow-up (one autonomous run):
1. `usageServiceDB.ts:18` — `DEV_MODE = process.env.NODE_ENV !== 'production'`
2. `usageServiceDB.ts:25` — `FREE.maxHuntsPerDay: 0` → `FREE.maxHuntsPerDay: 1`
3. `Account.tsx:40-50` — replace PRO features list with the four capability-honest claims above
4. `Account.tsx:37` — replace STANDARD `notIncluded` list to mirror corrected PRO claims
5. `LandingPage.tsx:156` — drop "top 5" framing per Issue 4 path A → "one daily Hunt across the S&P 500, 2 ticker lookups, 1 year of history. No card required."
6. Backend build passes; frontend build passes; fixture tests `3/3`
7. Commit + push to `autobox/strikerewind-rename`
8. Update state files

If Travis pushes back on any of the three issues (e.g. wants real-time data on Pro after all), AutoBox revises the packet and re-surfaces.

---

## Suggested post copy:

> Pre-deploy audit on StrikeRewind found three customer-facing-promise-vs-built-reality mismatches that would surface the moment `strikerewind.com` goes live (same shape as the PAF "no tracking" claim you flagged): FREE tier landing-page promise of "top 5 Hunt results per day" hits a hard "STANDARD or PRO subscription required" block in the backend, the dev override that masks every tier limit is hardcoded `true` (no env escape), and the Pro tier feature list claims four capabilities that aren't built (real-time data, price/IV alerts, CSV exports, API access). Packet at `artifacts/2026-04-30-strikerewind-tier-copy-and-limits-audit.md` has the exact line numbers and recommended one-line corrections. Reply `APPROVED: STRIKEREWIND TIER COPY + LIMITS PRE-DEPLOY` to land all three fixes in one bounded run before the deploy gate fires.
