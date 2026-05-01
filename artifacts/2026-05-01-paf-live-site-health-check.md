# PAF live-site health check — 2026-05-01

## Why

PAF is the live earning property. The last time it was eyeballed was the 2026-04-29 conversion-event engagement-paths followup ship (commit `dpl_HZBQwWWtW1MMuA9pyoKdd2hrcGEm`). Since then no run has verified the production surface still renders correctly. With AdSense Auto Ads serving on the apex and a Google Ads Search campaign expiring 2026-05-04, silent regression on any of the recently-shipped fixes (conversion event in `<head>`, `/privacy/` disclosure, `/ads.txt`, content-pruning redirects, SEO subhead leak fix) would silently rot revenue. Every StrikeRewind owner gate is dark, so the highest-leverage no-approval move was operator hygiene on the actually-earning property.

## Method

Direct curl-driven verification against `https://profitafterfees.com` — six checks, 30 total assertions:

1. Endpoint availability — apex / privacy / ads.txt / sitemap.xml
2. ads.txt content — canonical line for AdSense authorization
3. Homepage `<head>` regression — conversion event must NOT fire on every page load (the 2026-04-28 23:15 UTC fix)
4. Engagement-path conversion fire — `app.js` must contain the `fireConversionOnce()` helper + three call sites + three `conversionFired` guard references (the 2026-04-29 00:30 UTC followup)
5. Privacy disclosure — `/privacy/` mentions Google AdSense + Google Ads, footer links to `/privacy/` from homepage
6. Comparison/calculator pages — 12 pages return 200; 2 redirect pairs return 308 → canonical; 7 deleted process docs / .bak still return 404

## Result

**All 30 checks pass. No regressions detected.**

### Endpoint availability

| URL | Status | Bytes | TTFB |
|---|---|---|---|
| `/` | 200 | 15877 | 0.115s |
| `/privacy/` | 200 | 9562 | 0.209s |
| `/ads.txt` | 200 | 59 | 0.146s |
| `/sitemap.xml` | 200 | 1769 | 0.121s |

### ads.txt content

```
google.com, pub-3560388500961643, DIRECT, f08c47fec0942fa0
```

Matches the line shipped 2026-04-27 22:25 UTC and the AdSense publisher ID embedded in the homepage `<script>` tag (`ca-pub-3560388500961643`). AdSense demand-side platforms remain authorized.

### Conversion event regression — homepage `<head>`

`grep -c "gtag('event', 'conversion'" /tmp/paf_home.html` → **0** occurrences in homepage HTML. The 2026-04-28 fix (delete unconditional event from `<head>`) is intact. The page-load-fires-conversion bug has not regressed.

### Conversion fire — `app/app.js` (engagement paths)

`https://profitafterfees.com/app/app.js` (6704 bytes):

- `AW-18121518600` (the conversion send_to target): **1** occurrence — exactly one fire path, no duplicates
- `fireConversionOnce`: **4** occurrences — 1 helper definition + 3 call sites (input listener, preset click, form submit) per the 2026-04-29 followup ship
- `conversionFired`: **3** occurrences — `let conversionFired = false` declaration + early-return guard + post-fire assignment

Every visible engagement path on the calculator records exactly one conversion per visit.

### Privacy disclosure

`/privacy/` page contains:
- "Google AdSense": 1 occurrence
- "Google Ads": 4 occurrences
- "Privacy": 8 occurrences

Homepage footer contains 1 link to `/privacy/`. AdSense Program Policies' clear-and-easily-accessible privacy requirement remains satisfied.

### Comparison / calculator pages — 200

`gumroad-vs-stripe`, `paddle-vs-stripe`, `paypal-vs-stripe-fees`, `stripe-fees-for-online-courses`, `stripe-fees-for-notion-templates`, `stripe-fees-for-micro-saas`, `how-to-calculate-profit-margin-on-digital-products`, `ai-feature-cost-calculator`, `ai-model-pricing-index`, `transaction-fee-calculator`, `saas-pricing-calculator`, `online-course-pricing-calculator` — all 12 return HTTP 200.

### Pruning passes still hold

| Loser slug | Code | Final URL |
|---|---|---|
| `/stripe-processing-fee-calculator/` | 308 | `/transaction-fee-calculator/` |
| `/llm-cost-calculator/` | 308 | `/ai-feature-cost-calculator/` |

| Deleted doc | Code |
|---|---|
| `/launch/forum-post` | 404 |
| `/launch/seo-strategy` | 404 |
| `/launch/launch-week` | 404 |
| `/launch/distribution` | 404 |
| `/launch/` | 404 |
| `/home/` | 404 |
| `/break-even-price-calculator.bak/` | 404 |

### SEO subhead leak — `/lemonsqueezy-vs-stripe/`

`grep -c "without the space"` → **0** occurrences. The 2026-04-29 SEO-process-language replacement is intact.

## What this rules out

- AdSense ad-serving silently failing because pub ID rotated
- AdSense disclosure quietly dropped from a footer
- Conversion event regressing back into homepage `<head>` and torching the Google Ads Search campaign's signal quality
- Engagement-path conversion fire silently breaking (e.g. someone refactored `fireConversionOnce` and removed a call site)
- A pruned page accidentally re-deployed via cache or sitemap drift
- The lemonsqueezy SEO-subhead leak drifting back via a stale build

None of these failure modes is firing.

## What this does NOT rule out

- Visual regression (text now overlaps a button, an image now 404s, mobile layout broke at a specific width) — would need browser-rendered screenshots; out of scope for a curl-driven check
- AdSense impressions / eCPM trending down — needs Travis-side dashboard access
- Google Ads campaign verification clearance status — needs Travis-side dashboard access
- Search Console crawl errors — needs Travis-side GSC access
- Live calculator math correctness — would need DOM evaluation in a real browser
- New regressions specific to AI Feature Cost Calculator's downstream provider-pricing data — would need provider-side spot-check

## Next step

No remediation required. The PAF revenue path is intact end-to-end on the live surface. Continuing to wait on Travis for the three open StrikeRewind gates (`APPROVED: DEPLOY ON VERCEL+RENDER STARTER, $7/MO`; `APPROVED: STRIKEREWIND TIER COPY + LIMITS PRE-DEPLOY`; `MIGRATION APPLIED: SPREAD_RESULTS WAREHOUSE`).
