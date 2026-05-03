# PAF Google Ads — extend or expire decision packet

Date: 2026-05-03
Project: Profit After Fees
Decision deadline: 2026-05-04 (tomorrow — current $50 total cap end-of-day)
Current cash balance: $162.45

## TL;DR
The PAF Google Ads $50 test cap ends tomorrow. AutoBox cannot pull live ad metrics from this box (no Google Ads API credentials present), so this is an owner-only check. The decision splits cleanly into one of three branches based on what the dashboard shows. Reply formats below are ready to paste.

## What's known going in
- Total approved test cap: **$50.00**.
- Spend as of 2026-04-29 (last reported by Travis): **$15.05** (all from Performance Max, since paused). Search campaign had not spent yet.
- Remaining headroom against the $50 cap as of 2026-04-29: **$34.95**.
- Both campaigns were dark pending advertiser verification (1–10 day Google review, submitted ~2026-04-28). 5 days have now elapsed — verification may have completed at any point in the window.
- Conversion event was broken until 2026-04-28 22:32 UTC (`gtag('event','conversion',...)` was firing on every page load). It was rewired to fire once on first calculator input that night. Performance Max's 3 reported "conversions" pre-date the fix and should be treated as page views, not real input events.
- Active Search campaign: `PAF Search - Fee Calculators`, Maximize Clicks, $1.50 max CPC, $10/day, 8 phrase-match keywords (stripe / paypal / payment fee calculator variants).
- Performance Max campaign was paused by Travis 2026-04-29.

## Step 1 — Travis: pull this in the Google Ads dashboard (≤5 min)
Open account `490-612-1666`, set the date range to `2026-04-26 → today`, and capture the following two rows:

```
Campaign: PAF - Performance Max (PAUSED)
  Status: <paused / verification-blocked / other>
  Spend (date range): $<amount>
  Clicks / Impressions / Conv. (post-2026-04-28 22:32 UTC only): <numbers>

Campaign: PAF Search - Fee Calculators
  Status: <enabled / eligible / paused / verification-blocked / disapproved>
  Spend (date range): $<amount>
  Clicks / Impressions / Conv.: <numbers>
  Avg CPC: $<amount>
  Top 5 search terms (if any visible): <list>
  Any policy / disapproval warnings: <text>
Account: advertiser verification status: <verified / pending / failed>
```

## Step 2 — pick the branch and reply
Use the numbers above to pick exactly one of three branches.

### Branch A — verification still pending OR Search spend is $0 → **EXTEND, same cap**
If account is still under verification, or verification cleared late and the Search campaign hasn't had a fair window to actually run, the test never happened. Extending is the only way to get the data the $15.05 already spent was supposed to buy.

Action in the dashboard:
1. Move the Search campaign budget end date from `2026-05-04` to `2026-05-18` (two clean weeks of post-verification runtime).
2. Keep the $50 total cap (so worst-case incremental spend is `$50 − current spend`, not a fresh $50).
3. Leave Performance Max paused.

Reply format:
```
ADS DECISION: EXTEND, end date 2026-05-18, $50 cap unchanged
Verification status: <verified YYYY-MM-DD / still pending>
Search spend so far: $<amount>
Search clicks / impressions: <numbers>
```

### Branch B — Search ran clean, real signal in hand → **EXTEND, expand cap**
If the Search campaign ran at least 7 days post-verification with CTR ≥ 2%, avg CPC ≤ $2.00, and at least one search term that maps to PAF intent (e.g. "stripe fee calculator", "etsy seller fee"), the test bought useful learning and a second tranche is justified.

Action in the dashboard:
1. Push end date out to `2026-06-04` (next 30 days).
2. Raise total cap to `$150` (3× current; still bounded enough to qualify as a test).
3. Add the negative-keyword block from `artifacts/2026-04-26-google-ads-first-metrics-stop-loss-packet.md` (jobs, careers, developer API, login/support, chargeback/refund disputes, stock/investor terms, PDFs/templates/free downloads).
4. Keep Maximize Clicks; do NOT switch to Smart Bidding (still well under the 50-conversion threshold for learning-reset to be worth it).

Reply format:
```
ADS DECISION: EXPAND, end date 2026-06-04, cap raised to $150, negatives added
Search spend so far: $<amount> (CTR <%>, avg CPC $<amount>, conv <number>)
Top intent search terms: <2–3 examples>
```

NOTE: this branch crosses the BUDGET.md ledger ceiling (current cash $162.45). If approved, AutoBox will record the new $150 cap as a contingent spend in BUDGET.md and stop spending after the cap is reached. If you want a hard floor of cash kept aside, say so in the reply (e.g. `cap raised to $100, $62 cash floor`).

### Branch C — Search ran clean, signal weak or negative → **EXPIRE**
If the Search campaign ran ≥7 days post-verification and the data is bad (CTR <1%, CPC >$3, zero on-page input conversions, irrelevant search terms), the lane is not worth a second tranche. Let the cap expire and roll the bandwidth into evidence-driven directions (AdSense passive earnings, organic indexing, PAF's existing direct traffic).

Action in the dashboard:
1. Pause the Search campaign at `2026-05-04 23:59`.
2. Do not raise the cap.
3. Leave Performance Max paused.

Reply format:
```
ADS DECISION: EXPIRE, paused 2026-05-04
Final Search spend: $<amount> (CTR <%>, avg CPC $<amount>, conv <number>)
Reason: <one-line: e.g. CPC too high / no calculator-intent terms / CTR floor>
```

## What AutoBox does on each reply
- Branch A: log the extension in `BUDGET.md` (no new spend approved — same $50 cap), update `TODO.md`, remove the gate from `OPEN_GATES.md`.
- Branch B: same plus add the new $150 cap as a contingent line in `BUDGET.md` and reissue the stop-loss rules from `artifacts/2026-04-26-google-ads-first-metrics-stop-loss-packet.md` against the new ceiling.
- Branch C: log the final spend in `BUDGET.md`, add a `[DONE]` line to `TODO.md` with the post-mortem, remove the gate. No further AutoBox action on Google Ads until Travis re-opens the lane.

## Why this matters now
- The cap ends tomorrow. If nothing happens, the campaign auto-stops at midnight 2026-05-04 in the campaign's time zone. The $15.05 already spent then becomes the only data the test ever produced — and it was Performance Max in a learning phase with a broken conversion event.
- The Search campaign is the actually-clean test (correct bidding strategy + correct conversion event). Letting it expire silently would cost AutoBox the only paid-search signal PAF has had.
- Five-minute owner action; one-line reply unblocks the next step in either direction.

## Suggested post copy:
> PAF Google Ads $50 test cap ends tomorrow (2026-05-04). The campaign that actually has a chance of producing clean data — `PAF Search - Fee Calculators` — was dark for most of the window pending advertiser verification. I can't pull live metrics from this box (no Google Ads API), so I need 5 minutes of dashboard time from you. Decision packet at `artifacts/2026-05-03-paf-google-ads-extend-or-expire-decision.md` walks through the three branches (extend / expand / expire) with one-line reply formats for each. Default if you do nothing: campaign stops tomorrow at midnight, $15.05 of mostly-noise data is what we keep.
