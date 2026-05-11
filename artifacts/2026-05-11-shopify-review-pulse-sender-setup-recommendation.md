# Shopify Review Pulse Sender Setup Recommendation

Date: 2026-05-11

## Task

Convert the remaining outbound-email blocker into one concrete sender recommendation. No email was sent, no new credential was used, no account was created, and no money was spent.

## Recommendation

Use a known Gmail or Google Workspace mailbox for the first Shopify Review Pulse email.

Approval line: `CONNECT GMAIL: SHOPIFY REVIEW PULSE OUTBOUND`

## Why this is the right next move

The next revenue test is not an email-infrastructure project. It is one human-quality willingness-to-pay email to SellerPic, then a 72-hour wait.

Gmail is the smallest credible sender path because:

- The first test is one recipient, not a campaign.
- Replies land in a real inbox instead of an API dashboard.
- No domain purchase, paid email platform, DNS setup, or payment method is required.
- A known mailbox is more natural for a founder-style validation note than a fresh transactional-email domain.

## Live sender research

- Google says personal Gmail accounts can hit a sending limit at more than 500 recipients/messages in a day. This test sends one message, so volume is not the constraint.
- Google Workspace documents a daily user sending limit of 2,000 messages, with lower limits for trial accounts, and notes that limits are rolling 24-hour limits that can change.
- Resend's free plan lists 3,000 emails/month and 100 emails/day, but it still requires sender setup and introduces API/key/domain work before the first customer signal.
- Postmark offers a no-expiration Developer plan with 100 emails/month, but it is still an email-service setup step and is a better fit after the first manual willingness-to-pay signal.

Sources:

- Google Gmail limits: https://support.google.com/mail/answer/22839?hl=en
- Google Workspace sending limits: https://support.google.com/a/answer/166852?hl=en
- Resend pricing: https://resend.com/pricing
- Postmark pricing FAQ: https://postmarkapp.com/support/article/1285-pricing-billing-faq

## Options considered

| Option | Cost | Setup | Reply handling | Verdict |
|---|---:|---|---|---|
| Gmail / Google Workspace mailbox | $0 if existing mailbox is used | Owner connects/authorizes mailbox | Native inbox | Pick |
| Resend free | $0 | New account/API/domain setup | Possible, but extra setup | Later |
| Postmark Developer | $0 | New account/API/domain setup | Possible, but transactional-service shaped | Later |
| Manual copy/paste by Travis | $0 | None | Native inbox | Acceptable fallback, but less autonomous |

## Immediate post-approval action

After Travis approves `CONNECT GMAIL: SHOPIFY REVIEW PULSE OUTBOUND`, send exactly one email:

- To: `support@sellerpic.ai`
- Subject: `I made a public-review teardown for SellerPic`
- Body: use `workspace/shopify-review-pulse/outreach/sellerpic-first-email.md`

Then:

1. Record the send timestamp in `config/RUNLOG.md` and `config/HANDOFF.md`.
2. Wait 72 hours.
3. If no reply, send the A2Reviews fallback only.
4. Do not batch-send unless Travis explicitly widens the approval.

## Draft created

- `workspace/shopify-review-pulse/outreach/sellerpic-first-email.md`

The draft includes both current assets:

- SellerPic report: `workspace/shopify-review-pulse/prospect-reports/sellerpic.md`
- Offer page: `workspace/shopify-review-pulse/offer.html`

## Verification

- Checked local scripts/config/workspace for existing SMTP or outbound email tooling; none was configured.
- Confirmed the latest Codex compaction handoff is older than the latest completed Codex run.
- No external contact was made.

Cash balance: $162.45. Spend: $0.
