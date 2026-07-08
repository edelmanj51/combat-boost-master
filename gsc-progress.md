# GSC rollout — shared progress

Shared state for the GSC setup. **Coordinator Claude** reads this from GitHub; **server-side
Claude** appends an entry after every step that needs Joe's input. Full findings + per-site
routing table live server-side in `gsc-setup-handoff.md` (ask if you want it pushed here too).

Newest entry at the bottom.

---

## 2026-07-08 04:56 UTC
**Done:** Investigation complete (15 sites: 5 ready, 2 uncertain, 8 blocked because the custom
domain still serves the client's OLD site). Wired + tested the `GSC_VERIFICATION` meta-tag token
into the v5 template. Set up this shared progress file + auto-push. Starting rollout with the 4
Option-A sites (DNS on Cloudflare → robust DNS-TXT Domain property).
**Need from Joe:** Verify **up-top-ma** in GSC as a **Domain property**, using your ONE agency
Google account.
  1. GSC → Add property → **Domain** box → enter `uptopmartialarts.com` (no https, no www, no
     slash) → Continue.
  2. Copy the TXT value Google shows (`google-site-verification=...`).
  3. Cloudflare → select `uptopmartialarts.com` → DNS → Add record: Type **TXT**, Name **@**,
     Content = the value, TTL Auto → Save.
  4. Back in GSC → **Verify** (retry after ~5 min if it fails).
  Then relay back: the exact TXT value used + whether it said Verified or an error.
**Values to copy:** (none from me yet — Google generates the TXT value; paste it back here.)

## 2026-07-08 05:04 UTC
**Done:** ✅ **up-top-ma verified** (`uptopmartialarts.com`, Domain property via Cloudflare TXT).
1 of 4 Option-A sites done. Sitemap submission for it is queued for after all 4 are verified.
**Need from Joe:** Verify the next Option-A site, **tiger-paw-ma**, same steps (DNS-only, so its
missing local build doesn't matter here):
  1. GSC → Add property → **Domain** box → enter `tigerpawma.com` (no https, no www, no slash) → Continue.
  2. Copy the TXT value Google shows (`google-site-verification=...`).
  3. Cloudflare → select `tigerpawma.com` → DNS → Add record: Type **TXT**, Name **@**,
     Content = the value, TTL Auto → Save.
  4. Back in GSC → **Verify** (retry after ~5 min if it fails).
  Relay back: verified or error.
**Values to copy:** (Google generates the TXT value; paste it back if anything fails.)

## 2026-07-08 05:06 UTC
**Done:** ✅ **tiger-paw-ma verified** (`tigerpawma.com`, Domain property via Cloudflare TXT).
2 of 4 Option-A sites done.
**Need from Joe:** Verify the next Option-A site, **north-georgia-martial-arts**, same steps:
  1. GSC → Add property → **Domain** box → enter `northgeorgiamartialarts.com` (no https, no www, no slash) → Continue.
  2. Copy the TXT value Google shows (`google-site-verification=...`).
  3. Cloudflare → select `northgeorgiamartialarts.com` → DNS → Add record: Type **TXT**, Name **@**,
     Content = the value, TTL Auto → Save.
  4. Back in GSC → **Verify** (retry after ~5 min if it fails).
  Relay back: verified or error.
**Values to copy:** (Google generates the TXT value; paste it back if anything fails.)

## 2026-07-08 05:10 UTC
**Done:** ✅ **All 4 Option-A sites verified** (up-top-ma, tiger-paw-ma, north-georgia,
ramires-ata) as GSC Domain properties. 🎉 They are now collecting data — no sitemap needed for
that. BUT sitemap submission is **blocked**: none of the 4 actually serve a sitemap
(`dist/sitemap.xml` missing on all; live sites return homepage HTML + 200 for any unknown path,
which GSC rejects as invalid). The build does NOT generate sitemaps — they'd have to be created,
committed, and pushed per client repo (needs qc.js + per-push approval; tiger-paw has no local
build at all).
**Need from Joe:** Decide how to handle sitemaps (see options below). Nothing to do in the
browser right now — the 4 properties are live and collecting.
  - Option A (recommended): skip sitemaps for now; data flows regardless. Revisit later.
  - Option B: I generate sitemap.xml + robots.txt for all 4, run QC, and show you for approval
    to push; then you submit `/sitemap.xml` in each GSC property.
  - Also pending: 2 uncertain sites (shorin, champion) + 8 blocked sites (domain still serves
    old site). Those are separate workstreams when ready.
**Values to copy:** none.

## 2026-07-08 05:13 UTC
**Done:** Sitemaps = SKIP for now (Joe's call). Resolved the 2 uncertain sites:
  - ✅ **shorin-ryu** (`shorinryuwakidokai.com`) IS our build (cloudflare server + our template
    markers, Cloudflare DNS) → **ready, Option A**. Flag: its live page has an EMPTY `<title>`
    (SEO bug — fix on next rebuild; does not block GSC).
  - ❌ **champion** (`championsportkarate.com`) is NOT our build (different 138 KB site proxied
    via Cloudflare) → **moved to BLOCKED** (domain must be pointed at the Pages project).
  Ready pool now: 4 verified + shorin-ryu (A) + agoge (B).
**Need from Joe:** Verify **shorin-ryu** as a Domain property, same steps as the others:
  1. GSC → Add property → **Domain** box → enter `shorinryuwakidokai.com` (no https/www/slash) → Continue.
  2. Copy the TXT value (`google-site-verification=...`).
  3. Cloudflare → select `shorinryuwakidokai.com` → DNS → Add record: Type **TXT**, Name **@**,
     Content = the value, TTL Auto → Save.
  4. Back in GSC → **Verify** (retry after ~5 min if it fails).
  Relay back: verified or error. (After this, agoge is the last ready site — Option B/meta tag,
  which needs a client-repo push + approval; I'll lay out its steps then.)
**Values to copy:** none from me — Google generates the TXT value.

## 2026-07-08 05:25 UTC
**Done:** ✅ **shorin-ryu verified** (`shorinryuwakidokai.com`, Domain property). **5 sites now
verified & collecting** (up-top, tiger-paw, north-georgia, ramires, shorin). Confirmed agoge
builds clean + `qc.js` PASSES (17 checks), so its meta-tag push will be low-risk. Starting agoge
(Option B — HTML meta tag). Its canonical is `https://www.agogekm.com`.
**Need from Joe (agoge, phase 1 — browser):**
  1. GSC → Add property → **URL prefix** box (the RIGHT box, NOT Domain) → enter exactly
     `https://www.agogekm.com` → Continue.
  2. In the methods list choose **HTML tag**.
  3. Google shows `<meta name="google-site-verification" content="XXXX" />`. Copy ONLY the
     content value (the `XXXX`) and relay it to me.
  4. **Do NOT click Verify yet** — the tag isn't live until I build it in + you approve the push
     + Cloudflare redeploys. I'll tell you when to click Verify.
  Then (phase 2, me): I wire the token into agoge's repo, set the value, rebuild, run qc.js,
  screenshot review, and show you for approval to push. (phase 3): after push + redeploy I
  confirm the tag is live, then you click Verify.
**Values to copy:** Joe brings back agoge's `google-site-verification` content value.

## 2026-07-08 05:28 UTC
**Done:** Agoge phase 2 complete. Wired the `GSC_VERIFICATION` token into agoge's repo, set the
value (`PIRSNroKr...YGx8`), rebuilt, ran `qc.js` → **17/17 PASSED**. Diff is exactly 3 lines
(source index.html token, client-data.yaml value, dist/index.html meta tag) — nothing else
changed. No visual/screenshot review needed (head-only meta tag, zero rendered change);
verified instead that the diff contains only the tag, school name present, no token leaks.
**Need from Joe:** **Approve the push of the `agoge-krav-maga` client repo** (client-repo pushes
need explicit approval). Reply "approved" (or push it yourself). After I push → Cloudflare
redeploys → I confirm the tag is live at https://www.agogekm.com → THEN you click **Verify** in
GSC for the `https://www.agogekm.com` URL-prefix property.
**Values to copy:** none.

## 2026-07-08 05:29 UTC
**Done:** ✅ Agoge approved + pushed (`agoge-krav-maga` commit `d2fb30b`). Cloudflare redeployed;
confirmed the verification meta tag is **LIVE** at https://www.agogekm.com (~60s after push).
**Need from Joe:** Go back to the GSC `https://www.agogekm.com` **URL-prefix** property and click
**Verify** now. Relay back: verified or error.
**Values to copy:** none.

## 2026-07-08 05:31 UTC — MILESTONE: all ready sites verified 🎉
**Done:** ✅ **agoge-krav-maga verified** (`https://www.agogekm.com`, URL-prefix, HTML meta tag).
**All 6 ready sites are now verified and collecting GSC data:**
  1. up-top-ma — uptopmartialarts.com (Domain / Cloudflare TXT)
  2. tiger-paw-ma — tigerpawma.com (Domain / Cloudflare TXT)
  3. north-georgia-martial-arts — northgeorgiamartialarts.com (Domain / Cloudflare TXT)
  4. ramires-ata — ramiresatabba.com (Domain / Cloudflare TXT)
  5. shorin-ryu-karate-palestine — shorinryuwakidokai.com (Domain / Cloudflare TXT)
  6. agoge-krav-maga — www.agogekm.com (URL-prefix / meta tag)
**Need from Joe:** Nothing right now — phase 1 (all sites already serving our build) is DONE.
When ready, next workstream is the **9 blocked sites** (custom domain still serves the client's
OLD site — must be pointed at the Cloudflare Pages project before GSC is meaningful):
crestview, dublin, moores, saga, kick-start, american-colleges, gmwons, camal-and-cruz, champion.
**Values to copy:** none.

### Notes / carry-forward
- Data lag: GSC has ~2-day lag and NO backfill — data accrues from each verification date forward.
- Sitemaps: intentionally skipped (not required for data). Build does not generate them.
- SEO bug to fix on next rebuild: shorin-ryu's live homepage has an EMPTY `<title>`.
- `GSC_VERIFICATION` token now lives in the v5 template AND agoge's repo → future meta-tag
  verifications are a one-line `client-data.yaml` change.
