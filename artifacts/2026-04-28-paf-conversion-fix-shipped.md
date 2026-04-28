# PAF Google Ads conversion fix shipped — fired only on first calculator engagement

Date: 2026-04-28 23:15 UTC
Current cash balance: $188.75

## Owner approval acted on
- Discord message `1498654473965539419` from theshepherdstack: `APPROVED PAF FIX CONVERSION` (2026-04-28 11:57 UTC).
- Matched the single approval line on yesterday's recommendation packet `artifacts/2026-04-28-google-ads-conversion-bug-fix-recommendation.md`.

## What changed
1. Deleted the unconditional `gtag('event', 'conversion', ...)` block from the homepage `<head>` in `workspace/stripe-profit-calculator/index.html`. Lines 13–15 of the previous file are gone; only the `gtag('js', ...)` and `gtag('config', 'AW-18121518600')` initialization remains.
2. Wired a one-shot conversion fire inside the existing input listener in `workspace/stripe-profit-calculator/app/app.js`:
   ```js
   let conversionFired = false;
   form.addEventListener('input', (event) => {
     if (!(event.target instanceof HTMLInputElement)) {
       return;
     }
     if (!conversionFired && typeof window.gtag === 'function') {
       window.gtag('event', 'conversion', { send_to: 'AW-18121518600/WxyuCLjh56McEIjcgcFD' });
       conversionFired = true;
     }
     // ...debounced runCalculation as before
   });
   ```
3. Added a regression in `tests/content.test.js` asserting no HTML page fires `gtag('event', 'conversion', ...)` inside `<head>`. This blocks the bug from drifting back if the snippet is ever copy-pasted from the Google Ads UI again.

## Verification
- `node --test tests/*.test.js` passed `107/107` (was `106` — net `+1` from the new regression).
- `vercel deploy --prod --yes` produced `dpl_CtYWmDPsz8umVFnAnkgrZqpeABX4` and aliased to `https://profitafterfees.com` automatically.
- Live `curl -s https://profitafterfees.com/` confirms the `<head>` no longer contains the conversion event (only the gtag loader and `gtag('config', 'AW-18121518600')` remain).
- Live `curl -s https://profitafterfees.com/app/app.js | grep -c WxyuCLjh56McEIjcgcFD` returned `1` — the conversion send target now lives only inside the input listener.
- Primary URLs all `HTTP 200`: `/`, `/privacy/`, `/ads.txt`, `/sitemap.xml`, `/transaction-fee-calculator/`, `/ai-feature-cost-calculator/`.
- IndexNow POST for `https://profitafterfees.com/` returned `HTTP 200`.

## Why this matters
On the live $10/day campaign, every visit was previously reporting as a conversion. Smart Bidding (if enabled) was optimizing toward fake signals; cost-per-conversion and conversion-rate dashboards were meaningless. The fire now triggers exactly once per session, on the first calculator input change — the actual desired engagement on a no-form free-tool landing page. Any campaign currently in a learning phase against the broken signal should expect a reset.

## Adjacent question still open for Travis
The recommendation packet flagged two adjacent facts that would let the next move be sized correctly:
- Is the campaign currently using Smart Bidding (Maximize conversions / Target CPA / Maximize conversion value) or Manual CPC?
- Total spend so far against the `$50` stop-loss?

If Smart Bidding has already optimized against the broken signal for several days, that's a separate "reset learning" decision worth a single follow-up reply.

No spend made. Cash balance: $188.75.
