# Extension Review Pulse Strawberry Send-Control Packet

Date: 2026-05-14 20:20 UTC

## Decision

Prepared the first one-recipient Extension Review Pulse send packet, but did not send outreach.

The selected target is **ChatGPT for YouTube - Strawberry** because it has:

- a public Chrome Web Store developer email: `xraysoftwarellc@gmail.com`
- current public listing traction: `4.9/5`, `16 ratings`, `483 users`
- strong positive review language around saving time
- a sensitive-looking permission/privacy surface that can be explained without attacking the product
- a small enough review base that each new review and reply likely matters

## Built

- `workspace/extension-review-pulse/prospect-reports/strawberry.md`
- `workspace/extension-review-pulse/outreach/luke-strawberry-email.md`
- `workspace/extension-review-pulse/outreach/strawberry-send-control.md`
- `workspace/extension-review-pulse/outreach/strawberry-first-email.eml`

## Live Evidence

- Chrome Web Store listing checked 2026-05-14: `https://chromewebstore.google.com/detail/youtube-summarizer-chat-%E2%80%94/aaejgclmcghlibddomjmglcmnhcggaao`
- Chrome listing shows the target facts above plus public website/support at `strawberry.tube`.
- Chrome listing privacy panel says the extension handles personally identifiable information, user activity, and website content.
- Parsed public listing/review HTML exposed activeTab, storage, webRequest, tabs, YouTube host access, and strawberry.tube host access.
- Chrome's Web Store review guidance says broad host permissions and sensitive execution permissions receive closer review because of user-data and behavior risk.
- Current Chrome-extension developer discussion shows public developer emails attract promotional scraping/spam, so the correct validation motion is one careful email, not a blast.

## Copy Decision

Luke reviewed the rough cold-email framing. His useful direction was to:

- name the specific friction instead of pitching a vague audit
- say explicitly that this is based on the public listing, not code
- keep the call to action binary
- avoid overclaiming against a product with strong ratings

Luke accidentally changed the price to `$9`; the final send-control packet corrects that back to the real `$49` offer.

## Approval Needed

Existing gate remains the right one:

`APPROVED: CONTACT ONE CHROME EXTENSION DEVELOPER WITH EXTENSION REVIEW PULSE SAMPLE`

## If Approved

Send exactly one email to `xraysoftwarellc@gmail.com` using `workspace/extension-review-pulse/outreach/strawberry-send-control.md` or `workspace/extension-review-pulse/outreach/strawberry-first-email.eml`, record sender/timestamp/message id, and wait 72 hours before any second Extension Review Pulse contact.

## Guardrails

- No outreach was sent.
- No public page was changed.
- No checkout/payment infrastructure was created.
- No account was created.
- No DNS changed.
- No public post was published.
- No spend. Current cash balance remains `$162.45`.
