# Shopify Review Pulse fulfillment kit

Date: 2026-05-12

## Task

Create the private paid-report fulfillment kit so the first positive reply or $49 payment can be served without another strategy, copy, or workflow pass.

## Why this was the right non-gated move

The current revenue blockers are owner gates:

- `CREATE/CONNECT MAILBOX: reviewpulse@theshepherdstack.com FOR SHOPIFY REVIEW PULSE OUTBOUND`
- `CREATE STRIPE PAYMENT LINK: SHOPIFY REVIEW PULSE $49 ONE-OFF REPORT`
- `APPROVED: PUBLISH SHOPIFY REVIEW PULSE FOUNDER POST`

Another landing-page or teaser polish pass would not create more leverage. The remaining autonomous gap was fulfillment readiness: if Travis creates the mailbox, creates the Stripe link, or publishes the founder post and someone replies, Review Pulse needs to deliver a credible paid report quickly.

## Live validation used

- Shopify says merchants are more likely to install apps with good ratings, and positive reviews can affect App Store search/category visibility.
- Shopify lets developers reply to public app reviews, so reply drafts are a useful deliverable.
- Shopify partner guidance says review replies should build trust, stay specific, and avoid creating a negative merchant experience.
- AppFollow's current review-management positioning validates that teams pay for review tagging, metrics, templates, and review workflow.

## Built

- `workspace/shopify-review-pulse/fulfillment/paid-report-template.md`
  - Private template for a paid one-off report.
  - Sections: executive read, install drivers, trust risks, App Store page edits, public reply drafts, one-week action plan, and compliance checks.

- `workspace/shopify-review-pulse/fulfillment/sellerpic-paid-report-draft.md`
  - Private paid-report version for SellerPic.
  - Converts the generated public-review sample into concrete deliverables: listing copy, pricing clarity text, support/reply drafts, and a three-step action plan.
  - This file must not be published or attached to the locked teaser before payment or explicit sample approval.

- `workspace/shopify-review-pulse/fulfillment/delivery-checklist.md`
  - Step-by-step first fulfillment workflow.
  - Includes regeneration command, evidence spot-check, compliance pass, delivery package, and delivery email template.

- `workspace/shopify-review-pulse/README.md`
  - Documents the private fulfillment kit and warns not to deploy or expose it.

- `workspace/shopify-review-pulse/.vercelignore`
  - Explicitly excludes `fulfillment/` in addition to the existing Markdown/source/outreach/prospect exclusions.

## Verification

- `node --check workspace/shopify-review-pulse/review_pulse.mjs` passed.
- `find workspace/shopify-review-pulse/fulfillment -type f -maxdepth 1 -print -exec wc -w {} \;` confirmed three private fulfillment files exist:
  - `delivery-checklist.md`
  - `paid-report-template.md`
  - `sellerpic-paid-report-draft.md`
- `.vercelignore` now explicitly excludes `fulfillment/`, so these private paid-report files are not part of the public Vercel deployment.

## No-gate actions avoided

- No outreach sent.
- No checkout or payment infrastructure created.
- No public post made.
- No spend.
- No StrikeRewind or PAF work.

## Next move

If the mailbox gate clears first, send exactly one SellerPic message using the existing `.eml`. If the Stripe Payment Link gate clears first, add that payment link to the public offer page before sending. If the publish gate clears first, publish the founder post only after reply handling is ready.

## Sources

- Shopify review management docs: https://shopify.dev/docs/apps/launch/marketing/manage-app-reviews
- Shopify partner review-reply guidance: https://www.shopify.com/partners/blog/reply-to-reviews/
- AppFollow review management page: https://get.appfollow.io/app-review-management
