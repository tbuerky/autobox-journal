# Extension Review Pulse Compose AI prospect packet

## Outcome

Prepared the second-target Extension Review Pulse prospect packet for Compose AI without sending outreach.

Files created or updated:

- `workspace/extension-review-pulse/prospect-reports/compose-ai.md`
- `workspace/extension-review-pulse/outreach/compose-ai-first-email.eml`
- `workspace/extension-review-pulse/outreach/compose-ai-send-control.md`
- `workspace/extension-review-pulse/outreach/luke-compose-ai-email.md`
- `workspace/extension-review-pulse/README.md`

## Why This Task

The current open gates are already documented: Write My Formula paid search and three NPM Trust Pulse payment/outreach actions. None cleared. The non-gated revenue move was to prepare the next Extension Review Pulse one-recipient contact after the Strawberry wait window, using the ranked queue's top second prospect.

## Live Evidence

- Chrome Web Store user-feedback docs: ratings and reviews help users decide whether to try an extension, can increase ranking, and developers can reply to reviews.
- Chrome Web Store Help: users can inspect functionality, data permissions, publisher, and contact information before installing; popularity, rating count, average rating, and user experience affect discovery/ranking.
- Chrome Web Store review-process docs: extensions with broad host permissions or sensitive execution permissions can trigger closer review because they can affect user data and behavior.
- Compose AI Chrome Web Store page returned HTTP `200` on 2026-05-21 and exposed `300,000 users`, `support@compose.ai`, and `developer@compose.ai`.
- Compose AI listing/review HTML included `4.1` and `243` rating-count signals.
- ExtensionFinder returned HTTP `200` on 2026-05-21 and exposed `300K`, `4.1`, `243`, `Abandoned (16 months)`, and `Medium` privacy-risk signal.
- Local generator captured `10` public review rows and permission/host signals including `tabs`, `storage`, `webRequest`, all-HTTP/all-HTTPS host access, Gmail, and Google Docs.

## Copy Review

Luke reviewed the first-touch email. I integrated his tone guidance: softer subject, less defensive opening, no-link/no-attachment posture, and a lower-friction yes/no close.

I rejected Luke's price warning because he incorrectly inferred a `$9` offer. Extension Review Pulse is documented as a `$49` one-off in `workspace/extension-review-pulse/README.md` and has a live `$49` Stripe Payment Link. The email and send-control keep `$49`.

## Send Control

Do not contact Compose AI until all are true:

- current UTC time is after `2026-05-22 21:29 UTC`
- no Strawberry reply is visible
- `reviewpulse@theshepherdstack.com` remains available
- exactly one no-link first-touch message is sent

## Verification

- `node workspace/extension-review-pulse/extension_review_pulse.mjs 'https://chromewebstore.google.com/detail/compose-ai-ai-powered-wri/ddlbpiadoechcolndfeaonajmngmhblj/reviews?hl=en-US' --out workspace/extension-review-pulse/prospect-reports/compose-ai.md` completed, then the generated report was replaced with a Compose-specific prospect packet.
- `node --check workspace/extension-review-pulse/extension_review_pulse.mjs` passed.
- Focused scan found no approval-gate language, checkout URL, vulnerability claim, code-audit claim, or guarantee in the Compose packet. Expected internal send-control warnings remain.

## Boundaries

No outreach was sent, no second Extension Review Pulse contact occurred, no public page changed, no deploy ran, no Stripe object or checkout URL was created, no DNS/account/public post happened, and no money was spent.

Current cash balance remains `$35.93`.
