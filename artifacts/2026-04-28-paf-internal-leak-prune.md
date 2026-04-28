# 2026-04-28 — Profit After Fees public-leak prune

## What was wrong

Three of the live PAF URLs were serving content that should never have been on a public domain selling itself as a finished product:

- `https://profitafterfees.com/launch/launch-packet.md` (HTTP 200)
- `https://profitafterfees.com/launch/forum-answers.md` (HTTP 200)
- `https://profitafterfees.com/launch/search-cluster.md` (HTTP 200)

These were internal launch/process notes. The opening of `launch-packet.md` reads `Owner scope: workspace-only packet for a tiny public experiment site`, then walks through the publish checklist, day-one distribution plan, "success signal for this packet", and forum reply hooks. `search-cluster.md` is a raw on-site SEO cluster sketch with target keywords and angles. `forum-answers.md` is a draft answer bank for forum threads.

Per `config/RULES.md` rule 14 ("Never ship internal-facing copy, experiment notes, SEO scaffolding labels, or process language on a public page") and rule 15, this is a direct quality-gate violation. Any visitor or AdSense reviewer who stumbled into these (linked or not, all are crawlable URLs) would see this site as an experiment, not a product.

A separate stale-duplicate also lived at `https://profitafterfees.com/home/` — a 306-line older homepage variant canonicalized to `/` but still served as a full page on its own URL.

A `break-even-price-calculator.bak/` directory also existed in source (already 404 on production via Vercel filename routing).

## Why now (vs. another SEO page or another packet)

The wakeup brief explicitly called out: "Avoid piling more sections onto the site when the sharper move is pruning, grouping, hierarchy, or stronger product copy. Anything public-facing must be reviewed as customer-facing copy before ship: remove internal labels, experiment language, SEO/process scaffolding, and notes-to-self."

PAF is currently spending paid Google Ads dollars to land first-time visitors and is mid-AdSense approval. Every internal-leak URL on the same domain undermines that spend and that approval, regardless of whether anything links to it.

This was a no-spend, no-owner-input cleanup that the operator could do directly without burning approval budget on Travis.

## What changed

Source deletions:
- `workspace/stripe-profit-calculator/launch/launch-packet.md`
- `workspace/stripe-profit-calculator/launch/forum-answers.md`
- `workspace/stripe-profit-calculator/launch/search-cluster.md`
- `workspace/stripe-profit-calculator/launch/` (directory)
- `workspace/stripe-profit-calculator/home/index.html`
- `workspace/stripe-profit-calculator/home/` (directory)

`break-even-price-calculator.bak/index.html` is owned by `root` in the sandbox, so direct removal failed; `sudo` is gated. The directory remains in source but already 404s on production (Vercel does not serve `*.bak` paths) and is explicitly excluded from the test walker. Nice-to-have, not a public-facing issue.

Test added in `tests/content.test.js`:

```javascript
test('no internal-only or stale-duplicate paths exist that would leak to the live domain', () => {
  const launchDir = resolve(projectRoot, 'launch');
  const homeDir = resolve(projectRoot, 'home');

  assert.equal(existsSync(launchDir), false, 'launch/ contains internal launch/forum/process notes and must not exist in the deployed tree');
  assert.equal(existsSync(homeDir), false, 'home/index.html is a stale duplicate of the homepage and must not exist in the deployed tree');
});
```

No public-facing copy was added or changed in this run. No new sections. Nothing customer-facing was rewritten.

## Verification

Tests:
- `node --test tests/*.test.js` → `113/113 pass` (was `111/111`).

Deploy:
- `vercel deploy --prod --yes` → `READY`, `dpl_FG6ucXTRHiSNCZB2hMpuKsMy8zVH`.
- Aliased to `https://profitafterfees.com` automatically by the project deploy hook.

Live HTTP checks (post-deploy):

| URL | Status |
|-----|--------|
| `https://profitafterfees.com/launch/launch-packet.md` | `404` |
| `https://profitafterfees.com/launch/forum-answers.md` | `404` |
| `https://profitafterfees.com/launch/search-cluster.md` | `404` |
| `https://profitafterfees.com/launch/` | `404` |
| `https://profitafterfees.com/home/` | `404` |
| `https://profitafterfees.com/` | `200` |
| `https://profitafterfees.com/profit-margin-calculator/` | `200` |
| `https://profitafterfees.com/selling-price-calculator/` | `200` |
| `https://profitafterfees.com/ai-feature-cost-calculator/` | `200` |
| `https://profitafterfees.com/privacy/` | `200` |
| `https://profitafterfees.com/ads.txt` | `200` |

All five internal-leak / stale-duplicate URLs are now `404`. All primary calculator pages, the `/privacy/` page, and `/ads.txt` still serve `200`.

## Out of scope (deliberately not touched this run)

Three pairs of overlapping calculator pages all serve `200`:
- `/course-pricing/` vs `/online-course-pricing-calculator/`
- `/software-pricing-calculator/` vs `/saas-pricing-calculator/`
- `/stripe-fee-per-transaction/` vs `/transaction-fee-calculator/`

Each pair has distinct title/H1 and self-canonical, so Google sees three pairs of internal duplication. Consolidating them via 301 redirects is a defensible next pruning move, but each pair has slightly different framing/intent and the right canonical choice deserves its own pass with a brief from Cove on which slug "wins" and explicit owner sign-off if any of these are already accumulating organic clicks. Saving for a future run.

## Budget

No spend. Current cash balance: `$188.75`.
