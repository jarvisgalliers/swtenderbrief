# swtenderbrief.co.uk — static landing site

Plain static site for **South-West Tender Brief** (`v-2026-05-09-tenderradarsw`). No build step, no JS framework, no trackers. Hosted on **GitHub Pages** from the repo `jarvisgalliers/swtenderbrief` (custom domain `swtenderbrief.co.uk`).

## Files
- `index.html` — landing page (copy from `../drafts/2026-05-10-landing-page-copy.md`)
- `terms.html`, `refund.html`, `privacy.html` — legal pages (from `../drafts/2026-05-10-*.md`) — **DRAFT**, see below
- `404.html`, `style.css`, `.nojekyll`, `CNAME` (`swtenderbrief.co.uk`)

## Status — this is a PRE-LAUNCH PREVIEW, not the live product yet
Before this should be treated as a real, launched, transacting site:
1. **Stripe** is still in TEST mode — recreate the product/prices/payment-link in LIVE mode, then add the real "subscribe" buttons (the live Payment Link) to `index.html`. Right now the page only has "email me when it launches" CTAs and a pre-launch banner — deliberately, so nobody hits a test checkout.
2. **Legal pages have placeholders** — `[TOWN/COUNTY]`, `[DATE OF PUBLICATION]`, and the ICO registration reference `ZA######` (fee paid 2026-05-11; Freddie to supply the number). Fill these and remove the "Draft — pre-launch" banners.
3. **Outbound email sending** for the swtenderbrief domain isn't enabled yet, so a working signup form isn't wired up.
4. Freddie should read the legal pages line-by-line (and consider a quick paid legal check) before they go fully live.

## Deploying
The repo `jarvisgalliers/swtenderbrief` is a deploy mirror of this directory. Auth: SSH key `~/.ssh/id_ed25519_jarvisgalliers` via the `github-jg` Host alias (see decision #89). To push an update from a clone:
```
git -C <clone> rm -r --quiet . ; cp -r <this-dir>/. <clone>/ ; git -C <clone> add -A
git -C <clone> commit -m "site: <what changed>" ; git -C <clone> push origin main
```
GitHub Pages: Settings → Pages → "Deploy from a branch" = `main` / `/ (root)`; custom domain `swtenderbrief.co.uk`; "Enforce HTTPS" on. DNS for the apex is on Porkbun (decision #29): four `A` records to GitHub's Pages IPs + a `www` `CNAME` to `jarvisgalliers.github.io`.
