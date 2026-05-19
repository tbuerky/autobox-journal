# Extension Review Pulse comparison page

Date: 2026-05-19 14:23 UTC

## Task

Create one non-gated revenue-moving asset for the Extension Review Pulse lane while direct contact, payment links, and public posting remain approval-gated.

## Output

Shipped an indexable comparison page:

- Live URL: https://extension-review-pulse.vercel.app/extreviewbot-alternative
- Deployment: `dpl_GP7rkfmx9ff59bEo8US8TAg6hJJX`
- Local page: `workspace/extension-review-pulse/extreviewbot-alternative.html`
- Updated internal links from `workspace/extension-review-pulse/index.html`
- Added the route to `workspace/extension-review-pulse/vercel.json`
- Added the URL to `workspace/extension-review-pulse/sitemap.xml`
- Updated `workspace/extension-review-pulse/README.md`
- Screenshots:
  - `workspace/artifacts/2026-05-19-extension-review-pulse-comparison-page/live-desktop.png`
  - `workspace/artifacts/2026-05-19-extension-review-pulse-comparison-page/live-mobile.png`

## Why this page

The existing external actions are blocked on owner-controlled approvals:

- `APPROVED: CONTACT ONE CHROME EXTENSION DEVELOPER WITH EXTENSION REVIEW PULSE SAMPLE`
- `APPROVED: CREATE EXTENSION REVIEW PULSE $49 STRIPE PAYMENT LINK`
- `APPROVED: PUBLISH EXTENSION REVIEW PULSE X POST`

Instead of adding another approval packet, this run captured search-intent demand around existing extension-review tools. The page positions Extension Review Pulse as a one-off trust/copy pass for developers who do not yet need ongoing review monitoring.

## Live evidence used

- ExtReviewBot sells browser-extension review tracking across Chrome Web Store, Firefox Add-ons, and Microsoft Edge Add-ons, with Slack notifications, ratings analytics, AI summaries, translation, sentiment analysis, CSV export, and multi-extension tiers: https://www.extreviewbot.com/
- Chrome Review Bot positions itself around Chrome reviews delivered to Slack and negative-feedback notifications: https://chromereviewbot.com/
- Chrome Web Store review and policy surfaces make reviews, permissions, publisher details, privacy, and listing trust commercially relevant to extension developers: https://developer.chrome.com/docs/webstore/review-process
- Extension Radar publishes current Chrome extension competitor-analysis content, reinforcing that extension developers actively inspect review and competitor signals: https://www.extensionradar.com/blog/chrome-extension-competitor-analysis

## Copy boundary

The page does not claim to improve ratings, review counts, rankings, installs, approval outcomes, security posture, or policy compliance. It explicitly states that Extension Review Pulse is not affiliated with ExtReviewBot, Chrome Review Bot, Extension Radar, Google, or the Chrome Web Store.

Luke reviewed the planned comparison angle in `workspace/luke_extension_review_pulse_comparison.md`. His structural advice was useful, but his output repeated the stale `$9` price mistake, so the final page preserved the actual `$49` offer and avoided competitor-pricing claims.

## Verification

- `node --check workspace/extension-review-pulse/extension_review_pulse.mjs`
- Static validation of HTML boundaries, sitemap inclusion, and valid `vercel.json`
- Live route checks:
  - `/` HTTP 200
  - `/extreviewbot-alternative` HTTP 200
  - `/tldr-youtube-sample` HTTP 200
  - `/sitemap.xml` HTTP 200 and includes `/extreviewbot-alternative`
  - `/favicon.svg` HTTP 200
  - `/strawberry-preview` HTTP 200 with `X-Robots-Tag: noindex, nofollow`
  - private outreach and fulfillment paths HTTP 404
- Playwright live render:
  - desktop full-page screenshot captured
  - mobile full-page screenshot captured
  - browser console reported 0 errors and 0 warnings

## Guardrails

No outreach was sent. No public post was published. No Stripe object, payment link, checkout URL, account, DNS change, or paid service was created. Spend: `$0`. Current cash balance: `$57.18`.
