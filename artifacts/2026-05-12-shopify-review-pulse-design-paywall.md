# Shopify Review Pulse design/paywall run

Date: 2026-05-12

## Shipped

- Rebuilt the public landing page: `workspace/shopify-review-pulse/offer.html`
- Rebuilt the SellerPic report as a locked teaser preview: `workspace/shopify-review-pulse/sellerpic-teardown.html`
- Updated the first SellerPic email draft so it leads with the live locked preview and does not reveal the diagnosis in the email body: `workspace/shopify-review-pulse/outreach/sellerpic-first-email.md`
- Deployed to Vercel production:
  - Landing: https://shopify-review-pulse.vercel.app/offer.html
  - SellerPic locked preview: https://shopify-review-pulse.vercel.app/sellerpic-teardown.html
  - Final deployment: `dpl_A1FNPc11zN2AyWRkZSDcWFskr2WX`
- Screenshots:
  - `workspace/artifacts/2026-05-12-shopify-review-pulse-design/landing-desktop.png`
  - `workspace/artifacts/2026-05-12-shopify-review-pulse-design/landing-mobile.png`
  - `workspace/artifacts/2026-05-12-shopify-review-pulse-design/teaser-desktop.png`
  - `workspace/artifacts/2026-05-12-shopify-review-pulse-design/teaser-mobile.png`
- Domain/email recommendation: `artifacts/2026-05-12-shopify-review-pulse-domain-email-recommendation.md`

## What changed

The public page now presents Shopify Review Pulse as a focused $49 report for Shopify app teams. It explains who it is for, what the report checks, how the locked preview works, why the broader category is credible, and how to request the report without pretending checkout exists.

The SellerPic page no longer gives away the diagnosis, exact review evidence, or fixes. It shows:

- 102 public reviews identified
- 99 review text items sampled
- 5 review pages scanned
- 3 positive theme groups
- 3 risk theme groups
- severity bands
- locked deliverables: theme table, exact review evidence, prioritized action steps, listing-copy rewrite, reply drafts, pricing/onboarding clarity, and support-copy fixes

## Research used

- Shopify developer docs: app developers can manage and reply to reviews; published reviews are visible and count toward rating.
- Appbot: validates the paid category with review sentiment, topics, dashboards, and integrations; Small plan is listed at $49/month annually or $59 monthly.
- AppFollow: validates review-management demand with sentiment, tagging, AI replies, and automation.
- CARFAX report structure: supports the "summary first, details inside the full report" pattern.
- Hunter: current free plan includes 50 monthly credits and one connected email account, but it still requires account setup, so it is optional later rather than needed for the first SellerPic send.

## Verification

- HTML parser accepted both changed pages.
- `node --check workspace/shopify-review-pulse/review_pulse.mjs` passed.
- Public landing leak check found no real prospect names in `offer.html`.
- SellerPic teaser has both `<meta name="robots" content="noindex,nofollow">` and Vercel `X-Robots-Tag: noindex, nofollow`.
- Playwright Chromium screenshots were generated for desktop and mobile.
- Visual screenshot pass found no mobile text overlap or horizontal overflow requiring another iteration.
- Live Vercel checks:
  - `https://shopify-review-pulse.vercel.app/offer.html` returned HTTP 200.
  - `https://shopify-review-pulse.vercel.app/sellerpic-teardown.html` returned HTTP 200 with `x-robots-tag: noindex, nofollow`.
  - Internal files (`README.md`, outreach draft, raw prospect report, source script) returned HTTP 404 after adding `.vercelignore`.

## Gate

Replaced the vague mailbox gate with the exact next owner action:

`CREATE/CONNECT MAILBOX: reviewpulse@theshepherdstack.com FOR SHOPIFY REVIEW PULSE OUTBOUND`

After that clears, send only the SellerPic email and wait 72 hours before any fallback target.

## Discord-ready update

Did: rebuilt Shopify Review Pulse landing + locked SellerPic teaser, deployed live, added screenshots, and tightened the mailbox gate.
See: https://shopify-review-pulse.vercel.app/offer.html and https://shopify-review-pulse.vercel.app/sellerpic-teardown.html
Next: create/connect reviewpulse@theshepherdstack.com, then send only the SellerPic email and wait 72h.
Blocked on you: `CREATE/CONNECT MAILBOX: reviewpulse@theshepherdstack.com FOR SHOPIFY REVIEW PULSE OUTBOUND` (+1 more)

Attempted direct Discord post, but the configured bot request returned HTTP 403.

## Cash

$162.45 unchanged. No spend.
