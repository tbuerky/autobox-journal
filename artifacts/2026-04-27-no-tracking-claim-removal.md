# 2026-04-27 — Remove the false "no tracking" claim from profitafterfees.com

## Why this run
The wake-up prompt directed me away from another internal doc or another SEO page and toward sharper conversion / quality-control work. While auditing the live site I found a customer-trust contradiction worth fixing immediately:

- The footer of every page printed `Profit After Fees · static page, no tracking, no signup · one calculator, one job`.
- The homepage hero list printed `No signup. No tracking.`.
- The same pages load Google Ads conversion tracking (`gtag.js` for `AW-18121518600`) and Google AdSense (`adsbygoogle.js` for `ca-pub-3560388500961643`).

A skeptical indie maker (the target reader) opening DevTools sees the contradiction in seconds. Leaving a false "no tracking" promise on the page burns the most expensive thing PAF has — first-visit credibility — at exactly the moment Travis is paying Google Ads to bring those visitors in.

## What changed (live now)

Routed through Luke (per RULES.md "public-facing copy") for the replacement strings and verified there are no other third-party scripts, no email forms, no newsletter widgets, and no account/contact forms before adopting his lines.

Files updated:
- `workspace/stripe-profit-calculator/index.html` — hero list `<li>` and footer `<p>`.
- `workspace/stripe-profit-calculator/ai-feature-cost-calculator/index.html` — footer `<p>`.
- `workspace/stripe-profit-calculator/ai-model-pricing-index/index.html` — footer `<p>`.
- `workspace/stripe-profit-calculator/llm-cost-calculator/index.html` — footer `<p>`.
- `workspace/stripe-profit-calculator/tests/content.test.js` — replaced the assertion of the old hero copy and added a regression test that asserts no HTML page anywhere on the site contains the phrase `no tracking`.

Final customer-facing copy:
- Hero list bullet (homepage): `No signup, no account, no email.`
- Footer line (4 affected pages): `Profit After Fees · free, no signup, ad-supported · one calculator, one job`
- The second footer line (`Independent calculator. Not affiliated with Stripe. Results are estimates, not tax or financial advice.`) was left untouched on the pages where it appears.

## Verification
- `node --test tests/*.test.js` — `121/121` passing locally.
- `vercel deploy --prod` produced deployment `stripe-profit-calculator-j4e7l5ssy-travis-4599s-projects.vercel.app`.
- `vercel alias set ... profitafterfees.com` returned `Success! https://profitafterfees.com now points to ...`.
- Live `curl` confirmed the new footer line on `/`, `/ai-feature-cost-calculator/`, `/ai-model-pricing-index/`, and `/llm-cost-calculator/`.
- Live `curl` confirmed the homepage hero now reads `<li>No signup, no account, no email.</li>` and no longer prints `No tracking`.
- A grep of the deployed site for `no tracking` returned zero hits.

## Truthfulness of the new claims (so this stays honest)
- `free` — the site has no paid tier and no checkout.
- `no signup` — there is no signup, login, or account flow.
- `no account, no email` — there is no email-collection form, no newsletter, no contact form on any page.
- `ad-supported` — only third-party scripts loaded sitewide are `gtag.js` (Google Ads) and `adsbygoogle.js` (Google AdSense). No other analytics, heatmap, session-replay, A/B, or fingerprinting scripts are loaded. If that ever changes, the "ad-supported" line will need to be updated again.

## Next step
Return to highest-leverage owner-side evidence:
- Profit After Fees: `ADS STATUS:` reply (Ads/AdSense state) and pause-at-`$50` enforcement.
- StrikeSight: `ROTATED: STRIKESIGHT KEYS READY`, options-data approval, or domain approval.
- AI Feature Margin Check: public-post URL and submitted scenarios from Travis.

If a small, accurate `/privacy` page becomes the next priority, that would be the natural follow-up — the kind of reader who notices a contradiction will look for one anyway.

## Budget
No spend. Current cash balance: `$188.75`.
