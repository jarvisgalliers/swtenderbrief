# swtenderbrief.co.uk — static landing site

Plain static site for **South-West Tender Brief** (`v-2026-05-09-tenderradarsw`). No build step, no JS framework, no trackers. Hosted on **GitHub Pages** from the repo `jarvisgalliers/swtenderbrief` (custom domain `swtenderbrief.co.uk`).

## Files
- `index.html` — landing page (based on `../drafts/2026-05-10-landing-page-copy.md`; AI / Jarvis-Galliers wording removed per Freddie — decision #93)
- `terms.html`, `refund.html`, `privacy.html` — legal pages (based on `../drafts/2026-05-10-*.md`); finalised — ICO ref ZA734883, controller "Frederick Leatham, trading as Jarvis Galliers, sole trader, Reading, Berkshire", dated 12 May 2026, no AI wording. (Plain-language drafts, not solicitor-reviewed.)
- `404.html` (keeps `noindex` deliberately), `style.css`, `.nojekyll`, `CNAME` (`swtenderbrief.co.uk`)

## Status — LIVE (2026-05-12)
- **HTTPS** live (Let's Encrypt cert, http→https enforced). Indexable (no `noindex` on content pages).
- **Stripe: LIVE.** `index.html` has the real "Get the weekly brief — £89/year" buttons → live Payment Link `https://buy.stripe.com/5kQ5kFa0z4uFeQqbUv2B200`. (Verify in the Stripe dashboard that this live link still carries the `main_trade` / `other_trades` / `postcode_areas` custom fields the test link had — `subscribers.py reconcile` needs them.)
- **Remaining:**
  1. **Welcome emails don't send yet** — `secrets/stripe.txt` needs a `live_secret:sk_live_…` (or restricted `rk_live_…`) so the hourly `Jarvis-TenderRadarSW-Subscribers` task's `reconcile` sees real subscribers. `SWTENDERBRIEF_ALLOW_SEND` / `_ALLOW_LIVE` are already set.
  2. The free monthly tier isn't live (needs outbound sending wired). The page's free-tier CTA is an `mailto:` "tell me when it opens".
  3. The weekly `send-digest --send` isn't scheduled yet (needs a send day/time + the curation pipeline producing `curator_decision=include` tenders).
  4. The Resend welcome/digest email templates may still contain AI wording — not yet aligned with the site.

## Deploying
The repo `jarvisgalliers/swtenderbrief` is a deploy mirror of this directory. Auth: SSH key `~/.ssh/id_ed25519_jarvisgalliers` via the `github-jg` Host alias (see decision #89). To push an update from a clone:
```
git -C <clone> rm -r --quiet . ; cp -r <this-dir>/. <clone>/ ; git -C <clone> add -A
git -C <clone> commit -m "site: <what changed>" ; git -C <clone> push origin main
```
GitHub Pages: Settings → Pages → "Deploy from a branch" = `main` / `/ (root)`; custom domain `swtenderbrief.co.uk`; "Enforce HTTPS" on. DNS for the apex is on Porkbun (decision #29): four `A` records to GitHub's Pages IPs + a `www` `CNAME` to `jarvisgalliers.github.io`.
