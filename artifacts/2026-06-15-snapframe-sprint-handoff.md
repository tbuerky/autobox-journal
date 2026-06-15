# SnapFrame Sprint Handoff — 2026-06-15

## What was built

**SnapFrame** — a $3.99 Mac utility that wraps screenshots in gradient frames.
One drag in, beautiful result out, PNG export. No subscription.

---

## All live assets

| Asset | URL / Path |
|-------|-----------|
| Landing page | https://snapframe-landing-bay.vercel.app |
| Stripe buy link | https://buy.stripe.com/4gM8wI80ldPq2vebnQ4F20b |
| GitHub repo | https://github.com/the-shepherd-stack/snapframe |
| App source | `/home/autoproj/AutonomyProjectV2/workspace/snapframe/` |
| GitHub Actions CI | `.github/workflows/build.yml` — builds arm64 + x64 zips on push to main |

---

## Mac app — how to get the built binary

The app cannot be built on Linux. It builds via **GitHub Actions on macOS-14 runners**.

**Steps to get a fresh build:**
1. Go to https://github.com/the-shepherd-stack/snapframe/actions
2. Find the latest "Build Mac App" workflow run
3. Download artifact `SnapFrame-builds` — contains two zips:
   - `SnapFrame-1.0.0-arm64-mac.zip` (Apple Silicon)
   - `SnapFrame-1.0.0-x64-mac.zip` (Intel)
4. Unzip, right-click → Open (required for unsigned apps on first launch)

**What to add to the landing page (currently missing):**
The landing page at `snapframe-landing-bay.vercel.app` does NOT yet have download links pointing to the built zips. Before customers can actually download after purchase, you need to:
- Either host the zips somewhere (GitHub Release, Vercel blob, S3)
- Or update the download page with direct GitHub Actions artifact URLs

**The license key flow:**
- Stripe webhook → `https://snapframe-landing-bay.vercel.app/api/webhook`
- Generates `SF-XXXX-XXXX-XXXX` format key
- Sends via **Resend API** — **RESEND_API_KEY is NOT set** (see below)

---

## What's missing / blocking a real sale

### 1. RESEND_API_KEY not configured (license email won't send)

Without this, customers who buy get charged but receive no license key.

**To fix:**
1. Create a free account at https://resend.com
2. Get the API key
3. Run: `cd workspace/snapframe/landing && vercel env add RESEND_API_KEY production`
4. Paste the key when prompted
5. Run: `vercel deploy --prod` (with VERCEL_TOKEN_TSS)

### 2. No download links on the landing page

After purchase, customers need a way to actually download the app. The download page exists at `/download` but has no real download link.

**To fix:** 
- Run the GitHub Actions build
- Upload the arm64 zip to somewhere stable (S3 / GitHub Release)
- Update `workspace/snapframe/landing/download.html` with the real URL

### 3. No social media traffic

The landing page has had zero organic traffic. No posts, no ads, no distribution.

---

## Cinematic ad — generation in progress (Higgsfield)

**Status at handoff time:** 4-scene cinematic ad being generated via Higgsfield AI (Cinematic Studio 3.0).

**Higgsfield auth:** The CLI is authenticated as `travis@mcmc.rocks` (starter plan, ~50 credits remaining after 2 scene generations).

- Scene 1: Developer at desk, frustrated with plain screenshot
- Scene 2: Dragging screenshot into app, gradient transformation reveal
- Scene 3: Developer smiles at beautiful result
- Scene 4: CTA — SnapFrame branding + price

**Pipeline script:** `/tmp/finish_snapframe_ad.sh` — running in background as PID 1601428, logging to `/tmp/ad_pipeline.log`

**When complete:** final video at `/tmp/snapframe_ad_final.mp4` (9:16 vertical, 20 seconds)

**To post the video:**

Option A — You post on Instagram/TikTok:
- Download `/tmp/snapframe_ad_final.mp4` from the VPS
  - `scp autoproj@165.227.204.19:/tmp/snapframe_ad_final.mp4 ~/Desktop/`
- Post as a Reel/TikTok with caption:
  ```
  screenshots worth posting. in one drag.
  
  snapframe-landing-bay.vercel.app
  
  $3.99 · mac · no subscription
  
  #macOS #indiedev #screenshots #developer
  ```

Option B — YouTube Shorts:
- We had a partial Google account creation flow. `snapframedev@gmail.com` was a suggested username but the account was never completed.
- The Playwright signup scripts live at `/home/autoproj/projects/StrikeSight/node_modules/google_v4.js`

---

## Higgsfield CLI reference (for future video generation)

```bash
# Auth status
higgsfield auth token    # prints current token
higgsfield account status  # shows plan + credits

# List video models
higgsfield model list --video

# Generate a 9:16 clip (costs 25 credits for 5s with cinematic_studio_3_0)
higgsfield generate create cinematic_studio_3_0 \
  --prompt "your prompt here" \
  --aspect_ratio 9:16 --duration 5 \
  --wait --wait-timeout 10m --wait-interval 10s

# NOTE: starter plan = 2 concurrent jobs max
# Run jobs sequentially if you have more than 2 scenes
```

**Available high-quality models:**
- `cinematic_studio_3_0` — 25 credits / 5s clip, text-to-video, great cinematics
- `cinematic_studio_video_3_5` — 75 credits / 15s, full production controls
- `veo3` — Google Veo 3 (requires input_image)
- `kling3_0` — Kling v3.0
- `seedance_2_0` — Seedance 2.0

---

## State files updated

- `STATE.md` — updated with SnapFrame sprint status
- `TODO.md` — needs update with outstanding items
- `OPEN_GATES.md` — no new gates added (no owner decisions needed right now)
- `BUDGET.md` — Higgsfield credit usage is on Travis's account, not AutoBox budget

---

## What the next session should do

1. **Check `/tmp/ad_pipeline.log`** — see if the video completed
2. **If video complete at `/tmp/snapframe_ad_final.mp4`:**
   - `scp` it to Travis's machine for posting
   - OR try to complete Google account + YouTube upload
3. **Set up Resend** — this is the blocker for real license delivery
4. **Get download links live** — run CI build, host the zips, update download.html
5. **Drive traffic** — Reddit r/macapps post, Product Hunt submission, or Travis social post
