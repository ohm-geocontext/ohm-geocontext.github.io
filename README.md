# ohm-geocontext.github.io

The landing page for **[GeoContext](https://geocontext.info)** — served at
<https://geocontext.info> via GitHub Pages.

A single, self-contained static page. No build step, no framework, no
submodules — open `index.html` in a browser and what you see is what
ships. (Fitting, for a project whose whole pitch is *no fork, no build,
no account*.)

## Files

| Path | Purpose |
|---|---|
| `index.html` | The entire site — markup + inline CSS, self-contained. |
| `assets/logo.png` | The GeoContext mark (networked globe + `{ }` map pin). |
| `assets/og.png` | 1200×630 social/OpenGraph card. |
| `favicon.svg` | Vector favicon. |
| `CNAME` | Custom domain → `geocontext.info`. |
| `.nojekyll` | Serve files as-is, skip Jekyll processing. |
| `robots.txt` / `sitemap.xml` | Crawl hints. |

## Develop

```bash
# any static server works; e.g.
python3 -m http.server 8080
# → http://localhost:8080
```

Fonts (Switzer, JetBrains Mono) load from CDNs at runtime; everything
else is local. The design follows the GeoContext brand: warm paper
surface, editorial typography, a single teal-green accent, and the data
palette from a real `geocontext.json` for the accent dots. Light and
dark modes both get first-class treatment via `prefers-color-scheme`,
and motion respects `prefers-reduced-motion`.

## Deploy

GitHub Pages, served from the default branch root.

1. **Settings → Pages →** Source: *Deploy from a branch*, branch `main`,
   folder `/ (root)`.
2. **Custom domain:** `geocontext.info` (the `CNAME` file already sets
   this). Add the matching DNS records at the registrar:
   - apex `geocontext.info` → four `A` records to GitHub Pages
     (`185.199.108.153`, `.109.153`, `.110.153`, `.111.153`) and the
     `AAAA` equivalents, **or** an `ALIAS`/`ANAME` to
     `ohm-geocontext.github.io`.
   - optional `www` → `CNAME` to `ohm-geocontext.github.io`.
3. Tick **Enforce HTTPS** once the certificate is issued.

## Regenerate the OG image

```bash
F=/usr/share/fonts/truetype/dejavu
convert -size 1200x630 xc:'#f5f0e8' \
  -fill '#efe8da' -draw "rectangle 0 612 1200 630" \
  \( assets/logo.png -resize 380x380 \) -gravity West -geometry +96+8 -composite \
  -gravity NorthWest \
  -font "$F/DejaVuSans-Bold.ttf" -pointsize 94 -fill '#1b1a17' -annotate +540+150 'GeoContext' \
  -font "$F/DejaVuSans.ttf" -pointsize 39 -fill '#6b6459' -annotate +544+286 'Publish a map of any' \
  -font "$F/DejaVuSans.ttf" -pointsize 39 -fill '#6b6459' -annotate +544+336 'public dataset.' \
  -font "$F/DejaVuSansMono-Bold.ttf" -pointsize 30 -fill '#17795e' -annotate +544+452 'geocontext.info' \
  -font "$F/DejaVuSansMono.ttf" -pointsize 24 -fill '#8b8475' -annotate +544+506 'No fork  ·  No build  ·  No account' \
  assets/og.png
```

---

Apache-2.0 · Made in Bologna by [OpenHistoryMap](https://www.openhistorymap.org).
