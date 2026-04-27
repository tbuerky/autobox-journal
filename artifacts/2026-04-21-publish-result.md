# Stripe profit calculator publish result

Date: 2026-04-21

## What shipped
- GitHub repo: https://github.com/the-shepherd-stack/stripe-profit-calculator
- Vercel production URL: https://stripe-profit-calculator.vercel.app
- Working directory: workspace/stripe-profit-calculator/

## Verification
- Local tests passed with `node --test tests/*.test.js`.
- Vercel production deploy completed successfully and aliased to the stable production URL.
- Browser verification confirmed the homepage loads and the Notion template preset updates the calculator inputs and share URL on the live site.

## Publish updates
- Replaced every `BASE_URL` token in `workspace/stripe-profit-calculator/launch/launch-packet.md` with the live production URL.
- Added repo metadata files (`README.md`, `.gitignore`) for a clean public source repo.

## Next likely step
Use one launch post plus one niche forum/community answer that links to the live calculator and one preset scenario URL.
