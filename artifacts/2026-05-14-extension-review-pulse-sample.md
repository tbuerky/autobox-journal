# Extension Review Pulse Sample Run

Date: 2026-05-14 18:39 UTC

## Decision

Created a fresh active-business validation artifact outside the gated Shopify Review Pulse lane: **Extension Review Pulse**, a one-off Chrome Web Store review and trust teardown for browser-extension developers.

This is not a full new broad research cycle. It is a narrow adjacent wedge chosen because the current Review Pulse lane is blocked by owner-side send/payment/intake gates and the latest state explicitly says not to create more Review Pulse collateral by default.

## Why This Lane

The parent category is already proven: browser-extension review monitoring and analytics.

Live evidence:

- ExtReviewBot sells browser-extension review tracking across Chrome Web Store, Firefox Add-ons, and Microsoft Edge Add-ons, with Slack alerts, AI summaries, sentiment analysis, CSV export, and a $7/month Pro plan.
- PeakReviews and Extension Radar also position around review analytics, sentiment, competitor, and pain-point extraction for app or extension developers.
- Chrome Web Store listing pages expose public rating, user count, developer contact details, manifest permissions, and public reviews.
- Current Chrome-extension developer discussions show visible pain around fake one-star reviews, security accusations, reply/report confusion, and low review volume.

Sources checked:

- `https://www.extreviewbot.com/`
- `https://www.peakreviews.io/`
- `https://www.extensionradar.com/`
- `https://chromewebstore.google.com/detail/tldr-for-youtube-%E2%80%93-chatgp/jgfhphpbcccicopbdffbppbdcccifhcm/reviews?hl=en-GB`
- `https://www.reddit.com/r/chrome_extensions/comments/1ond0r7/got_a_fake_1star_review_claiming_critical/`
- `https://www.reddit.com/r/chrome_extensions/comments/1tbpmsi/fake_review_has_this_ever_happened_to_you_too/`

## Built

- `workspace/extension-review-pulse/extension_review_pulse.mjs`
- `workspace/extension-review-pulse/README.md`
- `workspace/extension-review-pulse/sample-tldr-youtube-report.md`

The generator fetches a Chrome Web Store reviews URL, parses the public listing/review data available in the rendered HTML, and writes a short Markdown report focused on install drivers, trust/permissions risk, and copy/reply fixes.

Sample target:

- `TLDR for YouTube – ChatGPT Video Summarizer`
- Chrome Web Store rating parsed: `4.4/5` across `7` ratings.
- Public reviews captured: `3`.
- Public contact parsed: `nobotak.com@gmail.com`.
- Parsed trust surface includes `activeTab`, `storage`, `tabs`, YouTube host permissions, ChatGPT host permissions, and Google video host permissions.

## Offer

First price test: `$49` one-off.

Deliverable:

- revised Chrome listing copy
- permissions-in-plain-English block
- screenshot-caption rewrites
- public reply drafts for bad or suspicious reviews
- one review-request prompt that avoids fake-review or review-exchange language

## Why It Might Sell

Monthly analytics tools make sense for mature extension teams, but many Chrome-extension developers have tiny teams, visible developer emails, and just enough rating/review pain to pay for a one-off trust repair pack before committing to recurring software.

The sample report is intentionally sharper than a generic landing-page roast. The buyer-specific hook is permission trust: Chrome extension users often inspect permissions and reviews before installing, and bad security/privacy language can suppress installs even when the review is unfair.

## Approval Needed

`APPROVED: CONTACT ONE CHROME EXTENSION DEVELOPER WITH EXTENSION REVIEW PULSE SAMPLE`

## If Approved

Send one concise message to the parsed public developer email for the sample target or a better current Chrome Web Store target. The message should link or attach `workspace/extension-review-pulse/sample-tldr-youtube-report.md`, ask whether a `$49` one-off trust/review teardown is useful, and wait for a reply. Do not batch-send.

## Guardrails

- No outreach was sent.
- No public page was changed.
- No checkout/payment infrastructure was created.
- No account was created.
- No DNS changed.
- No public post was published.
- No spend occurred.
