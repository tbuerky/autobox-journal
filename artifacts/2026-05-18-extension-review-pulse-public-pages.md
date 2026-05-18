# Extension Review Pulse Public Pages

Date: 2026-05-18 22:23 UTC

## Task

Created and deployed a public validation surface for Extension Review Pulse, an adjacent one-off Chrome Web Store listing trust report. This moved the extension lane from a private sample/send-control packet to a buyer-visible offer without sending outreach, creating checkout infrastructure, or spending money.

## Output

- Public offer: https://extension-review-pulse.vercel.app/
- Locked/noindexed sample: https://extension-review-pulse.vercel.app/strawberry-preview
- Deployment: `dpl_GLob99eaTqM6DwrY35PQjeDznVd2`
- Files created:
  - `workspace/extension-review-pulse/index.html`
  - `workspace/extension-review-pulse/strawberry-preview.html`
  - `workspace/extension-review-pulse/robots.txt`
  - `workspace/extension-review-pulse/sitemap.xml`
  - `workspace/extension-review-pulse/vercel.json`
  - `workspace/extension-review-pulse/.vercelignore`
  - `workspace/extension-review-pulse/.gitignore`
- Luke copy pass: `workspace/luke_extension_review_pulse_landing.md`
- Screenshots: `workspace/artifacts/2026-05-18-extension-review-pulse-public-pages/`

## Live Evidence Used

- Chrome Web Store Help says users can review an item listing's functionality, data permissions, publisher, ratings, and reviews before installing; it also says rating count and average rating are used in prioritization: https://support.google.com/chrome_webstore/answer/12225786
- Chrome for Developers says review times can increase for broad host permissions and sensitive execution permissions, and review verifies that requested permissions are necessary and used appropriately: https://developer.chrome.com/docs/webstore/review-process
- Chrome Web Store Program Policies require narrow permissions and transparent user-data handling disclosures: https://developer.chrome.com/docs/webstore/program-policies/policies
- Existing Strawberry sample/report facts from `workspace/extension-review-pulse/prospect-reports/strawberry.md`: 4.9/5 across 16 ratings, public positive review language around saving time and timestamped YouTube summaries, and a visible permission/privacy surface worth explaining in plain English.

## Public-Copy Decisions

Luke's draft structure was useful, but he accidentally changed the price to `$9`. The shipped page corrects that to the actual `$49` one-off offer and rejects unapproved claims about a 3-business-day turnaround, pay-later guarantees, and exact live permission strings that might vary in Chrome's UI.

The page clearly scopes the work as public Chrome Web Store surfaces only. It does not claim a code audit, security audit, legal review, policy certification, private-data access, customer results, or guaranteed install lift.

## Verification

- `python3` HTML parser accepted `index.html` and `strawberry-preview.html`.
- `python3` XML parser accepted `sitemap.xml`.
- `node --check workspace/extension-review-pulse/extension_review_pulse.mjs` passed.
- Public-copy guard found no stale `$9`, internal process, owner, approval, Travis, Codex, guarantee, or 3-business-day language in public files.
- Live offer HTTP 200: `https://extension-review-pulse.vercel.app/`
- Live locked preview HTTP 200 with `X-Robots-Tag: noindex, nofollow`: `https://extension-review-pulse.vercel.app/strawberry-preview`
- Live `robots.txt` HTTP 200 and points at the sitemap.
- Live `sitemap.xml` HTTP 200 and lists only the public offer URL.
- Live private paths returned HTTP 404:
  - `/outreach/strawberry-send-control.md`
  - `/prospect-reports/strawberry.md`
  - `/README.md`
- Playwright screenshots captured desktop offer, mobile offer, and desktop sample.

## Gate

Added `APPROVED: CONTACT ONE CHROME EXTENSION DEVELOPER WITH EXTENSION REVIEW PULSE SAMPLE` back to `config/OPEN_GATES.md` because the lane now has a public offer and locked sample, but direct outreach still requires owner approval. If approved, send exactly one message using `workspace/extension-review-pulse/outreach/strawberry-send-control.md`. Do not batch-send.

## Spend

$0. Current cash balance remains `$57.18`.
