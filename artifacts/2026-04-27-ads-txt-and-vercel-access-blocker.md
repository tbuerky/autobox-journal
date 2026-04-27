# 2026-04-27 — PAF ads.txt source fix + live Vercel alias permission blocker

## What was found
Live `https://profitafterfees.com/ads.txt` returned `HTTP 404`. Google AdSense expects an `ads.txt` file at the site root that authorizes the publisher. Without it, AdSense can mark inventory as unauthorized and demand-side platforms can suppress bids — directly capping AdSense revenue on every Google Ads click Travis is paying for.

Sitewide audit also confirmed zero manual `<ins class="adsbygoogle">` ad slots exist anywhere on the site, so AdSense revenue today depends entirely on Auto Ads being approved AND enabled in the publisher console for `profitafterfees.com`. That is a separate question from `ads.txt` and is captured in "Open question for Travis" below.

## What I changed in source
- New file `workspace/stripe-profit-calculator/ads.txt` containing exactly one line:
  ```
  google.com, pub-3560388500961643, DIRECT, f08c47fec0942fa0
  ```
  - `pub-3560388500961643` matches the publisher ID already public in the AdSense head script (`ca-pub-3560388500961643`).
  - `f08c47fec0942fa0` is Google's well-known certification authority ID for AdSense and is constant across publishers.
- New regression in `workspace/stripe-profit-calculator/tests/content.test.js` asserting that `ads.txt` exists at the site root and contains the canonical AdSense DIRECT line.

## Verification (source + project Vercel deploy)
- `node --test tests/*.test.js` passed `110/110`.
- `vercel deploy --prod --yes` returned a successful production deployment in the project `travis-buerkys-projects/stripe-profit-calculator` at `https://stripe-profit-calculator-brkibl9i5-travis-buerkys-projects.vercel.app`. (Direct fetch of that URL is gated by Vercel deployment protection, which is normal for preview/canonical project URLs.)

## Live blocker (permission gate)
- `vercel alias set ... profitafterfees.com` and `... www.profitafterfees.com` both returned `Error: You don't have access to the domain profitafterfees.com under travis-buerkys-projects.`
- `vercel teams ls` only lists `travis-buerkys-projects` (`team_D1xtJO462AlXr8nD1kCG8ymc`); the previously-cached `team_EGsm5UDqHv7Y9FKIhCOaILSK` returns `current_team_invalid` ("not a member of the current team anymore").
- `vercel domains ls --scope team_D1xtJO462AlXr8nD1kCG8ymc` does not include `profitafterfees.com` — that team owns 8 other domains (`one-page-site.com`, `theshepherdstack.com`, etc.) but not the PAF apex.
- `.vercel/project.json` in the workspace was rewritten at `2026-04-27 20:06:07 UTC` to `prj_LlUvP2WegJFuBldkyFWl8tnuM1Rs` / `team_D1xtJO462AlXr8nD1kCG8ymc`, which does not match the project currently aliased to the apex.
- Live apex is still serving the prior good deploy (privacy page reachable, `no tracking` claim absent), so customer-facing state has not regressed; it is just frozen at the previous deploy state.

## What this means
- The `ads.txt` source change is shipped and tested but is **not yet live on the apex**, because the deployment chain that points to `profitafterfees.com` is no longer reachable from this sandbox.
- Every subsequent change to PAF that needs to reach customers will hit the same wall until the access is fixed.

## What I need from Travis (one approval / action)
Pick exactly one option and reply. After that, I will redeploy ads.txt to the live apex within one run.

**Option A — restore my access to the team that owns the domain (preferred).**
Re-add this Vercel CLI session (user `tbuerky`, token `vca_6ebs…BV0xEWE7` if rotated, or whatever new token Travis prefers) to whichever team currently owns `profitafterfees.com`. Then drop me a short Discord note: `VERCEL ACCESS RESTORED: <team-slug>`. I will re-link `.vercel/project.json` and redeploy.

**Option B — Travis runs the alias from his own machine.**
1. `cd workspace/stripe-profit-calculator` (or any clone of the same source).
2. `git pull` (if synced) so `ads.txt` is present locally. If not synced, copy the one-line file:
   ```
   google.com, pub-3560388500961643, DIRECT, f08c47fec0942fa0
   ```
   into the site root.
3. `vercel deploy --prod` and then `vercel alias set <new-deploy-url> profitafterfees.com` and `... www.profitafterfees.com` from his authorized account.
4. Reply `ADS.TXT LIVE` and I will verify.

**Option C — move/reattach the domain.**
Reattach `profitafterfees.com` and `www.profitafterfees.com` to the project `travis-buerkys-projects/stripe-profit-calculator` (`prj_LlUvP2WegJFuBldkyFWl8tnuM1Rs`). After that, my next `vercel alias set` will succeed and I will redeploy.

## Open question for Travis (capture once access is back)
Independent of `ads.txt`, please confirm:
1. AdSense account approval status for `profitafterfees.com` (approved / pending / limited / disapproved).
2. Whether **Auto Ads** is enabled in the AdSense console for this site.
3. If Auto Ads is enabled and the account is approved, current daily impressions/eCPM/estimated earnings (any non-zero number from the AdSense dashboard).

If Auto Ads is the chosen monetization mode and the account is approved, no further code changes are needed beyond `ads.txt` going live. If you want manual placements (typically higher fill rate on calculator-heavy pages), reply with one ad unit slot ID from the AdSense console and I will add a single in-content `<ins class="adsbygoogle">` slot to the homepage results card and verify it serves.

## Why this was the chosen task
PAF, StrikeSight, and the AI utility all currently sit behind owner-side approval/evidence gates. The wakeup brief explicitly told me to avoid piling more sections onto the site and to look for sharper monetization, conversion, or quality-control work. A missing `ads.txt` is a real revenue gap on the only paid-traffic property in the portfolio: every Google Ads click that lands on PAF passes through a site whose AdSense relationship is currently unverifiable to demand-side platforms. Fixing it is concrete, no-spend, and reversible.

Suggested post copy: not applicable — this is an internal access blocker, not a public copy task.

Current cash balance: `$188.75`. No spend occurred.
