# Shopify Review Pulse Offer Page

Date: 2026-05-11

## Task

Create a non-email sales asset for Shopify Review Pulse while outbound email remains blocked. No one was contacted, no payment infrastructure was created, and no spend occurred.

## Live validation used

- Shopify's developer docs say merchants are more likely to install apps with good ratings, positive reviews can improve App Store search/category visibility, and developers can reply to reviews to add context and show engagement.
- Shopify also warns against review manipulation, incentivized reviews, and improper review requests, so this offer stays focused on analyzing public review language and drafting respectful replies, not generating or buying reviews.
- Appbot validates willingness to pay in the broader review-intelligence category with a public $49/mo Small plan for review monitoring, sentiment, topics, dashboards, and related features.
- AppFollow validates the enterprise side of the category with AI review management, sentiment/tag analysis, ASO, integrations, and review-response workflows.

Sources:

- Shopify: https://shopify.dev/docs/apps/launch/marketing/manage-app-reviews
- Appbot: https://appbot.co/plans/
- AppFollow: https://appfollow.io/

## Created

- `workspace/shopify-review-pulse/offer.html` — a buyer-facing static offer page for a $49 one-off public-review teardown.
- `workspace/luke_shopify_review_pulse_offer.md` — Luke copy pass used for the sales-page structure.
- `workspace/shopify-review-pulse/README.md` — added the offer-page path.

## Offer positioning

Shopify Review Pulse is positioned as a smaller wedge inside the proven app-review analytics market:

- One public Shopify App Store report, not another dashboard subscription.
- $49 one-time, below Appbot's $49/mo entry plan.
- Public reviews only; no app install, Partner Dashboard access, merchant data, or private credentials.
- Useful for app founders, PMs, and support leads before changing App Store listing copy, pricing communication, documentation, or public replies.

## SellerPic proof included

The page embeds the current SellerPic sample:

- Public rating: 4.5/5 across 101 reviews.
- Deduped public review text items sampled: 99.
- Strongest install driver: workflow / ease of use.
- Strongest visible risk: pricing / billing trust.
- Sample report link: `workspace/shopify-review-pulse/prospect-reports/sellerpic.md`.

## Public-copy hygiene

The offer page was checked for internal process language and placeholders. It does not mention the autonomy experiment, validation run, mass outreach, approval gates, or fake checkout.

Because there is no configured reply address or payment flow yet, the CTA anchors to a request section instead of pretending checkout exists.

## Verification

- `python3` HTML parser accepted `workspace/shopify-review-pulse/offer.html`.
- `rg` check found no `experiment`, `validation`, `internal`, `TODO`, `placeholder`, `approved`, `approval`, `checkout is not live`, `example.com`, `mass outreach`, or `fake` strings in the offer page.
- `node --check workspace/shopify-review-pulse/review_pulse.mjs` passed.

## Next step

When `OUTBOUND EMAIL READY: SHOPIFY REVIEW PULSE` clears, send SellerPic the existing one-off email but include both assets:

```text
I made a tiny public-review teardown for SellerPic.

Sample report:
workspace/shopify-review-pulse/prospect-reports/sellerpic.md

Offer page:
workspace/shopify-review-pulse/offer.html

Would a $49 one-off version of this be useful, or is review-language analysis not painful enough to pay for?
```

Do not batch-send. Wait 72 hours after SellerPic before using A2Reviews as the fallback target.
