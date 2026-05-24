# Extension Review Pulse Freedom locked preview

Date: 2026-05-24 20:22 UTC

## Task

Create one conversion asset for the prepared Freedom Extension Review Pulse prospect without sending outreach before the Compose AI wait clears.

## Result

- Live noindex preview: https://extension-review-pulse.vercel.app/freedom-preview
- Source: `workspace/extension-review-pulse/freedom-preview.html`
- Deployment: `dpl_Fi2qTySgcoaQUTpm21o6mDNdRrAb`
- Screenshots:
  - `workspace/extension-review-pulse/output/playwright/freedom-preview/local-desktop.png`
  - `workspace/extension-review-pulse/output/playwright/freedom-preview/live-desktop.png`

## Evidence

Live checks on 2026-05-24 showed Freedom's Chrome Web Store listing at `60,000 users`, `3.3/5` across `99` ratings, version `19.0.0`, updated `September 18, 2024`, public contact `support@freedom.to`, trial/free and premium/paid language, and authentication-information disclosure. Freedom's Help Center says the extension can act as a standalone blocker on ChromeOS/Linux after sign-in and sync, while Mac/Windows require the desktop app and use the extension for the green-screen blocked-site flow.

Sources:

- https://chromewebstore.google.com/detail/freedom-website-blocker-f/abdkjmofmjelgafcdffaimhgdgpagmop
- https://support.freedom.to/en/articles/1347519-freedom-browser-extension

## Copy boundaries

The preview is a locked teaser for use only after a positive reply. It does not include the Stripe link, does not go into the first-touch email, and does not claim a code audit, security audit, privacy audit, legal review, vulnerability finding, unsafe verdict, policy certification, affiliation, or guaranteed install lift.

Luke reviewed the public-copy direction, but his returned recommendation included stale `$9` pricing plus unsupported delivery/refund claims. Final copy used only the useful Freedom-specific framing and preserved the live `$49` offer.

## Verification

- `node --check workspace/extension-review-pulse/extension_review_pulse.mjs` passed.
- `python3 -m json.tool workspace/extension-review-pulse/vercel.json` passed.
- Local and live Playwright Firefox screenshots were captured.
- Live `/freedom-preview` returned HTTP `200` with `X-Robots-Tag: noindex, nofollow`.
- Live `/`, `/request`, and `/sitemap.xml` returned HTTP `200`.
- Live private `/outreach/freedom-first-email.eml` and `/prospect-reports/freedom.md` returned HTTP `404`.
- No IndexNow submission was made because the preview is noindex and intentionally absent from the sitemap.

## Gates and spend

`config/OPEN_GATES.md` remains unchanged:

- `APPLY: WRITE MY FORMULA GOOGLE ADS BROADENING IMPORT`
- `RESOLVE: WRITEMYFORMULA.COM VERCEL DOMAIN ACCESS`

No outreach/email/contact form, IndexNow submission, checkout/payment change, ad/bid/budget change, DNS/account/legal/bank/destructive production change, public post, bulk send, or spend occurred. Current cash balance remains `$35.93`.
