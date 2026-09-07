# BreakPoint Insight website

Static site. No build step. Deployed on Vercel from this repository.

## Structure
- `index.html` — homepage
- `peter-hillis.html`, `brendan-gladman.html` — partner biographies
- `insight-*.html` — Insights articles
- `assets/` — Open Graph share images, favicon
- `vercel.json` — clean URLs (`/peter-hillis` serves `peter-hillis.html`), cache and security headers
- `robots.txt`, `sitemap.xml`

## Before the first public deploy
1. Replace `BREAKPOINT_DOMAIN` in every `.html`, `robots.txt` and `sitemap.xml` with the real domain, e.g. `breakpointinsight.com`:
   `grep -rl BREAKPOINT_DOMAIN . | xargs sed -i "s/BREAKPOINT_DOMAIN/breakpointinsight.com/g"`
2. Replace the two portrait placeholders (`<div class="portrait">…</div>`) with `<img>` tags pointing at photos in `assets/`.
3. Complete `brendan-gladman.html` (amber placeholder spans).
4. Check product status labels on `index.html`.

## Deploy
Push to GitHub, import the repository in Vercel (Framework preset: Other; no build command; output directory: `.`), add the domain under Project → Settings → Domains, and set the DNS records Vercel shows at the registrar.

## Editing
Each page is self-contained (CSS inline). Shared elements (nav, footer, tokens) are duplicated per page; change them in every file or keep them in sync with a search-and-replace. Design tokens are frozen; see the `:root` block at the top of each file.

## Adding an Insight
Copy `insight-not-demonstrated.html`, replace the head metadata, kicker, title, body and "Read next" block, add an OG image to `assets/`, add the page to `sitemap.xml`, and link it from the Insights section of `index.html`.
