# PAF Google Ads — data-in recommendation

Date: 2026-05-07
Project: Profit After Fees
Campaign: `PAF Search - Fee Calculators` (account `490-612-1666`)
Current cash balance: $162.45
Approved cap: $50 total (only $5.90 spent — $44.10 still inside the existing approval)

## TL;DR
Travis pulled the dashboard 2026-05-07. The campaign hit its 2026-05-04 end date and is likely auto-paused. The numbers in hand show a clean *quality* signal but the test never bought enough volume to be meaningful. The right call is **extend the existing $50 cap with a higher max-CPC bid** to spend the remaining $44.10 of already-approved budget on real volume, then decide expand-vs-expire on actual conversion data.

## What the data actually says (Apr 26 → May 3)

| Metric | Value | Branch B threshold | Verdict |
|---|---:|---:|---|
| Impressions | 129 | (no floor) | Thin — ~16/day, auction rarely bid us in |
| Clicks | 4 | (no floor) | Statistical noise for conversion math |
| Spend | $5.90 | n/a | $0.74/day actual vs. $10/day budget — budget never bound |
| CTR | 3.10% | ≥ 2% | **Pass** — above industry average |
| Avg CPC | $1.48 | ≤ $2.00 | **Pass** |
| Conversions | 0 | ≥ 1 intent term mapped | **Inconclusive** — 4 clicks is below the floor where we'd expect even one conv |

The two quality criteria from the 2026-05-03 packet's Branch B (`CTR ≥ 2%`, `CPC ≤ $2`) are met. The volume criterion (`≥ 7 days post-verification with real signal`) is not — the campaign ran $0.74/day actual against a $10/day budget, meaning Google rarely bid us into the auction even after verification cleared. Bidding ceiling, not duration, was the binding constraint.

## Why expire-now is wrong
Branch C (expire) needs *negative signal* — bad CTR, bad CPC, irrelevant search terms. We have *no signal*. Calling it dead at 4 clicks throws away the only paid-search lane PAF has tested, with $44.10 of the existing approval still on the table. The CTR is genuinely promising; it deserves real volume before we judge it.

## Why a fresh full extend is unnecessary
Branch A (extend, same cap) was written for the case where verification ate the window. That happened. But re-running the same setup will reproduce the same outcome — the bid was the binding constraint, not the calendar.

## Primary recommendation — one approval line

**Extend end date to 2026-05-21 and raise max CPC from $1.50 to $3.00. Keep total $50 cap unchanged.**

- $3.00 max CPC is still well below calculator-intent benchmark ($2–$8 typical for SaaS calculator keywords). It buys auction wins, not waste.
- Total approved spend does not change. Worst case, we burn the remaining $44.10 inside the existing approval. AutoBox does not cross a new spending gate.
- Two clean weeks at a binding bid should produce ≥ 30–60 clicks. That is the volume floor where conversion signal becomes interpretable.
- After 2026-05-21, the data either supports Branch B (expand cap to $150 next tranche) or Branch C (expire with real evidence). Either way we exit the inconclusive zone we're in now.

### Owner action (≤ 5 min in Google Ads dashboard)
1. Open `PAF Search - Fee Calculators` in account `490-612-1666`.
2. Resume the campaign if it auto-paused on 2026-05-04.
3. Edit the campaign budget end date: `2026-05-04` → `2026-05-21`.
4. Edit the bid strategy: max CPC `$1.50` → `$3.00` (Maximize Clicks, unchanged otherwise).
5. Confirm total spend cap stays at `$50.00`.

### Reply format
```
ADS DECISION: EXTEND TO 2026-05-21, MAX CPC $3.00, $50 CAP UNCHANGED
Resumed: <yes / no — needed verification reset>
Final May-3 numbers confirmed: 129 imp / 4 clicks / $5.90 / 3.10% CTR / 0 conv
```

## Alternatives Travis can override to (plain text, not parallel approvals)

- **Branch C (expire)** — if Travis is done with this lane regardless of signal. Reply `ADS DECISION: EXPIRE, final spend $5.90, reason <text>`. AutoBox logs the post-mortem and removes the gate. Lost cost: $5.90 + 8 days of verification friction.
- **Same-cap, same-bid extend (original Branch A)** — if Travis wants more conservative play. Reply `ADS DECISION: EXTEND TO 2026-05-21, $50 CAP UNCHANGED, BID UNCHANGED`. Predicted outcome: another two weeks of $0.74/day, no new conversion data. Likely lands us back in this same packet on 2026-05-22.
- **Broaden keywords + add negatives** — separate concern. Once volume is unlocked by the bid raise, the negative-keyword block from `artifacts/2026-04-26-google-ads-first-metrics-stop-loss-packet.md` becomes the next move.

## What AutoBox does on each reply

- `EXTEND TO 2026-05-21, MAX CPC $3.00, $50 CAP UNCHANGED` — note the bid raise in `BUDGET.md` (no new approval line; cap unchanged). Re-arm the stop-loss rules from the 2026-04-26 packet against the existing $50 ceiling. Re-pull data 2026-05-22 and ship the next decision packet (expand vs. expire).
- `EXPIRE` — record final spend, post-mortem entry in `TODO.md`, remove gate. No further AutoBox work on Google Ads until Travis re-opens the lane.
- `EXTEND ... BID UNCHANGED` — same as the conservative path, schedule 2026-05-22 re-pull.

## What still does not need approval
- AdSense Auto Ads remain on; passive earnings continue to accrue against the AdSense threshold.
- Conversion event fix from 2026-04-28 is still live and verified by smoke (run 5 of 2026-05-06 confirmed `gtag` fires once, `send_to=AW-18121518600/WxyuCLjh56McEIjcgcFD`).

## Suggested post copy:
> PAF Google Ads data is in: 129 imp / 4 clicks / $5.90 / 3.10% CTR / 0 conv. CTR + CPC pass Branch B's quality bar but volume was too thin to read conversions. The bid was the binding constraint, not the calendar. Recommend EXTEND to 2026-05-21 with max CPC raised $1.50 → $3.00, $50 cap unchanged. Five-min dashboard edit, no new spend approval needed. Packet at `artifacts/2026-05-07-paf-google-ads-data-in-recommendation.md`. Reply `ADS DECISION: EXTEND TO 2026-05-21, MAX CPC $3.00, $50 CAP UNCHANGED`. Cash $162.45.
