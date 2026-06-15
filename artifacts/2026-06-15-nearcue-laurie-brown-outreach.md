# NearCue Laurie Brown Outreach

Date: 2026-06-15 08:33 UTC

## Task

Sent one researched, no-attachment first-touch email to Laurie Brown at `laurie@lauriebrown.com` for NearCue.

## Why This Target

NearCue needs a first buyer and current owner state prioritizes no-spend, people-first distribution without public posts, paid ads, or bulk sending.

Laurie Brown is a fit because her public virtual-presentation coaching page discusses camera choice, eye contact, on-camera best practices, remembering a presentation, and building effective virtual presence. The page publishes `laurie@lauriebrown.com`.

Live page checked:
- `https://lauriebrown.com/results-and-public-speaking-coach/virtual-presentation-coach/`

NearCue maps to that workflow as a tiny browser cue strip that keeps a few speaking beats near the webcam line.

## Controls

- One recipient only.
- No attachment.
- No spend.
- No public post.
- No partnership, affiliate, endorsement, guarantee, call request, or bulk-send language.
- Gmail prior-contact search found no matching thread for `laurie@lauriebrown.com`, `lauriebrown.com`, or `Laurie Brown` in the last 365 days.
- Recent NearCue reply search found only the two prior sent NearCue emails and no inbound reply needing handling.
- Luke reviewed the buyer-facing email; operator accepted the stronger problem-led subject and softened the suggested "no scrolling script" line because the app advances short beats rather than scrolling a full script.

## Verification

- `https://nearcue.vercel.app/` returned HTTP `200`.
- `https://nearcue.vercel.app/app/` returned HTTP `200` and page content includes `NearCue Studio`, script input, cue strip, and opacity controls.
- Stripe Payment Link `plink_1TiOtW4BEFFaauKWBjsXvOD4` is active, redirects after completion to `https://nearcue.vercel.app/thanks`, and line items show one-time `amount_total: 399` USD with no recurring or subscription data.
- Stripe checkout sessions for that payment link are still open/unpaid, so no NearCue sale is verified.
- Stripe product `prod_UhoWIJQR4kcK3n` is named `NearCue`; the expanded Payment Link line item still has stale description `NotchPrompter`, which should be cleaned up in a later single-task run if it appears buyer-visible.
- Gmail send returned id/thread `19eca69fb1ffe9b3` with `SENT` label.
- Gmail readback verified sender `Travis Buerky <tbuerky@gmail.com>`, recipient, subject, body, `SENT` label, and no attachments.

## Email

Subject: `a small tool for keeping your eyes up on camera`

```text
Hi Laurie,

Your virtual presentation coaching covers a lot of what I was thinking about when I built this: camera setup, eye contact, and remembering your points without breaking presence.

I made a small browser tool for that last part. It's called NearCue. You paste in 5 to 10 short speaking beats, and it holds them as a translucent strip near the top of the screen, close to the webcam, so someone can glance at the next point without dropping their eyes to a document or a notes window.

You can try the studio here: https://nearcue.vercel.app/app/

It's $3.99 once, no subscription. If it looks useful for clients working on on-camera presence, the checkout link is here: https://buy.stripe.com/bJe9AMdkFbHigm477A4F20a

No attachment and nothing to schedule. It just seemed close to the work you already teach.

Best,
Travis
```

## Result

No sale is verified yet. Next NearCue action should continue no-spend people-first distribution only if no reply needs handling, or clean up the stale Stripe line-item description if buyer-visible checkout copy shows the old name.

Current cash balance remains `-$24.07`.
