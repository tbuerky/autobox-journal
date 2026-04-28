# Profit After Fees: Google Ads conversion event fires on every page load — fix recommendation

Date: 2026-04-28 10:30 UTC
Current cash balance: $188.75

## What I found

The live homepage at `https://profitafterfees.com/` fires a Google Ads conversion event unconditionally inside the `<head>`, on every page load:

```html
<script>
  gtag('event', 'conversion', {'send_to': 'AW-18121518600/WxyuCLjh56McEIjcgcFD'});
</script>
```

Source: `workspace/stripe-profit-calculator/index.html` lines 13–15. Verified live by `curl -s https://profitafterfees.com/`. The conversion ID matches your Google Ads account `AW-18121518600`.

This snippet is not in any AutoBox artifact. The original tag-install run only added `gtag('config', ...)`. The conversion event was added later, manually — most likely copy-pasted directly from the Google Ads "conversion action" setup screen, which generates that exact text.

## Why this matters now

Google's UI literally labels that snippet as the "event snippet" and instructs the user to fire it on the action they want to count. Putting it in `<head>` makes it fire on every visit. Effects on a paid-traffic site:

1. **100% conversion rate is reported.** Every Google Ads click registers as a conversion in the Ads UI.
2. **Smart Bidding is poisoned.** If the campaign uses any auto-bid strategy ("Maximize conversions", "Target CPA", "Maximize conversion value"), Google is optimizing toward "every click = a conversion", which steers spend toward whichever ads/keywords/audiences get the most clicks regardless of quality.
3. **Cost-per-conversion math is meaningless.** The $50 stop-loss can be hit while the dashboard shows wins; you cannot tell which keywords actually performed.
4. **No real engagement signal is tracked.** The thing a free calculator landing page would actually want to count — the visitor *using* the calculator — is not being measured anywhere.

## Primary recommendation

Move the conversion event off page load and fire it exactly once when the visitor performs a real engagement: the first time any calculator input changes.

The existing app code already has the right hook. `workspace/stripe-profit-calculator/app/app.js` line 170 already attaches an `input` listener to `#calculator-form`. The fix is to add a single one-shot conversion call inside that listener:

```js
let _gadsConversionFired = false;
form.addEventListener('input', (event) => {
  // ...existing handling...
  if (!_gadsConversionFired && typeof window.gtag === 'function') {
    window.gtag('event', 'conversion', { send_to: 'AW-18121518600/WxyuCLjh56McEIjcgcFD' });
    _gadsConversionFired = true;
  }
});
```

And the unconditional `<script>` block in the homepage `<head>` is removed.

This counts the actual desired action on a free-tool landing page — the visitor engaging with the calculator — once per session, instead of once per page load. It is the standard recommended placement for a Google Ads conversion action on a no-form landing page.

**Approval line:** `APPROVED: PAF FIX CONVERSION TO CALCULATOR ENGAGEMENT`

On that reply, in the next AutoBox run I will:
1. Delete lines 13–15 of `workspace/stripe-profit-calculator/index.html`.
2. Add the one-shot conversion fire inside the existing `input` listener in `app/app.js`.
3. Add a regression test that asserts no HTML page contains `gtag('event', 'conversion'` inside `<head>`.
4. Run the full `node --test tests/*.test.js` suite (currently `106/106`).
5. `vercel deploy --prod`, verify live HTML, and submit IndexNow for the homepage.
6. Note in BUDGET.md that no spend occurred for this fix.

## Alternatives considered (context only — not parallel approval lines)

- **Remove the conversion event entirely** and rely on GA4 engagement metrics. Cleaner, but you lose the ability to feed Google Ads any conversion signal and it would force a campaign-side switch off Smart Bidding.
- **Fire on the `Recalculate` button submit only.** Narrower coverage; misses the more common path where defaults are adjusted live and the user never clicks the button. The existing `input` listener is a strictly larger, more accurate signal.
- **Leave as-is.** Continues to corrupt Smart Bidding and conversion reporting on a campaign already burning $10/day. Not recommended.

## Adjacent question worth a separate reply (no approval needed today)

Whichever direction you take on the conversion fix, two facts about the campaign would let me size the next move:

- Is the campaign currently using Smart Bidding (Maximize conversions, Target CPA, etc.) or Manual CPC?
- Total spend so far against the $50 stop-loss?

If Smart Bidding has already been running on the broken signal for several days, that is a separate "reset learning" decision worth surfacing once we know the spend number.

## Verification done in this run

- `curl -s https://profitafterfees.com/` returned HTTP 200 and contains the unconditional conversion event in `<head>`.
- `grep` for `gtag('event', 'conversion'` and `WxyuCLjh56McEIjcgcFD` shows the only occurrence is `workspace/stripe-profit-calculator/index.html` (no other page is affected).
- `app/app.js` already exposes a `form.addEventListener('input', ...)` handler at line 170, so the fix has a clean attachment point.
- Site sitemap and primary URLs (`/`, `/privacy/`, `/ads.txt`, `/sitemap.xml`) still return HTTP 200.

## Owner-side gate

**Approval needed:** `APPROVED: PAF FIX CONVERSION TO CALCULATOR ENGAGEMENT`

No spend. Cash balance: $188.75.

## Suggested post copy:

PAF Google Ads is firing a conversion on every page load (currently in homepage `<head>`). Smart Bidding is being optimized toward fake signals while the $10/day campaign runs.

Reply `APPROVED: PAF FIX CONVERSION TO CALCULATOR ENGAGEMENT` and I will move the event to the first calculator input change, ship a regression, and deploy live next run.

If easy: also share whether the campaign is on Smart Bidding (Maximize conversions / Target CPA) or Manual CPC, and total spend so far.

Detail: artifacts/2026-04-28-google-ads-conversion-bug-fix-recommendation.md
