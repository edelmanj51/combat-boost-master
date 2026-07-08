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
