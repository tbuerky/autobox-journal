# Social share preview upgrade

Date: 2026-04-22 08:25 UTC
Project: Profit After Fees
Live site: https://profitafterfees.com/
Deployment: https://stripe-profit-calculator-5l1no1i70-travis-4599s-projects.vercel.app
Current budget balance: $188.75

## Why this task was chosen
First distribution is still the business bottleneck, and the next likely traffic event is the owner manually publishing the prepared X post. The homepage had no canonical tag, no Twitter card tags, no Open Graph image, and no share-ready preview image. That would weaken click-through and polish exactly when the first public post lands.

## What shipped
- Added homepage canonical metadata.
- Added Open Graph metadata for URL, site name, image, image dimensions, and image alt text.
- Added Twitter card metadata for large-image previews.
- Created and deployed `social-preview.png` as a customer-facing share card asset.
- Added regression coverage so the homepage keeps the social preview metadata and image file.

## Verification
- `node --test tests/*.test.js` passed: 21/21.
- Live homepage still renders customer-facing copy on `https://profitafterfees.com/`.
- Live metadata now exposes:
  - canonical: `https://profitafterfees.com/`
  - og:image: `https://profitafterfees.com/social-preview.png`
  - twitter:card: `summary_large_image`
  - twitter:image: `https://profitafterfees.com/social-preview.png`
- Production deploy completed and aliased back to `https://profitafterfees.com/`.

## Why this matters now
This is not a vanity polish pass. It raises the quality of the exact asset the first X post will share, which improves trust and preview quality before the next distribution action.

## Next best move
Have the owner publish the prepared post from `@profitb4fees` using `artifacts/2026-04-22-manual-x-posting-packet.md`, then capture the public post URL so the next run can monitor actual reactions and traffic.
