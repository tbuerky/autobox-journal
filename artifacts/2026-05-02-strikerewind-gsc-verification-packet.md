# StrikeRewind — Google Search Console verification: deploy-ready packet

**Date:** 2026-05-02
**Status:** Pre-baked. Travis-side action required to fire.
**Why this exists now:** StrikeRewind deploy is gated on `CARD ADDED: RENDER WORKSPACE`. When that gate clears and the site goes live at `https://strikerewind.com`, indexing latency is the next thing that decides how fast the first organic visitor lands. A new domain on the open web with no GSC verification is invisible to Search until Google crawls it on its own schedule. With verification + sitemap submission, indexing is typically hours-to-days instead of weeks. This packet compresses that motion from a multi-message back-and-forth into "Travis pastes one token, AutoBox lands the change in one move."

---

## Recommendation: Domain property via DNS TXT record

Google Search Console supports two verification surfaces:

1. **Domain property** (recommended): `strikerewind.com`. Verified once via a DNS TXT record on the apex. Covers all subdomains (`api.strikerewind.com`, `www.strikerewind.com`) and both `http`/`https`. Travis controls the DNS at the registrar, not Vercel, so this is also independent of any frontend redeploy.
2. **URL-prefix property** (fallback): `https://strikerewind.com/`. Verified via a `<meta name="google-site-verification">` tag in the home page `<head>`. Only covers that exact protocol/host/path prefix.

**Pick Domain.** Reason: a Domain property keeps verification valid through future host-protocol-subdomain changes (we will eventually have `api.strikerewind.com` via Render, and Domain coverage avoids re-verifying that as a separate property). The URL-prefix path requires a frontend redeploy on every token rotation; the Domain path does not. The fallback path is documented below in case Travis prefers it for any reason.

---

## Path A — Domain property (recommended)

### Travis-side steps (5 minutes)

1. Open https://search.google.com/search-console
2. Click **Add property** → choose **Domain** (the left column, not URL-prefix)
3. Enter `strikerewind.com` (no `https://`, no path)
4. Google shows a verification token in the form: `google-site-verification=<long-random-string>`. The full string after the `=` is what gets pasted as the **TXT record value** at the registrar.
5. At Travis's domain registrar (the same place strikerewind.com is registered):
   - Add a TXT record
   - Host / Name: `@` (or leave blank, depending on registrar UI — means apex)
   - Value: `google-site-verification=<long-random-string>` (the entire string, including the `google-site-verification=` prefix — paste it verbatim)
   - TTL: default (3600 / 1 hour is fine)
6. Wait 5–10 minutes for DNS propagation, then click **Verify** in GSC.

### Travis Discord reply

```
GSC VERIFIED: STRIKEREWIND DOMAIN
```

### AutoBox autonomous-run follow-up

On reply, the next autonomous run does exactly this — no further input needed:

1. **Submit sitemap** at https://search.google.com/search-console — Sitemaps tab, enter `sitemap.xml`, click Submit. (The sitemap is already deployed at `https://strikerewind.com/sitemap.xml` per commit `6321576`.) **NOTE: This step is Travis-side too — the GSC sitemap-submit UI requires being logged in. AutoBox writes the exact instruction line into the Discord reply.**
2. **No code change needed.** Domain DNS verification leaves `frontend/index.html` untouched. The `<meta name="google-site-verification">` tag is not used in this path.
3. **Verify** the TXT record is live by running `dig TXT strikerewind.com +short` and confirming the `google-site-verification=...` line is in the response.

### Expected timeline

- Verification: instant (Google polls DNS the moment Travis clicks Verify, and DNS is normally hot within minutes)
- First crawl: usually within hours (Googlebot prioritizes newly-verified properties)
- First indexed page: usually within 1–3 days
- Full sitemap indexed: usually within a week

---

## Path B — URL-prefix property (fallback)

Use this only if Path A's DNS step is impractical for some reason.

### Travis-side steps

1. Open https://search.google.com/search-console
2. Click **Add property** → choose **URL prefix** (the right column)
3. Enter `https://strikerewind.com/`
4. Pick **HTML tag** verification method
5. Google shows a tag like `<meta name="google-site-verification" content="<long-random-string>" />`. Copy the **content value only** (the long random string).

### Travis Discord reply

```
GSC URL-PREFIX TOKEN: <long-random-string>
```

(Replace `<long-random-string>` with the actual content value from the GSC tag.)

### AutoBox autonomous-run follow-up

On reply, the next autonomous run does exactly this:

1. **Insert verification meta tag** in `frontend/index.html` directly under the existing `<meta name="theme-color">` line. Exact diff:

   ```diff
        <meta name="theme-color" content="#0B0F14" />
   +    <meta name="google-site-verification" content="<long-random-string>" />
        <title>StrikeRewind — Credit spread optimizer</title>
   ```

   Replace `<long-random-string>` with the value Travis pastes.

2. **Build + deploy frontend to Vercel** under the `the-shepherd-stack` account using `VERCEL_TOKEN_TSS`. The current Vercel deploy command shape is `vercel deploy --prod --token "$VERCEL_TOKEN_TSS"` from `frontend/` (the deploy architecture packet covers the broader Vercel setup; here we only need the redeploy to ship the new tag).

3. **Live-verify** with `curl -s https://strikerewind.com | grep google-site-verification` — must return exactly the new line.

4. **Travis returns to GSC** and clicks **Verify**. **AutoBox writes this final step into the Discord reply** — Travis must click Verify, AutoBox cannot click that button on his behalf.

5. **Submit sitemap** in GSC Sitemaps tab. Travis-side, same as Path A.

### Why this path is the fallback

- Tokens leak into source HTML, including any cache or archive that picked up the page during the verification window.
- Tag persists in code forever (or until manually removed). Domain DNS verification has no such code residue.
- Subdomains (`api.strikerewind.com`) require separate URL-prefix properties; Domain coverage handles all of them once.
- Every redeploy reissues the tag; if Vercel cache or routing ever serves a stale `index.html`, verification can silently break and no one notices until GSC stops returning data.

---

## Pre-flight checks (already verified, no Travis action)

- `frontend/index.html` exists and has a clean `<head>` with no existing `google-site-verification` meta tag (verified 2026-05-02).
- `frontend/public/sitemap.xml` exists and lists `/`, `/privacy`, `/terms` with correct `lastmod` dates (verified 2026-05-02).
- `frontend/public/robots.txt` exists and points at `https://strikerewind.com/sitemap.xml` (verified 2026-05-02).
- Vercel deploy auth path: `the-shepherd-stack` account via `VERCEL_TOKEN_TSS` (per `CLAUDE.md`).
- DNS for `strikerewind.com` is owned by Travis at the registrar; a separate TXT record does not conflict with the existing `A @ → 76.76.21.21` (Vercel) and `CNAME www → cname.vercel-dns.com` records that the deploy pipeline TODO step 5 calls out.

---

## What this does not cover

- **GSC sitemap submission** is Travis-side either way (UI-gated). Closest autonomous alternative would be the [Indexing API](https://developers.google.com/search/apis/indexing-api), which only works for `JobPosting` and `BroadcastEvent` schemas — not general pages — so it cannot replace the manual sitemap submit for StrikeRewind's landing/privacy/terms set.
- **Bing Webmaster Tools** equivalent verification is not in this packet. Bing has its own DNS verification flow; if/when StrikeRewind ranks for any term, AutoBox can prepare a parallel packet. Not worth the indirection while Google indexing is the only real organic surface that matters.
- **Google Analytics / GA4** — separate setup, separate verification surface. Out of scope here. AdSense (PAF) is also a separate verification on a separate property.

---

## State files updated by this run

- `TODO.md` — `[READY — POST-RENDER-DEPLOY]` line points at this packet so the next autonomous run after `CARD ADDED: RENDER WORKSPACE` clears can find it without re-deriving the plan.
- `RUNLOG.md`, `HANDOFF.md`, `SCORECARD.md` — appended.
- `OPEN_GATES.md` — unchanged. This packet does NOT raise a new gate; Travis already has the existing card-add gate in front of him, and the GSC verification step doesn't fire until after deploy. No reason to crowd the public hero "Waiting on" block with a gate that can't be acted on yet.
- `BUDGET.md` — unchanged. No spend. Cash balance: `$162.45`.

---

## Public-copy hygiene per `RULES.md` rule 14/15

This packet is internal — not customer-facing. No copy review required. The only customer-visible change either path could ship is one `<meta>` tag in `frontend/index.html` (Path B), which is invisible to humans and contains no copy.

---

## Suggested post copy

Travis can choose either path. AutoBox handles the rest in the next autonomous run.

**For Path A (recommended, DNS):**

> StrikeRewind GSC verification is staged. Add Domain property `strikerewind.com` in Search Console, paste the TXT record at the registrar (host `@`, value the full `google-site-verification=...` string), wait 5 min, click Verify. Reply `GSC VERIFIED: STRIKEREWIND DOMAIN` and I'll cover the sitemap submit step. Full instructions: `artifacts/2026-05-02-strikerewind-gsc-verification-packet.md` Path A.

**For Path B (fallback, meta tag):**

> StrikeRewind GSC URL-prefix verification is staged. Add `https://strikerewind.com/` as URL prefix in Search Console, pick HTML tag method, copy the content value. Reply `GSC URL-PREFIX TOKEN: <value>` and the next autonomous run lands the meta tag and redeploys in one move. Full instructions: `artifacts/2026-05-02-strikerewind-gsc-verification-packet.md` Path B.
