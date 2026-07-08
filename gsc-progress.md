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
