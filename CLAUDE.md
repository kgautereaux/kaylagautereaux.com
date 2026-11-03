# kaylagautereaux.com

Kayla Gautereaux's personal website. Quarto site, published to GitHub Pages, live at https://kaylagautereaux.com since November 2, 2026. It replaced a Squarespace site.

Read `DEPLOY.md` for launch history and the DNS records. This file is the working guide.

## Build, preview, publish

```bash
cd /Users/kgautereaux/Projects/teaching/web/kaylagautereaux.com
quarto preview            # local preview (or the "kaylagautereaux-site" entry in ~/Projects/.claude/launch.json, port 4848)
quarto render             # builds into docs/ (gitignored)
git add -A && git commit -m "..." && git push origin main
quarto publish gh-pages --no-prompt --no-browser
```

- Source: `main` branch of github.com/kgautereaux/kaylagautereaux.com (public). Built site: `gh-pages` branch, written only by `quarto publish`.
- Stop a running `quarto preview` before `quarto render` or `quarto publish`. Rendering while the preview runs leaves the preview serving stale or broken pages.
- After publishing, confirm with `curl -s https://kaylagautereaux.com/<page>.html | grep "<new text>"`. GitHub Pages usually updates within a minute.
- Never commit to or check out `gh-pages` by hand.

### Domain gotchas (learned the hard way)

- The root `CNAME` file (`kaylagautereaux.com`) is required. `quarto publish` copies it to `gh-pages`, which keeps the custom domain attached. Removing it detaches the domain.
- `site-url` in `_quarto.yml` must stay `https://kaylagautereaux.com` (used for Open Graph and the sitemap).
- HTTPS certificate: GitHub only requests one when the domain is saved after DNS is correct. If the cert ever shows as missing, re-save the domain: `echo '{"cname": null}' | gh api -X PUT repos/kgautereaux/kaylagautereaux.com/pages --input -`, then the same with `"kaylagautereaux.com"`, then `echo '{"https_enforced": true}' | gh api -X PUT ... --input -`.
- DNS lives at GoDaddy. Apex `@` A records point to GitHub (185.199.108–111.153); `www` CNAME to `kgautereaux.github.io`; `research` and `studio` CNAMEs to `kgautereaux.github.io`. The MX and TXT records run Kayla's email: never touch them.
- Shell DNS lookups (`dig`) don't work from Claude's sandbox. Use `https://dns.google/resolve?name=...&type=...` in the browser pane instead.

### Never commit or publish

`.gitignore` excludes these, and `_quarto.yml` `render:` lists only the six public pages:
- `Kayla Gautereaux Headshots/` and the 1.9GB headshot zip
- `brand-strategy.md` (private March 2026 career notes)
- `brand-options/` (old logo previews and palettes)
- the `shared-design` symlink

## Site structure

Top menu: About · Teaching · Research (→ research.kaylagautereaux.com) · Voice Studio (→ studio.kaylagautereaux.com) · AI & Learning · Contact. The footer also links Research Archive, Studio, Presentations & Media, and social icons (LinkedIn, Instagram, YouTube).

| File | Page | Notes |
|---|---|---|
| `index.qmd` | Home | Split hero (lab spectrogram photo), "Singing for health" row with Berklee Office Hours video (autoplays muted with captions; browsers block sound), stats strip (2026 / 2023 / 35 / 33), alternating rows: Research, Teaching, AI and learning; closing photo band (Kayla as the Mother in *Amahl and the Night Visitors*) |
| `about.qmd` | About | Chronological story: San Diego, New England Conservatory, Boston Conservatory, How I teach (+ VocalFri podcast), What I'm building now, Presentations and publications (selected), Performing (+ Earthshot video), Awards / Education |
| `teaching.qmd` | Teaching | Two degrees, then "How students move through the program" (Arriving, Every week, The teaching exam, Research, After graduation), Workshops (VPPW + sign-up), Vocal Academy (+ sign-up), Private studio |
| `ai-learning.qmd` | AI and Learning | AI as a partner in teaching and learning, not a replacement. Podcast, studio portal (3 screenshots, demo buttons), research archive (built and maintained with Claude), consulting |
| `speaking.qmd` | Presentations & Media | Watch and listen (video + 2 podcast players), Presentations and publications by year (generated from `career-manager/voice-faculty-portfolio/cv-draft.md` plus 2026 talks), VocalFri episodes, topics |
| `contact.qmd` | Contact | kgautereaux@gmail.com, LinkedIn, Boston area |

Page IDs: the old `ai-voice`, `learning-tools`, `research`, and `studio` pages were removed or renamed; don't recreate them.

## Design system (chosen November 2026)

- **Look:** deep teal. Panels `#0F3533`, seafoam buttons on dark `#5FBFAE`, headings `#14504C`, links and buttons on light `#1F7A72`, page `#F8FAF9`, light tint `#E8F1EF`, muted text `#4F5F5C`. Teal was sampled from the spectrogram in the hero photo.
- **Never navy** (Boston Conservatory's brand color; the site must not read as institutional). **Plum is retired** for this site.
- **Type:** Newsreader (name, headings, body) and Instrument Sans (menus, buttons, labels, captions), loaded from Google Fonts in `_quarto.yml`. Forum, DM Sans, and Libre Baskerville were dropped.
- **Layout pieces in `styles.css`:** `.hero.hero-split`, `.split` / `.split.reverse` rows, `.photo-band`, `.stats-strip` with `.stat-big` / `.stat-note`, `.lab-photo`, `.screenshot-frame`, `.shot-row`, `.singing-gallery`, `.video-embed`, `.podcast-player`, `.photo-credit`, `.two-col`. The later "Deep teal theme" and "Stats" blocks at the end of `styles.css` override earlier rules.
- **Media first:** put the photo, video, podcast, or screenshot directly under each heading, then the text.
- Favicon: white Newsreader "G" on teal (`favicon.svg`, `images/favicon-32.png`, `images/apple-touch-icon.png`). Social preview: `images/og-card.jpg` (lab photo crop).
- Check every change at desktop (1280) and phone (375) widths before publishing.

## Media and credits

- Berklee photos by **Simon Simard** (VPPW 2026 shoot): `lab-spectrogram`, `lab-breathing`, `vppw-workshop`, `vppw-piano`, `vppw-ear-model`, `vppw-group`. Every use carries `[Photo: Simon Simard for Berklee]{.photo-credit}`. Originals: `~/Downloads/berklee-mediagraph-download-#4191121.zip`.
- Performance photos (`singing-*`): photographer and event unknown except `singing-costume` (the Mother in Menotti's *Amahl and the Night Visitors*). Headshots (`about`, `about-accent`, `hero`, `studio`, `speaking`): photographer not yet credited.
- Images are web-sized (1600px long side, ~80% JPEG, metadata stripped). Never add full-resolution originals.
- Embeds: YouTube via `youtube-nocookie.com`; VocalFri via Podbean `player-v2/?i=<id>` (88x5b-1998280 = Scientific Method Informed Voice Teaching; 2k3gu-1a9fb06 = AI and the Voice Practitioner).

## Writing rules (Kayla's, firm)

- Plain, collegial, first person. Tell the story; don't punch it. No em dashes.
- No taglines, slogans, wry asides, punchy fragments, colon reveals, "not X but Y" (except her own "partner, not replacement" line for AI), habitual groups of three, or summing-up closers. Lines she rejected: "I liked it more than I expected to," "I still perform," "Each of these roles shapes the others," "That is where I learned how clinical research is run," "Voice teacher, researcher, and builder."
- Spell out acronyms at first use per page (NATS, PAVA, IRB, MGH); outside readers don't know them.

## Facts to get right

- Assistant Professor of Voice and Vocal Pedagogy, Boston Conservatory at Berklee. On this site, do not use "Head of Vocal Pedagogy" (fine on her resume, not here). Never "voice scientist."
- Hired 2022 to lead the research side of two graduate degrees in voice teaching and singing (supporting scholarly reading, research, and publication). Never "degrees with no connection to science."
- Leads the area since 2024: she *leads* the MM in Vocal Pedagogy and MFA in Musical Theater Vocal Pedagogy (never "directs"). The MM is genre-inclusive, never "the classical track."
- *Directs* the Vocal Pedagogy Professional Workshop (VPPW) and Vocal Academy.
- MGH Voice Center partnership predates her; she *strengthened* it.
- Acoustic Vocal Pedagogy Workshop (Embodied Music Lab): faculty and organizer since 2019. She did not found it.
- Do not say she taught herself Python.
- Mezzo-soprano. 2022 Earthshot Prize Awards in Boston: backup for Ellie Goulding's "Still Falling for You," with the Prince and Princess of Wales in the audience.
- AI Supported Voice Studio Portal: PAVA 2026 Best Microworkshop/ToolTalk. Research archive: 33 studies, 17 topics, 2022–2026, built and maintained with Claude.
- 35 conference presentations by alumni since 2022 (19 Voice Foundation, 7 PAVA, 6 NATS). 2023 NATS Voice Pedagogy Award.
- Journal of Singing article is by Mariana Elosúa Serna and Brian Manternach (82, no. 3, 2026, doi 10.53830/sing.00189); it builds on Mariana's thesis, which Kayla supervised.
- Verify enrollment or outcome numbers with Kayla before adding them. The March 2026 outcome stats are commented out in `teaching.qmd` until confirmed.

## Open items

- Kayla to export anything wanted from Squarespace, then cancel it.
- Optional: add kaylagautereaux.com under GitHub profile Settings → Pages → Verified domains (adds one TXT record in GoDaddy).
- A singing recording for About (placeholder comment in `about.qmd`).
- Headshot photographer credit; captions and credits for the other three performance photos.
- Confirm current graduate outcome numbers before restoring them.
- research.kaylagautereaux.com still uses navy and studio.kaylagautereaux.com uses plum; matching them to the teal look is a separate decision.
