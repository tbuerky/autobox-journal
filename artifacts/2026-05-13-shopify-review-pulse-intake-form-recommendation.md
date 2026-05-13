# Shopify Review Pulse Intake Form Recommendation

Date: 2026-05-13

## Outcome

Created a concrete free-form intake recommendation for Shopify Review Pulse and raised one approval gate.

No form account was created, no public page was changed, no checkout was created, no outreach was sent, and no spend occurred.

## Why This Was the Right Task

The active Review Pulse revenue motions remain gated:

- outbound SellerPic email depends on Google sign-in verification
- payment collection depends on Stripe Payment Link approval
- public founder-post distribution depends on publish approval

The public offer page currently uses a `mailto:` request CTA pointed at `reviewpulse@theshepherdstack.com`, the same mailbox that is not accessible yet. That means a visitor could try to request a report before the mailbox gate clears and the request could be missed. A free hosted intake form is the smallest credible bypass for inbound demand capture.

This does not replace the first SellerPic email. It makes the public page and founder post safer to use once Travis approves the form path.

## Live Research

- Tally's official pricing page says it offers unlimited forms and submissions with most features free: https://tally.so/help/plans-and-pricing
- Formspree's official docs say Free starts at 50 submissions per month and stores 30 days of submission history: https://help.formspree.io/articles/account-management/account-limits/
- Google Forms can create shareable or embeddable forms, but it depends on Google account access, which is already the current Review Pulse bottleneck: https://workspace.google.com/products/forms/

## Options Considered

1. **Tally free form — recommended.** Best fit because it avoids code, avoids spend, and is not tied to the currently blocked Google mailbox. Travis can create the form and share the URL; Codex can then wire it into the public offer page and founder-post copy.
2. **Formspree.** Good for static HTML, but the free tier is capped and notifications still want a working email address. It is more useful after the mailbox is accessible.
3. **Google Forms.** Good free tool, but it routes through the same Google-account surface currently blocking the mailbox. It is not the cleanest workaround.
4. **Keep mailto only.** Rejected because it leaves the public request path dependent on a mailbox that is currently inaccessible.

## Exact Approval Needed

```text
APPROVED: CREATE FREE TALLY INTAKE FORM FOR SHOPIFY REVIEW PULSE
```

## Form Spec Created

New spec:

```text
workspace/shopify-review-pulse/intake/tally-form-spec.md
```

It includes the title, description, success message, field list, consent checkbox, and the exact site-update steps after a Tally URL exists.

## What Happens After Approval

1. Travis creates the free Tally form from the spec and provides the form URL, or approves Codex to create it if credentials/access are available.
2. Codex replaces the `mailto:` CTAs in the public offer page and locked previews with the Tally URL.
3. Codex updates the founder-post packet to point at the form before publishing.
4. Codex redeploys the Shopify Review Pulse Vercel project and verifies the live CTAs.

## Gate Reconciliation

Kept existing gates:

- `VERIFY GOOGLE SIGN-IN: reviewpulse@theshepherdstack.com OUTBOUND ACCESS`
- `CREATE STRIPE PAYMENT LINK: SHOPIFY REVIEW PULSE $49 ONE-OFF REPORT`
- `APPROVED: PUBLISH SHOPIFY REVIEW PULSE FOUNDER POST`

Added:

- `APPROVED: CREATE FREE TALLY INTAKE FORM FOR SHOPIFY REVIEW PULSE`

## Verification

- Confirmed `workspace/shopify-review-pulse/offer.html`, `sellerpic-teardown.html`, and `a2reviews-teardown.html` all currently contain `mailto:reviewpulse@theshepherdstack.com` CTAs.
- Created a concrete form spec under `workspace/shopify-review-pulse/intake/`.
- Did not change any public URL or payment surface before approval.
- Budget unchanged at `$162.45`.
