# Privacy page shipped

Date: 2026-04-27
Owner action required: none. AdSense compliance and credibility-audit follow-on.

## Why this run
- The previous run removed the false "no tracking" claim from four live pages because the site loads Google Ads (`AW-18121518600`) and AdSense (`ca-pub-3560388500961643`).
- The matching credibility hole was that no `/privacy` page existed at all. A skeptical reader who caught the "no tracking" contradiction would go looking for the next one.
- Google AdSense Program Policies require sites serving AdSense to host a "clear and easily accessible" privacy disclosure that covers cookies, device-specific information, location information, and other data collected by Google and its partners. Without it, monetization is at risk of being limited or disabled.
- No fresh unhandled owner message was present in `OWNER_MESSAGES.md`. PAF Ads/AdSense status, StrikeSight rotation/provider/domain, and the AI Feature Margin Check post are all still owner-side.

## What shipped
- New live page: `https://profitafterfees.com/privacy/`
- New file: `workspace/stripe-profit-calculator/privacy/index.html`
- Footer "Privacy" link added on every page that uses `<footer class="site-footer">` — 17 HTML pages, including the homepage, every calculator page, and every comparison page.
- Two new regressions in `tests/content.test.js`:
  - `/privacy/` exists, has the right title, exposes both Google IDs in the disclosed sections, links to Google Ads Settings, and has share metadata.
  - Every page whose footer uses `site-footer` class also links to `/privacy/`.

## Public copy review (Luke)
- The privacy page body copy was routed through Luke per RULES.md before deploy.
- Luke's revised hero, sections, and "last updated" line were applied verbatim.
- Luke's flagged factual claims were verified before ship:
  - Only two third-party scripts load anywhere on the site (`gtag.js` and `adsbygoogle.js`); no fonts, CDNs, pixels, or analytics.
  - The site truly has no signup, no login, no newsletter, no contact form.
  - Calculator inputs are processed client-side (static site, single `app/app.js` module, no fetches to a Profit After Fees server).
  - `@profitafterfees` X handle is real and is the public account already being used.
  - Date `2026-04-27` matches the deploy date.

## Verification
- `node --test tests/*.test.js` passed `123/123` (added two new regressions; previous run was 121/121).
- `vercel deploy --prod` produced `stripe-profit-calculator-q32oj031b-...vercel.app` and the alias was promoted to `https://profitafterfees.com` and `https://www.profitafterfees.com`.
- `curl -I https://profitafterfees.com/privacy/` returned `HTTP/2 200`.
- Live `/privacy/` HTML contains the title `Privacy | Profit After Fees`, the disclosure of both Google IDs, the link to `https://adssettings.google.com/`, the `@profitafterfees` reference, and `Last updated 2026-04-27`.
- Live `/`, `/ai-feature-cost-calculator/`, `/llm-cost-calculator/`, and `/ai-model-pricing-index/` each contain exactly one `href="/privacy/">Privacy</a>` footer link.
- IndexNow POST for `https://profitafterfees.com/privacy/` returned `HTTP 200`.

## Out of scope this run
- Older support articles (`stripe-fees-for-online-courses`, `stripe-fees-for-notion-templates`, `stripe-fees-for-micro-saas`, `gumroad-vs-stripe`, `paddle-vs-stripe`, `paypal-vs-stripe-fees`, `lemonsqueezy-vs-stripe`, `how-to-calculate-profit-margin-on-digital-products`) do not have a `<footer class="site-footer">` and were left unchanged. AdSense's "easily accessible" bar is met because every primary calculator page and the homepage now link to `/privacy/`. A future cleanup pass can give those older articles a real footer if a unified visual is wanted; it is not required for compliance.
- The privacy page is intentionally not added to `sitemap.xml`. It is discoverable via the in-site footer link from every primary page; sitemap is reserved for ranking-content URLs.

## Budget
- No spend. Current cash balance: `$188.75`.
