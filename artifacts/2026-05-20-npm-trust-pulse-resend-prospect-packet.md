# NPM Trust Pulse Resend prospect packet

Date: 2026-05-20

## Decision

Prepared one target-specific NPM Trust Pulse prospect packet for Resend. Do not send it until Travis explicitly approves the one-recipient outreach gate.

Approval line:

`APPROVED: CONTACT RESEND WITH NPM TRUST PULSE SAMPLE`

## Why This Task

Write My Formula's next traffic move is gated on paid-search approval. The wakeup prompt says not to repeat a wait-only blocker, so this run moved the non-gated NPM Trust Pulse lane from generic sample to a specific first prospect.

## Live Market Evidence

- Snyk Advisor continues to expose package health scoring for npm packages: `https://snyk.io/advisor/`
- Socket and similar tools validate the broader package-trust/security category.
- OpenSSF Scorecard positions automated repository health metrics as a way for maintainers and consumers to assess security risk: `https://www.scorecard.dev/`
- npm's ecosystem still has visible demand around package security and trust signals.

This keeps the offer anchored to an existing category, but narrows the buyer to commercial SDK maintainers who want their public install surface to look safer and clearer.

## Target Selected

Resend, package `resend`.

Evidence checked:

- npm package: `resend`
- Latest version: `6.12.3`
- Weekly downloads: `5,453,628` from `2026-05-13` to `2026-05-19`
- Repository: `https://github.com/resend/resend-node`
- GitHub stars: `908`
- GitHub open issues: `18`
- GitHub last push: `2026-05-20T11:58:26Z`
- npm license: `MIT`
- Official contact page lists `support@resend.com`, `careers@resend.com`, and `security@resend.com`: `https://resend.com/contact`
- Resend has public security documentation, so the prospect framing should be "make this easier to find from npm", not "you lack security": `https://resend.com/docs/security`

## Files Created

- Prospect report: `workspace/npm-trust-pulse/prospect-reports/resend.md`
- Send-control packet: `workspace/npm-trust-pulse/outreach/resend-send-control.md`
- First-touch `.eml`: `workspace/npm-trust-pulse/outreach/resend-first-email.eml`

## Implementation Note

Also tightened `workspace/npm-trust-pulse/npm_trust_pulse.mjs` so generated buyer-facing fixes no longer recommend license cleanup when the package already has a standard SPDX license.

## Constraints

- No outreach was sent.
- No payment link was created.
- No account was created.
- No public post, deploy, DNS change, checkout change, or spend occurred.

## Next Action

If Travis replies exactly `APPROVED: CONTACT RESEND WITH NPM TRUST PULSE SAMPLE`, send exactly one email using `workspace/npm-trust-pulse/outreach/resend-first-email.eml`, then record the sender and UTC timestamp in `workspace/npm-trust-pulse/outreach/resend-send-control.md` and wait `72` hours before any second NPM Trust Pulse prospect.

