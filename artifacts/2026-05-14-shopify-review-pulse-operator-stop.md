# Shopify Review Pulse Operator Stop

Date: 2026-05-14 16:18 UTC

## Decision

Stop producing additional Shopify Review Pulse collateral by default. The lane has enough public proof, private fulfillment, fallback targets, and owner-send instructions to test willingness to pay.

The only action that should restart active Review Pulse work is a cleared gate, fresh owner instruction, or a material live-state change.

## Current State

- Public offer is already live at `https://shopify-review-pulse-eta.vercel.app/offer.html`.
- SellerPic locked preview is already live and noindexed at `https://shopify-review-pulse-eta.vercel.app/sellerpic-teardown.html`.
- SellerPic first-send control packet is ready at `workspace/shopify-review-pulse/outreach/sellerpic-send-control.md`.
- A2Reviews fallback preview and email are ready for use only after the SellerPic 72-hour window.
- Kaching and MAG private report drafts exist for later targets only.
- Reply handling and paid-report fulfillment files already exist under `workspace/shopify-review-pulse/fulfillment/`.

## Stop Condition

Do not build another target report, public preview, send kit, offer page, payment recommendation, or gate-recheck artifact for this lane unless one of these happens:

1. Travis clears one of the current Review Pulse gates.
2. SellerPic has been sent and the 72-hour wait has elapsed.
3. A live dependency breaks, such as the offer page or locked preview returning non-200, the noindex header disappearing, or the target contact path changing.
4. Travis gives fresh owner instruction changing the priority.

## Action Map

- On `APPROVED: SEND SELLERPIC TEST FROM ACCESSIBLE OWNER MAILBOX`: send exactly one SellerPic email to `support@sellerpic.ai` from an owner-accessible mailbox using `workspace/shopify-review-pulse/outreach/sellerpic-send-control.md`; record sender, UTC timestamp, and message id if visible; wait 72 hours before A2Reviews.
- On `VERIFY GOOGLE SIGN-IN: reviewpulse@theshepherdstack.com OUTBOUND ACCESS`: send exactly one SellerPic email from the branded Gmail web UI if SMTP from this host still fails; record timestamp and wait 72 hours.
- On `APPROVED: CREATE FREE TALLY INTAKE FORM FOR SHOPIFY REVIEW PULSE`: create or receive the free Tally URL, replace `mailto:` CTAs on the offer and locked previews, redeploy, and verify live CTAs.
- On `CREATE STRIPE PAYMENT LINK: SHOPIFY REVIEW PULSE $49 ONE-OFF REPORT`: create the single $49 Stripe Payment Link, add it only where appropriate, redeploy, and verify checkout links without inventing payment URLs.
- On `APPROVED: PUBLISH SHOPIFY REVIEW PULSE FOUNDER POST`: publish the existing founder-post packet only from the approved account/path, and only if replies can be captured.

## Evidence

This decision is based on the existing completed artifacts and state:

- `artifacts/2026-05-14-shopify-review-pulse-single-action-gate.md`
- `workspace/shopify-review-pulse/outreach/sellerpic-send-control.md`
- `workspace/shopify-review-pulse/fulfillment/reply-and-close-kit.md`
- `workspace/shopify-review-pulse/fulfillment/sellerpic-paid-report-draft.md`
- `workspace/shopify-review-pulse/fulfillment/a2reviews-paid-report-draft.md`
- `workspace/shopify-review-pulse/fulfillment/kaching-paid-report-draft.md`
- `workspace/shopify-review-pulse/fulfillment/mag-product-reviews-paid-report-draft.md`

## Guardrails

- No outreach was sent.
- No public page was changed.
- No checkout or payment infrastructure was created.
- No account was created.
- No DNS was changed.
- No public post was published.
- No spend occurred.
