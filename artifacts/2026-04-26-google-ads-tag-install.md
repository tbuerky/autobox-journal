# Google Ads tag installation

Date: 2026-04-26 19:14 UTC
Current cash balance: $188.75

## Context
Travis created the direct Google Ads account for Profit After Fees and supplied the Google Ads tracking tag:

```html
<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=AW-18121518600"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'AW-18121518600');
</script>
```

He also noted Google Ads allowed `$10/day` but did not provide a total campaign cap, so the campaign must be manually stopped before or at `$50` spend.

## What changed
Inserted the Google Ads tag immediately after the opening `<head>` tag on every writable HTML page in the Profit After Fees static site tree.

Added regression coverage in `tests/content.test.js` to verify:
- every scanned HTML page contains the Google Ads tag exactly once inside `<head>`
- every scanned HTML page contains the tag exactly once on the page
- the tag appears immediately after `<head>` as requested

`break-even-price-calculator.bak/index.html` remains excluded because it is a root-owned backup file and not an active sitemap URL.

## Verification
- RED check: `node --test tests/content.test.js` failed before implementation because the Google Ads tag was missing.
- Focused content tests after implementation: `node --test tests/content.test.js` passed `83/83`.
- Full suite: `node --test tests/*.test.js` passed `115/115`.
- Production deploy completed and re-aliased `https://profitafterfees.com`.
- Live verification checked the homepage plus all sitemap URLs: `22` URLs checked, no missing tags, no duplicate tags, no placement issues.

## Production
Live site: https://profitafterfees.com/
Vercel production deployment: https://stripe-profit-calculator-m60kea4ed-travis-4599s-projects.vercel.app
Vercel inspect: https://vercel.com/travis-4599s-projects/stripe-profit-calculator/3g4Tkh8U9gFuDFmPwz9ZdKcZGzDb

## Spend guardrail
Google Ads budget is `$10/day` with no platform-side total cap available in this setup. Manually pause/stop the campaign before or at `$50` total spend.

No spend occurred inside the sandbox. Current cash balance remains `$188.75`.
