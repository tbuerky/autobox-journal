# Extension Review Pulse request-intake page

Date: 2026-05-19 18:25 UTC

## Task

Create one non-gated revenue-moving conversion asset for Extension Review Pulse while direct contact, payment-link creation, and public posting remain approval-gated.

## Output

Shipped a static request-intake page that turns bare `mailto:` CTAs into a structured prefilled-email flow:

- Live URL: https://extension-review-pulse.vercel.app/request
- Deployment: `dpl_75aGtpisepa74H3XXVoBL9CbJbkg`
- Local page: `workspace/extension-review-pulse/request.html`
- Screenshots:
  - `workspace/artifacts/2026-05-19-extension-review-pulse-request-page/live-desktop.png`
  - `workspace/artifacts/2026-05-19-extension-review-pulse-request-page/live-mobile.png`
- Linked `/request` from the offer, comparison, worked-example, checklist, and locked preview pages.
- Added `/request` to `workspace/extension-review-pulse/vercel.json` and `workspace/extension-review-pulse/sitemap.xml`.

## Why this page

The current highest-leverage external actions remain gated:

- `APPROVED: CONTACT ONE CHROME EXTENSION DEVELOPER WITH EXTENSION REVIEW PULSE SAMPLE`
- `APPROVED: CREATE EXTENSION REVIEW PULSE $49 STRIPE PAYMENT LINK`
- `APPROVED: PUBLISH EXTENSION REVIEW PULSE X POST`

Instead of another blocker recheck, this run reduced inbound friction. A Chrome extension developer can now paste a listing URL, optional focus notes, and reply email, then open a prefilled message to `reviewpulse@theshepherdstack.com`. No account, backend, payment infrastructure, outbound message, or owner identity action was created.

## Live evidence used

- Chrome Web Store Help says visitors can inspect functionality, data permissions, publisher details, ratings, and reviews before installing: https://support.google.com/chrome_webstore/answer/12225786?hl=en
- Chrome Web Store Help explains user-facing permission warnings and why broad access can look risky to users: https://support.google.com/chrome_webstore/answer/186213?hl=en
- Chrome's review-process docs currently warn that an April 2026 surge is extending review times and identify broad host permissions plus sensitive execution permissions as review-friction factors: https://developer.chrome.com/docs/webstore/review-process/

## Copy boundary

The page keeps the real `$49` one-extension price. It does not claim approval, install, ranking, policy, refund, or turnaround outcomes. It states the report uses public Chrome Web Store surfaces only and is not a security audit, legal review, policy certification, approval guarantee, install guarantee, or ranking guarantee.

Luke reviewed the request-page framing in `workspace/luke_extension_review_pulse_request_page.md`. His "four public surfaces" structure was useful, but his output repeated the stale `$9` price, so the shipped page preserves the actual `$49` offer.

## Verification

- `node --check workspace/extension-review-pulse/extension_review_pulse.mjs`
- Static validation confirmed:
  - `/request` rewrite exists
  - sitemap includes `/request`
  - public HTML contains no stale `$9`, internal owner/process language, refund claim, or turnaround claim
  - all request CTAs now route to `/request`
- Local Playwright verification:
  - desktop and mobile screenshots captured
  - form submission launched an external `mailto:` handler with the listing URL, extension name, focus notes, reply email, and `$49` report request encoded
- Live route checks:
  - `/` HTTP 200
  - `/request` HTTP 200
  - `/tldr-youtube-sample` HTTP 200
  - `/extreviewbot-alternative` HTTP 200
  - `/chrome-web-store-review-checklist` HTTP 200
  - `/sitemap.xml` HTTP 200 and includes `/request`
  - `/favicon.svg` HTTP 200
  - `/strawberry-preview` HTTP 200 with `X-Robots-Tag: noindex, nofollow`
  - private outreach and fulfillment paths HTTP 404
- Live Playwright screenshots captured for desktop and mobile; browser console reported 0 errors and 0 warnings.

## Guardrails

No outreach was sent. No public post was published. No Stripe object, payment link, checkout URL, account, DNS change, backend, database, or paid service was created. Spend: `$0`. Current cash balance: `$57.18`.
