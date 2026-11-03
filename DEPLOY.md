# Launching kaylagautereaux.com

> **Status (2026-11-02)**: Kayla approved publishing. Site committed, pushed to github.com/kgautereaux/kaylagautereaux.com, and published to GitHub Pages at https://kgautereaux.github.io/kaylagautereaux.com/ for review. The custom domain is NOT attached yet, and DNS still points at Squarespace.

## Preview locally

```bash
quarto preview /Users/kgautereaux/Projects/teaching/web/kaylagautereaux.com
```

## Before launch: things to confirm

- [x] Contact email: personal Gmail (decided 2026-11-02)
- [x] Location: "Boston area" (decided 2026-11-02)
- [ ] Graduate outcome stats (42 graduates, 85% teaching, 65% at universities) were removed because they date from March. Confirm current numbers to restore them (commented out in `teaching.qmd`).
- [x] YouTube icon (Voice Box Channel): keep (decided 2026-11-02)
- [ ] Still open: a singing recording (photos and the Earthshot video are up), headshot photo credit, and photographer/event captions for the performance photos.

## Step 1: GitHub repo and publish (done 2026-11-02)

The site publishes the same way as the research archive: `quarto publish gh-pages` renders and pushes the built site to a `gh-pages` branch. `docs/` stays out of git.

Private files stay out: `.gitignore` excludes the headshot folder and 1.9GB zip, `brand-strategy.md`, `brand-options/` (including the old logo previews), and the `shared-design` symlink. `_quarto.yml` renders only the six public pages.

The first publish leaves the custom domain off on purpose. With a CNAME file in the published site, GitHub would redirect the github.io address to kaylagautereaux.com, which still shows Squarespace, so the new site could not be reviewed.

## Step 2: Point the domain at GitHub (Kayla does this in GoDaddy)

Do this only after the github.io site looks right. Keep Squarespace active until the new site is confirmed live.

1. **Attach the domain (Claude can do this when Kayla says go).** Create a file named `CNAME` in the project root containing `kaylagautereaux.com`, set `site-url: https://kaylagautereaux.com` in `_quarto.yml`, and run `quarto publish gh-pages --no-prompt`. (Quarto publishes a root `CNAME` file automatically, which is why it is left out until this step.) That publishes the CNAME file, which sets `kaylagautereaux.com` as the custom domain in the repo's Settings → Pages. From then on the github.io address redirects to kaylagautereaux.com, so do steps 2 to 5 right away.
   Also, on your GitHub profile, go to Settings → Pages → "Verified domains" and add `kaylagautereaux.com`. GitHub gives you a TXT record to add in GoDaddy. This stops anyone else from claiming your domain on GitHub.
2. **GoDaddy.** Sign in, open My Products → kaylagautereaux.com → DNS.
3. **Leave these alone**: the `research` and `studio` CNAME records, and any MX or TXT records for email.
4. **Replace the Squarespace records:**
   - Delete the `@` A records that point to Squarespace (they look like `198.185.159.x` or `198.49.23.x`).
   - Add four `@` A records: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - Optional (IPv6): four `@` AAAA records: `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153`
   - Change the `www` CNAME from `ext-cust.squarespace.com` to `kgautereaux.github.io`
   - If GoDaddy has domain forwarding turned on for this domain, turn it off.
5. **Wait.** DNS usually updates within an hour, sometimes up to 24.
6. **Back in GitHub** Settings → Pages, once the domain check turns green, tick "Enforce HTTPS."
7. **Check**: https://kaylagautereaux.com, https://www.kaylagautereaux.com, and that research. and studio. still load. Also click "Contact for Lessons" on the studio site: it points to `www.kaylagautereaux.com/contact`, which should now open the new Contact page.
8. **Then** cancel or downgrade the Squarespace site (export anything you want to keep first).

If the domain is registered at Squarespace rather than GoDaddy, the same records go in Squarespace's Domains → DNS settings instead.

## Updating the site later

Edit the `.qmd` files, then:

```bash
quarto publish gh-pages --no-prompt
```
