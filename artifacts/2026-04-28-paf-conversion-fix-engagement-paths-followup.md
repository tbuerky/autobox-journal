# PAF conversion fix follow-up — fire on every form-of-engagement Smart Bidding should optimize for

## Context
Earlier today's run shipped the owner-approved conversion-tracking fix (`APPROVED PAF FIX CONVERSION`): moved the `gtag('event', 'conversion', ...)` call out of the unconditional `<head>` block and into the existing `form.addEventListener('input', ...)` handler in `app/app.js`, gated by a single `conversionFired` boolean.

A post-deploy audit of `app/app.js` showed the fix only fired on raw `input` events on `<input>` elements — every other path that visibly engages the calculator was silently missing the conversion fire:

- Clicking a preset chip ("Cohort course", "Annual SaaS plan", etc.) calls `applyValuesToForm(...)` which sets `field.value = String(...)` programmatically. Programmatic value assignments do NOT dispatch `input` events. So picking a preset → fully rendered calculator result → no conversion recorded.
- Submitting the form (clicking the `Recalculate` button) re-runs the calculation but never touched the conversion fire.
- (Not changed this run) Copying the share link is downstream of the above paths, so the conversion has already fired by the time someone copies a share URL.

Effect on Smart Bidding: any visitor whose first action is a preset click — the lowest-friction, highest-intent calculator engagement on the page — failed to count as a conversion. The "engagement" signal we just fixed was still under-counting the cleanest engagements.

## What changed
- `workspace/stripe-profit-calculator/app/app.js`:
  - Extracted a single `fireConversionOnce()` helper at module scope. It exits early if `conversionFired` is true or `window.gtag` is not a function; otherwise it sends `gtag('event', 'conversion', { send_to: 'AW-18121518600/WxyuCLjh56McEIjcgcFD' })` and flips `conversionFired = true`.
  - Calls `fireConversionOnce()` from three places: the existing input handler (preserved), the preset button click handler (new), and the form submit handler (new).
  - The conversion `send_to` target now appears exactly once in `app.js` — inside the helper. No other code path can fire the wrong event by accident.
- `workspace/stripe-profit-calculator/tests/content.test.js`:
  - New regression `app.js fires the Google Ads conversion event on every form-of-engagement Smart Bidding should optimize for` asserts:
    1. `app.js` defines a single `fireConversionOnce` function.
    2. The conversion send_to target appears exactly once in `app.js` (inside the helper, not duplicated at call sites).
    3. The preset button click handler calls `fireConversionOnce()`.
    4. The form submit handler calls `fireConversionOnce()`.
    5. The form input handler calls `fireConversionOnce()`.
  - Existing "no conversion event in `<head>`" regression still passes.

## Verification
- `node --test tests/*.test.js` passed `109/109` (was `108` — net `+1` from the new regression).
- `vercel deploy --prod --yes` produced `dpl_HZBQwWWtW1MMuA9pyoKdd2hrcGEm`; aliased to `https://profitafterfees.com` and `https://www.profitafterfees.com` under team `travis-4599s-projects`.
- `curl https://profitafterfees.com/app/app.js | grep -c fireConversionOnce` → `4` (1 definition + 3 call sites).
- `curl https://profitafterfees.com/app/app.js | grep -c WxyuCLjh56McEIjcgcFD` → `1` (only inside the helper).
- `curl https://profitafterfees.com/ | grep -c WxyuCLjh56McEIjcgcFD` → `0` (homepage `<head>` stays clean).
- Primary URLs all `HTTP 200`: `/`, `/privacy/`, `/ads.txt`, `/sitemap.xml`, `/transaction-fee-calculator/`, `/ai-feature-cost-calculator/`, `/saas-pricing-calculator/`.

## Approval status
This is a follow-up to the existing `APPROVED PAF FIX CONVERSION` — same intent (move the fire from page load to first calculator engagement), just covering all three engagement paths the visitor sees instead of one. Not a new approval gate.

## Next-actor question for Travis (still open from prior runs)
- Bidding strategy (Smart Bidding vs Manual CPC) and total spend so far against the `$50` stop-loss. With the fire now correctly attached to every visible engagement path, any campaign that was in a learning phase against the broken signal can be assessed for whether a learning reset is needed.
- AdSense approval status / Auto Ads enablement / impressions / eCPM.

## Cash balance
`$188.75`. No spend.
