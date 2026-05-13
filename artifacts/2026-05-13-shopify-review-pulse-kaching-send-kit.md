# Shopify Review Pulse Kaching Send Kit

Date: 2026-05-13 16:35 UTC

## Outcome

Prepared Kaching Subscriptions as the third independent outbound target after SellerPic and A2Reviews.

This run did not send outreach, change public pages, create checkout/payment infrastructure, create accounts, touch DNS, or spend money. It converted the existing private Kaching paid-report draft into a ready manual-send kit with verified recipient evidence.

## Files Created

- `workspace/shopify-review-pulse/outreach/kaching-third-email.md`
- `workspace/shopify-review-pulse/outreach/kaching-third-email.eml`

## Live Evidence Checked

- Kaching Subscriptions App Store page identifies the app as **Kaching Subscriptions App**, developer **Kaching Bundles & Upsells**, rating **5.0 (623)**, Built for Shopify, and says app support is provided by Kaching Bundles & Upsells: https://apps.shopify.com/kaching-subscriptions
- Kaching help center says non-installed users can contact support by email: https://support.kachingappz.com/en/articles/8368954-how-can-i-contact-support
- Kaching Subscriptions privacy policy lists `support@kachingappz.com` as the contact email: https://www.kachingappz.com/blogs/privacy-policy-6
- Kaching's public site positions Kaching Subscriptions as its recurring-revenue app and repeats support-quality proof from customer language: https://www.kachingappz.com/

## Send Order

Unchanged:

1. SellerPic first after one send gate clears.
2. Wait 72 hours.
3. A2Reviews fallback if SellerPic does not reply.
4. Kaching only after those first two tests fail or complete.

## Why Kaching Is Worth Having Ready

Kaching is not a distressed prospect. That is part of why it is useful: the pitch is about protecting conversion on a strong app profile, not rescuing bad reviews. Subscription apps carry high trust sensitivity because merchants worry about billing, renewal rules, customer charge amounts, and support urgency. The existing private report draft maps Kaching's tiny low-star bucket to those exact trust questions while preserving the positive support story.

This gives the validation sequence a third target that is different from SellerPic and A2Reviews: a strong, fast-growing subscription app with enough public review volume and a clear contact path.

## Gates

No new gate. Existing gates still control all external action:

- `VERIFY GOOGLE SIGN-IN: reviewpulse@theshepherdstack.com OUTBOUND ACCESS`
- `APPROVED: SEND SELLERPIC TEST FROM ACCESSIBLE OWNER MAILBOX`

Do not send Kaching before SellerPic and A2Reviews have been tested according to the current 72-hour sequence.

## Budget

Cash remains `$162.45`. This run used no paid services and created no recurring spend.
