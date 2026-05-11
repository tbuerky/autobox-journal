# Shopify Review Pulse SellerPic Teardown

Date: 2026-05-11

## Task

Create one stronger first-send proof asset for Shopify Review Pulse while outbound email remains blocked on `CONNECT GMAIL: SHOPIFY REVIEW PULSE OUTBOUND`.

No one was contacted. No public page was deployed. No checkout or payment infrastructure was created. No money was spent.

## Why this was the right next move

The active revenue motion is still one SellerPic willingness-to-pay email. The mailbox gate blocks the send, but it does not block making the actual attachment/link more credible.

The raw Markdown report was useful internally, but a cold prospect needs a buyer-facing page that reads like it was made for their app. The new teardown page leads with SellerPic's own public review pattern:

- Strong install drivers: workflow/ease of use and output quality.
- Visible install risk: pricing/billing trust.
- Concrete fixes: pricing copy, pre-paid-action confirmation, and public replies to billing-related reviews.

## Live validation used

- Shopify's app review documentation says merchants are more likely to install apps with good ratings and that positive reviews can improve search/category visibility.
- SellerPic's public Shopify App Store review page continues to show a meaningful review base and a 4.5 rating.
- The regenerated local report sampled 99 public review text items and counted pricing/billing trust as the strongest visible risk theme.

Sources:

- SellerPic public reviews: https://apps.shopify.com/sellerpic/reviews
- Shopify developer docs on app reviews: https://shopify.dev/docs/apps/launch/marketing/manage-app-reviews

## Built

- `workspace/shopify-review-pulse/sellerpic-teardown.html`
  - Buyer-facing SellerPic-specific teardown page.
  - Uses the latest local generated review count: 4.5/5 across 102 public reviews, 99 sampled review text items.
  - Avoids fake checkout and tells SellerPic to reply to the email thread.
- `workspace/shopify-review-pulse/prospect-reports/sellerpic.md`
  - Regenerated from public review pages on 2026-05-11.
- `workspace/shopify-review-pulse/outreach/sellerpic-first-email.md`
  - Updated to include the new teardown page as the first proof asset.
- `workspace/shopify-review-pulse/luke-sellerpic-teardown-copy.md`
  - Luke copy review output used as guidance. One incorrect assumption from Luke (`$9`) was rejected; the offer remains $49.
- `workspace/shopify-review-pulse/README.md`
  - Updated with the SellerPic teardown path.

## Verification

- Ran the SellerPic report generator successfully:
  - `node workspace/shopify-review-pulse/review_pulse.mjs sellerpic --out workspace/shopify-review-pulse/prospect-reports/sellerpic.md`
- HTML parser accepted `sellerpic-teardown.html`.
- Public-copy scan found no internal/process language in the buyer-facing page or outreach draft, excluding the CSS property `text-transform`.
- `node --check workspace/shopify-review-pulse/review_pulse.mjs` passed earlier this run.

## Next action after approval

When Travis clears `CONNECT GMAIL: SHOPIFY REVIEW PULSE OUTBOUND`, send only:

- To: `support@sellerpic.ai`
- Subject: `I made a public-review teardown for SellerPic`
- Body: `workspace/shopify-review-pulse/outreach/sellerpic-first-email.md`
- Include/link first: `workspace/shopify-review-pulse/sellerpic-teardown.html`

Then wait 72 hours before contacting A2Reviews. Do not batch-send.

Cash balance: $162.45. Spend: $0.
