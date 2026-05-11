# Shopify Review Pulse Quality Hardening

Date: 2026-05-11

## Task

Remove the report-quality blocker before Shopify Review Pulse outreach. No email was sent because the outbound sending gate is still open.

## Live validation

- Shopify's developer docs confirm the commercial hook: app ratings affect merchant install trust, and positive reviews can improve App Store search/category placement.
- Shopify also says developers can reply to reviews, and thoughtful replies to negative reviews can show other merchants that the app team is engaged.
- Existing review-analytics products validate the category demand: Appbot and AppFollow both sell app-review monitoring, sentiment, tagging, and review-management workflows. Review Pulse remains a narrower wedge: one-off Shopify App Store teardown instead of another dashboard.
- Public contact paths exist for first targets: SellerPic exposes `support@sellerpic.ai`; RecurrinGO exposes `support@recurringo.com`; A2Reviews exposes `support@a2rev.com`.

## Code changes

Updated `workspace/shopify-review-pulse/review_pulse.mjs`:

- Added public review pagination by following Shopify `rel="next"` links.
- Added a 20-page default cap and `--pages N` override.
- Added a small delay between page requests.
- If Shopify returns HTTP 429 after at least one page, keep the successfully fetched pages instead of failing the entire report.
- Deduped repeated review text blocks.
- Parsed per-review star ratings where present and treat 1-2 star reviews as risk even when they contain positive theme words.
- Ranked top risk by actual negative hits instead of total theme hits, with pricing/support/quality weighted above generic workflow language.
- Tightened report wording from "reviews sampled" to "review text items sampled" because Shopify's archived/reply rendering can expose more public text items than the current rating count.

## Regenerated reports

- `workspace/shopify-review-pulse/prospect-reports/sellerpic.md`
- `workspace/shopify-review-pulse/prospect-reports/recurring-invoices.md`
- `workspace/shopify-review-pulse/prospect-reports/trustpilot-reviews.md`
- `workspace/shopify-review-pulse/prospect-reports/a2reviews.md`

## Pressure-test result

SellerPic remains the first-send target.

- It has a concrete pricing/billing trust issue in public reviews.
- The fuller paginated scrape changed the report from a page-one sample to 99 deduped public review text items.
- The report now separates the positive install driver (`Workflow / ease of use`) from the risk hook (`Pricing / billing trust`).

RecurrinGO is now acceptable only as a conversion-copy extraction test, not as a pain-first teardown.

- Pagination found support-risk text, but the dominant signal is still positive: 101 support-positive hits vs 5 support-risk hits.
- Its website claims 3,000+ Shopify merchants, so a polished conversion-language report may still be useful, but it is weaker than SellerPic for the first willingness-to-pay ask.

A2Reviews is the better second small-developer pain target if a second email is needed.

- Its Shopify listing exposes a direct support complaint and a developer reply that names `support@a2rev.com`.
- Lower review count and smaller developer profile likely mean higher response odds than Trustpilot.

Trustpilot has the strongest public pain but lowest likely response odds.

- The Shopify listing has heavy support/integration complaint clusters.
- It is a large incumbent, so use it as proof that the generator detects real pain, not as an early outbound target.

## First-send recommendation

Do not send a batch. Send one message to SellerPic first, wait 72 hours, then send A2Reviews only if SellerPic produces no reply.

### SellerPic email

To: `support@sellerpic.ai`

Subject: I made a public-review teardown for SellerPic

```text
I am testing a tiny report for Shopify app teams: it reads public App Store reviews and turns them into install drivers, trust risks, and fixes worth shipping this week.

I made one for SellerPic because the public review pattern is specific: merchants praise the workflow and photo output, but the visible install risk is pricing/billing trust.

The report is one page, not a dashboard:
workspace/shopify-review-pulse/prospect-reports/sellerpic.md

Would a $49 one-off version of this be useful, or is review-language analysis not painful enough to pay for?
```

### A2Reviews fallback email

To: `support@a2rev.com`

Subject: I made a public-review teardown for A2Reviews

```text
I am testing a tiny report for Shopify app teams: it reads public App Store reviews and turns them into install drivers, trust risks, and fixes worth shipping this week.

I made one for A2Reviews because the public listing has a clear support-response risk, but also strong positive language around ease of use and review management.

The report is one page, not a dashboard:
workspace/shopify-review-pulse/prospect-reports/a2reviews.md

Would a $49 one-off version of this be useful, or is review-language analysis not painful enough to pay for?
```

## Gate

Approval line: `OUTBOUND EMAIL READY: SHOPIFY REVIEW PULSE`

Immediately after that gate clears, send the SellerPic email only and record reply/non-reply. Do not contact more than one developer in the first 72 hours unless Travis explicitly asks for a broader batch.

## Sources

- Shopify developer docs: `https://shopify.dev/docs/apps/launch/marketing/manage-app-reviews`
- Shopify Help Center app-support docs: `https://help.shopify.com/en/manual/apps/getting-support`
- SellerPic reviews: `https://apps.shopify.com/sellerpic/reviews`
- RecurrinGO site/contact: `https://recurringo.com/`
- A2Reviews listing/contact evidence: `https://apps.shopify.com/a2reviews`
- Appbot: `https://appbot.co/`
- AppFollow: `https://appfollow.io/`

## Verification

- `node --check workspace/shopify-review-pulse/review_pulse.mjs`
- Regenerated SellerPic and A2Reviews successfully with paginated public review fetching.
- RecurrinGO and Trustpilot regeneration hit Shopify 429 after deeper pagination in one run; the script now preserves partial fetched pages after a 429 instead of discarding the report.

Cash balance: $162.45. Spend: $0.
