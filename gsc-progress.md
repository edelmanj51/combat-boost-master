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

## 2026-07-08 05:40 UTC — deep-dive on 4 sites (Crestview, Dublin, Moore's, Saga)
Joe scoped out kick-start / american-colleges / gmwons / camal / champion (not live — skip).
Investigated the remaining 4. **Two are NOT actually blocked — they're already live on www.**

- **Crestview — TRULY BLOCKED (DNS not pointed).** Our build is live & correct at
  `crestview-ata.pages.dev`. But `kickwithata.com` (apex + www) resolves to `72.52.145.122`
  (Apache) = the OLD ATA corporate site ("Learn Martial Arts in Niceville… | ATA Martial Arts"),
  nameservers still `dojoservers.com` (ATA's vendor). You own the domain, but its DNS is still
  delegated to ATA's platform, so it serves their site. **Fix:** point `kickwithata.com` at the
  `crestview-ata` Pages project (move NS to Cloudflare, or add records at current DNS).

- **Dublin — TRULY BLOCKED (domain parked, never pointed).** Build live & correct at
  `dublin-ata.pages.dev`. `dublinata.com` (apex + www) resolves to `208.91.197.27` (openresty,
  "403 Forbidden") = a registrar parking/default page via Domain.com nameservers. Domain was
  never pointed at the Pages project. **Fix:** configure DNS at Domain.com (or move to
  Cloudflare) → `dublin-ata` Pages project.

- **Moore's — NOT BLOCKED. Live on www.** `www.mooreskaratelodi.com` is CNAME→
  `moores-karate.pages.dev`, Cloudflare-served, our clean build (12 markers, no token leaks).
  Earlier "blocked" was a false alarm — I'd only probed the apex, which is dead (`64.90.49.155`,
  DreamHost default, no site). Only defect: apex doesn't redirect to www. Repo is INCOMPLETE
  (missing `client-data.yaml` + `qc.js`) so a rebuild isn't clean → verify via **DNS-TXT at
  DreamHost** (Domain property covers www; no repo work).

- **Saga — NOT BLOCKED. Live on www.** `www.sagataekwondo.com` is CNAME→
  `saga-taekwondo.pages.dev`, Cloudflare-served, our clean build (9 markers, no leaks). Apex
  `sagataekwondo.com` points to `192.0.2.1` (RFC-5737 documentation IP — a non-routable
  placeholder) = dead. DNS is on Wix. Also a canonical bug: site's canonical says apex
  `sagataekwondo.com` but the live site is www. Verify via **meta-tag token** (saga repo is
  complete, agoge-style) OR DNS-TXT at Wix. Fix canonical → www on next rebuild.

**Need from Joe:** Decide next move — (a) verify Moore's + Saga now (they're ready), and/or
(b) start repointing DNS for Crestview + Dublin (registrar/DNS action on domains you own).
**Values to copy:** none.

## 2026-07-08 05:43 UTC — starting Crestview + Dublin DNS repoint
Plan: move each domain's nameservers to Cloudflare, attach to its Pages project, then verify in
GSC via DNS-TXT (same as the other Cloudflare-DNS sites). Chose NS-move over a CNAME-at-current-
host because (1) Crestview's DNS is delegated to ATA's vendor `dojoservers.com` (Joe likely can't
edit records there — only NS at the registrar), (2) it covers apex + www, (3) it unlocks the easy
DNS-TXT verification. Pages builds are already live & correct at `crestview-ata.pages.dev` and
`dublin-ata.pages.dev`, so sites go live the moment DNS points there.

⚠️ SAFETY CHECK FIRST: moving NS moves ALL DNS. If either domain receives email (MX), we must copy
those records into Cloudflare or email breaks. Dublin = parked (low risk). Crestview = may have
ATA email. **Waiting on Joe to confirm whether either domain receives email before switching NS.**

**Need from Joe (browser) — do these steps PER domain (start both; propagation is the slow part):**
  Use the SAME Cloudflare account that hosts the Pages projects.
  1. Cloudflare → **Add a site** → enter the domain (`kickwithata.com` / `dublinata.com`) → Free plan.
  2. Cloudflare auto-scans existing DNS → **review the imported records** (keep MX/email, TXT/SPF,
     any subdomains). Tell me what it lists if unsure.
  3. Cloudflare shows **2 nameservers** (e.g. `x.ns.cloudflare.com`). At your **registrar**, replace
     the current nameservers:
       - kickwithata.com: currently `ns1/ns2.dojoservers.com` → replace with Cloudflare's.
       - dublinata.com: currently `ns1/ns2.domain.com` → replace with Cloudflare's.
  4. Wait for Cloudflare to email "active" (minutes–24h).
  5. Pages project (`crestview-ata` / `dublin-ata`) → **Custom domains** → **Set up a domain** →
     add both the apex and `www`. Cloudflare auto-creates the records.
  6. Confirm the domain loads OUR build; relay back → then I'll give the GSC DNS-TXT step.
**Values to copy:** Cloudflare will show the 2 nameservers per domain (you enter those at the
registrar). Relay them back if you want me to sanity-check.

## 2026-07-08 06:00 UTC — re-verified live state; correction on Dublin's email risk
Re-ran live DNS/HTTP checks on all 4 (Crestview, Dublin, Moore's, Saga) before resuming — nothing
had drifted since the last session except one important correction:

- **Crestview (`kickwithata.com`) — still truly blocked.** NS still `dojoservers.com`, apex still
  Apache/ATA's site. **Has an active MX record: `mx.ipage.com`.** Confirms the earlier flag — this
  domain receives email and MX must be copied into Cloudflare before any NS switch.
- **Dublin (`dublinata.com`) — still truly blocked, but the "low risk / parked" call was WRONG.**
  NS still `domain.com`, apex still openresty/403. It DOES have an active MX record —
  **`smtp.google.com` (Google Workspace)** — meaning someone currently receives email at this
  domain. Previous session assumed "parked = low risk" without actually checking MX; that was an
  error. Treat Dublin the same as Crestview: **do not move nameservers until the Google Workspace
  MX/TXT (SPF/DKIM) records are captured and re-created in Cloudflare**, or mail will start
  bouncing/silently dropping immediately on cutover.
- **Moore's — reconfirmed NOT blocked.** `www.mooreskaratelodi.com` → CNAME `moores-karate.pages.dev`,
  `server: cloudflare`, still serving our build. Ready for GSC now (Domain property, DNS-TXT at
  DreamHost — covers www since GSC Domain properties match all hosts).
- **Saga — reconfirmed NOT blocked.** `www.sagataekwondo.com` → CNAME `saga-taekwondo.pages.dev`,
  `server: cloudflare`, still serving our build. Ready for GSC now (meta-tag token, repo is clean —
  or DNS-TXT at Wix if Joe prefers Domain property).

Updated `gsc-setup-handoff.md` TL;DR + per-site table to move Moore's/Saga out of "blocked" into
"ready" (they were miscategorized as blocked from the very first pass, before the deep-dive
corrected it — table just hadn't been synced).

**Need from Joe — two independent decisions, can go in parallel:**
1. **Moore's + Saga:** want me to proceed with GSC verification now? For Moore's I'd give you the
   DNS-TXT steps (DreamHost). For Saga, your call: meta-tag token (I push a 3-line diff to the
   `saga-taekwondo` repo, same low-risk pattern as agoge, needs your push approval) or DNS-TXT at
   Wix (no repo change, but Wix's DNS UI can be finicky — your call which you'd rather do).
2. **Crestview + Dublin DNS repoint:** before touching either domain's nameservers, I need the
   current MX/SPF/DKIM records preserved. Two options:
   - You paste me whatever you can see in each domain's current DNS panel (dojoservers.com for
     Crestview, domain.com for Dublin) and I'll build the Cloudflare-side records to match before
     you flip NS.
   - Or, safer/slower: at each *current* DNS host, just add a CNAME (or A record, if that host
     doesn't support CNAME at apex) pointing the site to the Pages project directly — no NS move,
     no email risk at all, since MX stays untouched at the original host. This is more manual
     per-registrar work but sidesteps the email risk entirely. Given both domains have live email,
     I'd lean toward this option unless you want DNS fully consolidated onto Cloudflare anyway.
**Values to copy:** none yet — waiting on your call on both items above.

## 2026-07-08 06:05 UTC — Joe's decisions
**Done:** Joe decided: (1) proceed with Moore's + Saga verification now. (2) Crestview + Dublin
DNS repoint — **not yet**, holding off (email-risk domains, no rush). Leaving those two BLOCKED
until Joe says go.
**Need from Joe:** Moore's GSC steps below (Domain property, DreamHost DNS-TXT). Saga's method
(meta-tag repo push vs DNS-TXT at Wix) still needs Joe's pick — asking next.
**Values to copy:** none yet.

## 2026-07-08 06:08 UTC — Moore's + Saga kickoff
**Done:** Joe picked meta-tag for Saga (agoge-style repo push).
**Need from Joe (two independent things, do in either order):**

**A. Moore's — Domain property via DreamHost DNS-TXT:**
  1. GSC → Add property → **Domain** box → enter `mooreskaratelodi.com` (no https/www/slash) → Continue.
  2. Copy the TXT value Google shows (`google-site-verification=...`).
  3. DreamHost → domain's DNS panel → Add record: Type **TXT**, Name **@** (or blank/root,
     DreamHost's UI varies), Content = the value, TTL default → Save.
  4. Back in GSC → **Verify** (retry after ~5–30 min if it fails — DreamHost DNS can be slower to
     propagate than Cloudflare).
  Relay back: verified or error.

**B. Saga — phase 1 (browser, get the content value):**
  1. GSC → Add property → **URL prefix** box (NOT Domain) → enter exactly
     `https://www.sagataekwondo.com` (must be www — that's what's actually live; the site's own
     canonical tag wrongly says apex, ignore it) → Continue.
  2. In the methods list choose **HTML tag**.
  3. Google shows `<meta name="google-site-verification" content="XXXX" />`. Copy ONLY the
     `XXXX` content value and relay it to me.
  4. **Do NOT click Verify yet** — same as agoge, I need to build the tag into the repo, get your
     push approval, and confirm it's live first.
  Then I do phase 2 (wire token into saga-taekwondo repo, rebuild, qc.js, show diff for approval)
  and phase 3 (confirm live post-push, then you click Verify).
**Values to copy:** Moore's TXT value (if it fails) + Saga's `google-site-verification` content value.

## 2026-07-08 06:15 UTC — Saga phase 2 complete
**Done:** Joe supplied Saga's verification content value. Wired `GSC_VERIFICATION` into
`saga-taekwondo` repo (added the IF-block token to source `index.html`, set the value in
`client-data.yaml`), rebuilt, ran `qc.js` → **17/17 PASSED**. Diff is exactly 3 lines (source
token, client-data value, dist meta tag) — same minimal pattern as agoge. No visual change
(head-only tag), so no screenshot needed — verified instead via qc.js output (no token leaks,
school name present, all URLs/images valid).
**Need from Joe:** **Approve the push of the `saga-taekwondo` repo.** Reply "approved" (or push
it yourself). After push → Cloudflare redeploys → I'll confirm the tag is live at
`https://www.sagataekwondo.com` → then you click **Verify** in GSC for that URL-prefix property.
**Values to copy:** none.

## 2026-07-08 06:25 UTC — Saga pushed and live
**Done:** ✅ Joe approved + pushed (`saga-taekwondo` commit `88e2313`). Cloudflare redeployed;
confirmed the verification meta tag is **LIVE** at https://www.sagataekwondo.com.
**Need from Joe:** Go to the GSC `https://www.sagataekwondo.com` **URL-prefix** property and click
**Verify** now. Relay back: verified or error. Separately, Moore's DNS-TXT steps are still pending
whenever Joe's ready for those (Domain property, DreamHost) — see the 06:08 UTC entry above.
**Values to copy:** none.

## 2026-07-08 06:30 UTC — Moore's verified
**Done:** ✅ **moores-karate verified** (`mooreskaratelodi.com`, Domain property via DreamHost
DNS-TXT). **8 sites now verified & collecting GSC data:**
  1. up-top-ma — uptopmartialarts.com (Domain / Cloudflare TXT)
  2. tiger-paw-ma — tigerpawma.com (Domain / Cloudflare TXT)
  3. north-georgia-martial-arts — northgeorgiamartialarts.com (Domain / Cloudflare TXT)
  4. ramires-ata — ramiresatabba.com (Domain / Cloudflare TXT)
  5. shorin-ryu-karate-palestine — shorinryuwakidokai.com (Domain / Cloudflare TXT)
  6. agoge-krav-maga — www.agogekm.com (URL-prefix / meta tag)
  7. saga-taekwondo — www.sagataekwondo.com (URL-prefix / meta tag)
  8. moores-karate — mooreskaratelodi.com (Domain / DreamHost TXT)
**Need from Joe:** Nothing right now on the ready pool — all 8 sites that actually serve our
build are verified. Remaining workstream is the 7 truly blocked sites (domain doesn't serve our
build yet): crestview-ata, dublin-ata, kick-start-ma-atlanta,
aamerican-colleges-jiu-jitsu-karate-henrico, grand-master-wons-taekwondo-oklahoma-city,
camal-and-cruz, champion-sport-karate-papillion. Of those, only Crestview + Dublin are in scope
(the other 5 aren't live yet per Joe). Crestview + Dublin are on hold per Joe's call (both have
active email — Crestview: mx.ipage.com, Dublin: Google Workspace — repointing needs MX preserved
first). Say the word when ready to revisit.
**Values to copy:** none.

## 2026-07-08 06:40 UTC — Crestview + Dublin DNS repoint, GO
**Done:** Joe corrected the record — he personally owns both `kickwithata.com` and
`dublinata.com` (not client domains), and the email on them is his own or irrelevant. Prior
email-risk hold is lifted. Joe chose **move NS to Cloudflare** (cleanest, unlocks DNS-TXT
verification, consolidates management) over CNAME-at-current-host.
**Need from Joe (browser) — do these steps PER domain, can start both in parallel:**
  Use the SAME Cloudflare account that hosts the Pages projects.
  1. Cloudflare dashboard → **Add a site** → enter the domain (`kickwithata.com` first pass,
     then `dublinata.com`) → Free plan.
  2. Cloudflare auto-scans existing DNS records → **review what it imported** (it'll list the
     current A/MX/TXT records it found at dojoservers.com / domain.com). Since email doesn't
     matter here, no need to double check MX — just glance for anything obviously missing, then
     continue.
  3. Cloudflare shows **2 nameservers** to use (e.g. `x.ns.cloudflare.com`, `y.ns.cloudflare.com`
     — exact values are unique per domain, Cloudflare generates them on this step).
  4. Go to your **registrar** for each domain and replace the current nameservers:
     - `kickwithata.com`: currently `ns1.dojoservers.com` / `ns2.dojoservers.com` → replace with
       the 2 Cloudflare ones from step 3.
     - `dublinata.com`: currently `ns1.domain.com` / `ns2.domain.com` → replace with the 2
       Cloudflare ones from step 3.
  5. Wait for Cloudflare to email "site is now active" (usually minutes, can take up to 24h for
     full propagation).
  6. In Cloudflare, open the Pages project (`crestview-ata` for kickwithata.com, `dublin-ata` for
     dublinata.com) → **Custom domains** tab → **Set up a domain** → add both the apex
     (`kickwithata.com`) and `www.kickwithata.com` (same pattern for dublinata.com). Cloudflare
     auto-creates the DNS records once the zone is active.
  7. Confirm the domain now loads OUR build (school name should be correct, no ATA/old-site
     branding) — relay back once you see it, and I'll do a `server: cloudflare` + title check
     from here too.
  Then (my side): once confirmed live, I give you the DNS-TXT GSC verification steps for both
  (same pattern as up-top-ma/tiger-paw/etc — Domain property, TXT record at Cloudflare, since
  DNS is now on Cloudflare for both).
**Values to copy:** the 2 Cloudflare nameservers per domain (paste back if you want me to
sanity-check before you update the registrar).
