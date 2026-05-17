# Shopify Review Pulse A2Reviews Fallback Gate

Date: 2026-05-17 20:32 UTC

## Decision

The SellerPic 72-hour wait has elapsed and A2Reviews is now the correct fallback target, but I did not send the email from the connected Gmail account because the authenticated sender is `tbuerky@gmail.com` while the prepared outreach is from Mara at Review Pulse. Sending the branded outreach from Travis's personal Gmail would cross a sender-identity permission line.

## Evidence

- `conversion_readiness` returned `ready_for_fallback` at `2026-05-17T20:32:12.690Z`.
- The checker confirmed:
  - Review Pulse offer page HTTP 200: `https://shopify-review-pulse-eta.vercel.app/offer`
  - Stripe checkout HTTP 200: `https://buy.stripe.com/7sY4gs0xT9za9XGdvY4F203`
  - SellerPic listing HTTP 200 with `4.5/5` across `101` reviews
- Connected Gmail profile is `tbuerky@gmail.com`.
- Final Gmail searches returned no message IDs for SellerPic/reviewpulse signals, `from:support@sellerpic.ai`, or `to:reviewpulse@theshepherdstack.com` over the last 14 days. This still does not prove the separate `reviewpulse@theshepherdstack.com` inbox has no reply unless forwarding exists.
- Live web research revalidated A2Reviews as the fallback prospect: Shopify App Store shows A2Reviews at `4.1` across `23` reviews, and the listing/review surface includes the public contact path `support@a2rev.com`.
- Local test suite passed: `node --test workspace/shopify-review-pulse/tests/*.test.mjs` returned 10/10 passing tests.

Source: https://apps.shopify.com/a2reviews

## Exact Gate

`SEND: A2REVIEWS FALLBACK FROM REVIEWPULSE MAILBOX`

## Immediate Action After Gate Clears

Send exactly one first-touch email to `support@a2rev.com` from `reviewpulse@theshepherdstack.com` or another explicitly approved branded/reply-capable Review Pulse sender. Do not send Kaching, MAG, or Extension Review Pulse in parallel.

## Suggested post copy:

```text
To: support@a2rev.com
Subject: A2Reviews public review notes

Hi A2Reviews team,

I am Mara from Review Pulse. I was looking at public Shopify App Store reviews and pulled together a short A2Reviews-specific review teardown from public listing/review data.

The useful parts are the merchant themes that repeat, the objections that may slow installs, and a few listing/reply copy fixes.

Is this the right inbox for that, or could you point me to whoever owns A2Reviews' Shopify listing or customer-review workflow?

Thanks,
Mara
```

## Not Done

- No A2Reviews email was sent.
- No SellerPic follow-up was sent.
- No public page, checkout/payment infrastructure, DNS, account, public post, or budget change was made.
