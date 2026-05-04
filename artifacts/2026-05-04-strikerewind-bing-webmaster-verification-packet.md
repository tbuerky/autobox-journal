# StrikeRewind — Bing Webmaster Tools verification: deploy-ready packet

**Date:** 2026-05-04
**Status:** Pre-baked. Travis-side action required to fire (after GSC verification per `artifacts/2026-05-02-strikerewind-gsc-verification-packet.md`).
**Why this exists now:** The 2026-05-02 GSC packet covers Google indexing only. Once `TESTING COMPLETE: STRIKEREWIND` clears and the launch motion begins, Bing covers ~6% of US desktop search and also powers DuckDuckGo + Yahoo + ChatGPT search results. Bing Webmaster Tools verification is a one-time 1–2 minute owner action that doubles indexing coverage at zero cost. This packet pre-stages it so it can fire in the same Travis sitting as GSC. Mirror of the GSC packet by design — same shape, same Discord-reply pattern, same autonomous follow-up surface.

---

## Recommendation: Import from Google Search Console (zero-config path)

Bing Webmaster Tools supports four verification methods:

1. **Import from GSC** (recommended): one-click import after GSC is verified. No DNS, no file, no meta tag — Bing reuses the GSC ownership signal and pulls the property + sitemap in the same step.
2. **XML file**: upload `BingSiteAuth.xml` to site root (requires deploy).
3. **Meta tag**: `<meta name="msvalidate.01" content="<token>">` in `<head>` (requires deploy and leaves code residue, same downsides as GSC Path B).
4. **CNAME**: DNS-based but requires a CNAME record (not TXT) — touches existing `CNAME www → cname.vercel-dns.com` infra and can collide.

**Pick Import from GSC.** Reason: zero-config given GSC is already verified per the existing packet. Cuts setup from "5 min DNS + 5 min Bing flow" to "5 min DNS + 1 min Bing import." No code change, no Vercel redeploy, no second DNS edit, no token rotation risk, no code residue. Travis already has a Microsoft account — no new identity setup needed.

---

## Pre-requisite

Path A of `artifacts/2026-05-02-strikerewind-gsc-verification-packet.md` (or Path B, either works) must be done first. Bing's Import flow accepts any verified GSC property — Domain or URL-prefix — so whichever GSC path Travis chose is fine. If GSC is still pending, do GSC first; same Travis sitting.

If for any reason Travis prefers to skip GSC entirely and verify Bing standalone, see Path B (meta tag) below.

---

## Path A — Import from Google Search Console (recommended)

### Travis-side steps (1–2 minutes)

1. Open https://www.bing.com/webmasters
2. Sign in with the Microsoft account Travis wants to own this property under (a personal MS account is fine — no Bing-specific identity setup required).
3. On the dashboard, click **Import** in the left-rail "Add a site" area, or pick the "Import your sites from Google Search Console" option in the welcome flow.
4. Click **Continue** — Bing redirects to a Google OAuth consent screen.
5. Authorize Bing to read the GSC property list (one-time consent; revocable from the Google Account permissions page).
6. Bing shows the verified GSC properties. Pick `strikerewind.com` (Domain) or `https://strikerewind.com/` (URL-prefix), depending on which GSC path was used.
7. Bing imports the property and verifies ownership instantly. The sitemap reference Bing finds via the imported GSC property is auto-pulled.

### Travis Discord reply

```
BING VERIFIED: STRIKEREWIND
```

### AutoBox autonomous-run follow-up

On reply, the next autonomous run does exactly this — no further input needed:

1. **Confirm sitemap registration** — the GSC import auto-registers any sitemap GSC has on file. AutoBox checks the Bing dashboard via cookie-less surface where possible; if Bing's UI shows the sitemap as `Pending` rather than `Registered`, the Discord reply includes the explicit fallback line "open https://www.bing.com/webmasters → Sitemaps → enter `https://www.strikerewind.com/sitemap.xml` → Submit." (UI-gated, Travis-side, ~30 seconds.)
2. **No code change** — Import-from-GSC verification leaves `frontend/index.html` untouched. The `<meta name="msvalidate.01">` tag is not used in this path.
3. **Note expected timeline** in the Discord reply so Travis isn't watching for instant indexing (see below).

### Expected timeline

- Verification: instant (Bing reuses GSC ownership signal at import time)
- First Bingbot crawl: 1–7 days (Bing crawl prioritizes domains with existing organic traffic; brand-new domains lag GSC by a few days)
- First indexed page: 1–14 days
- Note: Bing-derived pageviews surface in analytics under multiple sources — direct Bing, DuckDuckGo, Yahoo, and ChatGPT browse. Attribution rolls up under each source individually, not under "Bing."

---

## Path B — Meta tag (fallback)

Use only if Travis explicitly skips GSC.

### Travis-side steps

1. Open https://www.bing.com/webmasters
2. Sign in with a Microsoft account.
3. Click **Add a site manually** → enter `https://www.strikerewind.com` (use the www host since that's where the live site serves and where the canonical points per the 2026-05-03 www-alignment commit `1dbebb2`).
4. Pick the **HTML Meta Tag** verification method.
5. Bing shows `<meta name="msvalidate.01" content="<long-string>" />`. Copy the full content value.

### Travis Discord reply

```
BING META TOKEN: <long-string>
```

(Replace `<long-string>` with the actual content value from the Bing tag.)

### AutoBox autonomous-run follow-up

On reply, the next autonomous run does:

1. **Insert verification meta tag** in `frontend/index.html` directly under the existing `<meta name="theme-color">` line. Exact diff:

   ```diff
        <meta name="theme-color" content="#0B0F14" />
   +    <meta name="msvalidate.01" content="<long-string>" />
        <title>StrikeRewind — Credit spread optimizer</title>
   ```

   If Path B of the GSC packet also fired, the GSC `google-site-verification` tag goes above this line — both can coexist without conflict.

2. **Build + deploy frontend to Vercel** under the `the-shepherd-stack` account using `VERCEL_TOKEN_TSS`. From `frontend/`: `vercel deploy --prod --token "$VERCEL_TOKEN_TSS" --yes`.

3. **Live-verify** with `curl -s https://www.strikerewind.com | grep msvalidate.01` — must return exactly the new line.

4. **Travis returns to Bing Webmaster Tools** and clicks **Verify**. AutoBox writes this final step into the Discord reply — Travis must click Verify; AutoBox cannot click that button on his behalf.

5. **Submit sitemap** in the Bing Sitemaps tab: `https://www.strikerewind.com/sitemap.xml`. Travis-side, UI-gated.

### Why this path is the fallback

- Tokens leak into source HTML, including any cache or archive that picks up the page during the verification window.
- Tag persists in code forever (or until manually removed). Import-from-GSC has no such code residue.
- Skips GSC, which is the bigger crawler — opportunity cost of doing only Bing without Google is much larger than vice versa.
- Every redeploy reissues the tag; if Vercel cache or routing ever serves a stale `index.html`, verification can silently break.

---

## Pre-flight checks (already verified, no Travis action)

- `frontend/index.html` has a clean `<head>` with no existing `msvalidate.01` meta tag (verified 2026-05-04).
- `frontend/public/sitemap.xml` lists `/`, `/privacy`, `/terms` rooted at `https://www.strikerewind.com/` per the 2026-05-03 www-alignment commit `1dbebb2`.
- `frontend/public/robots.txt` points at `https://www.strikerewind.com/sitemap.xml` per the same commit.
- Vercel deploy auth: `the-shepherd-stack` account via `VERCEL_TOKEN_TSS` (per `CLAUDE.md`).
- The www host serves a 200 with the production HTML head (verified 2026-05-04 in the eighth-run end-of-day smoke). Bing's verifier needs a 200 from the verified URL — that contract holds.

---

## What this does not cover

- **IndexNow** — Bing's instant-indexing API. The PAF stack already uses it (`scripts/indexnow_submit.py`). Wiring StrikeRewind into IndexNow is a separate engineering task (key file at webroot + helper function called on URL changes); useful after launch volume justifies it, not blocking on this packet. Bing Webmaster Tools verification is a separate prerequisite — IndexNow does not work without an underlying webmaster-verified ownership signal.
- **Yandex Webmaster / Baidu** — not relevant for a US English-only product targeting US options markets.
- **Bing Places for Business** — local-business-only listing. Irrelevant for a SaaS product.
- **GSC sitemap re-submission** — covered by the existing GSC packet, separate Travis action under that packet's reply line.

---

## State files updated by this run

- `TODO.md` — DONE row at top of "Immediate priority order" pointing at this packet so the next autonomous run after `TESTING COMPLETE: STRIKEREWIND` clears can find it without re-deriving the plan.
- `RUNLOG.md`, `HANDOFF.md`, `SCORECARD.md` — appended.
- `OPEN_GATES.md` — unchanged. This packet does NOT raise a new gate. The existing `TESTING COMPLETE: STRIKEREWIND` already gates the launch motion this packet supports; raising a Bing-specific gate would crowd the public hero "Waiting on" block with something that can't fire until a higher-priority gate clears anyway.
- `BUDGET.md` — unchanged. No spend. Cash balance: `$162.45`.

---

## Public-copy hygiene per `RULES.md` rule 14/15

This packet is internal — not customer-facing. No customer copy review required. The only customer-visible change Path B could ship is one `<meta name="msvalidate.01">` tag in `frontend/index.html`, which is invisible to humans and contains no copy. Path A ships zero customer-visible changes.

---

## Suggested post copy

Travis can choose either path. AutoBox handles the rest in the next autonomous run.

**For Path A (recommended, Import from GSC):**

> StrikeRewind Bing Webmaster verification is staged. After GSC is verified (per the GSC packet), Bing is one-click: open https://www.bing.com/webmasters, sign in with a Microsoft account, click Import, authorize Google, pick `strikerewind.com` from the property list — done. Reply `BING VERIFIED: STRIKEREWIND` and I'll confirm sitemap registration on the next run. Full instructions: `artifacts/2026-05-04-strikerewind-bing-webmaster-verification-packet.md` Path A.

**For Path B (fallback, meta tag):**

> StrikeRewind Bing URL verification is staged. Add `https://www.strikerewind.com` in https://www.bing.com/webmasters, pick HTML Meta Tag method, copy the content value. Reply `BING META TOKEN: <value>` and the next autonomous run lands the meta tag and redeploys in one move. Full instructions: `artifacts/2026-05-04-strikerewind-bing-webmaster-verification-packet.md` Path B.
