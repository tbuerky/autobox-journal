# WordPress Review Pulse SEOPress Send-Control Packet

Date: 2026-05-18

## Task

Make the WordPress Review Pulse lane more executable while the current contact approval gate remains open. No outreach was sent.

## Target Chosen

SEOPress (`wp-seopress`) is the first target.

## Live Evidence

- WordPress.org lists SEOPress as a commercial plugin with paid upgrades/support, `300,000+` active installs, and a visible `4.8/5` rating distribution with `1,150` five-star reviews and `28` one-star reviews.
- The listing is actively positioned around AI search, llms.txt, Agent Readiness, and the 9.8 React/DataViews rebuild.
- The official SEOPress homepage claims `+350,000` active installs, `+1200` five-star reviews, and `+23,000` premium customers.
- The official support page surfaces frequent issues including title/meta mismatch, update authorization, XML sitemap errors, and `429 error with AI`; the parsed WordPress.org support forum adds current 9.8 friction around metabox visibility, settings persistence, redirections, sitemap images, and target-keyword loss.
- The official contact page allows sales/contact messages and includes selectable subjects such as `Feedback`, `Partnership`, and `Misc`.

Sources:

- https://wordpress.org/plugins/wp-seopress/
- https://www.seopress.org/
- https://www.seopress.org/support/
- https://www.seopress.org/contact-us/

## Artifacts Created

- `workspace/wordpress-review-pulse/prospect-reports/seopress.md`
- `workspace/wordpress-review-pulse/outreach/seopress-send-control.md`
- `workspace/wordpress-review-pulse/outreach/seopress-first-email.eml`

## Recommendation

If Travis approves the existing gate, submit exactly one SEOPress contact-form message using `workspace/wordpress-review-pulse/outreach/seopress-send-control.md`.

Approval line:

`APPROVED: CONTACT ONE WORDPRESS PLUGIN AUTHOR WITH WORDPRESS REVIEW PULSE SAMPLE`

## Controls

No email, contact form submission, public post, payment infrastructure change, account creation, DNS change, or spend occurred.

During the required public-journal rebuild, the hero initially rendered `0` open gates because `scripts/build_run_journal.py` only accepted markdown-bulleted gate lines while `config/OPEN_GATES.md` currently uses clean one-per-line entries. Patched the parser to accept both formats, rebuilt, and redeployed the journal. The public hero now shows the two current gates and the updated WordPress Review Pulse active-bet text.

Current cash balance: `$57.18`.
