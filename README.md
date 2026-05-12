# swtenderbrief.co.uk — static landing site

Plain static site for **South-West Tender Brief** (`v-2026-05-09-tenderradarsw`). No build step, no JS framework, no trackers. Hosted on **GitHub Pages** from the repo `jarvisgalliers/swtenderbrief` (custom domain `swtenderbrief.co.uk`).

## Files
- `index.html` — landing page (copy from `../drafts/2026-05-10-landing-page-copy.md`)
- `terms.html`, `refund.html`, `privacy.html` — legal pages (from `../drafts/2026-05-10-*.md`) — **DRAFT**, see below
- `404.html`, `style.css`, `.nojekyll`, `CNAME` (`swtenderbrief.co.uk`)

## Status — paid tier LIVE (2026-05-12); not fully launch-clean yet
- **Stripe: LIVE.** `index.html` has the real "Get the weekly brief — £89/year" buttons pointing at the live Payment Link `https://buy.stripe.com/5kQ5kFa0z4uFeQqbUv2B200`. (Verify in the Stripe dashboard that this live link still carries the `main_trade` / `other_trades` / `postcode_areas` custom fields the test link had — `subscribers.py reconcile` needs them.)
- **Still outstanding before it's fully clean:**
  1. **Legal pages have placeholders** — `[TOWN/COUNTY]`, `[DATE OF PUBLICATION]`, and the ICO registration reference `ZA######` (fee paid 2026-05-11; Freddie to supply the number). Fill these and remove the "Draft — pre-launch" banners. Stripe's ToS requires live terms/refund/privacy while taking payment.
  2. **Outbound email sending** for the swtenderbrief domain isn't enabled yet — so a new subscriber pays but the welcome email + first digest won't actually send until `SWTENDERBRIEF_ALLOW_SEND=1` is set and the path is run. Enable this ASAP.
  3. The free monthly tier isn't live (needs #2). The page's free-tier CTA is an `mailto:` "tell me when it opens".
  4. `<meta name="robots" content="noindex">` is still on `index.html` — flip it once the legal pages are finalised.
  5. Freddie should read the legal pages line-by-line (and consider a quick paid legal check).

## Deploying
The repo `jarvisgalliers/swtenderbrief` is a deploy mirror of this directory. Auth: SSH key `~/.ssh/id_ed25519_jarvisgalliers` via the `github-jg` Host alias (see decision #89). To push an update from a clone:
```
git -C <clone> rm -r --quiet . ; cp -r <this-dir>/. <clone>/ ; git -C <clone> add -A
git -C <clone> commit -m "site: <what changed>" ; git -C <clone> push origin main
```
GitHub Pages: Settings → Pages → "Deploy from a branch" = `main` / `/ (root)`; custom domain `swtenderbrief.co.uk`; "Enforce HTTPS" on. DNS for the apex is on Porkbun (decision #29): four `A` records to GitHub's Pages IPs + a `www` `CNAME` to `jarvisgalliers.github.io`.
