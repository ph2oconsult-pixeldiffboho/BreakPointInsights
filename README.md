# BreakPoint Insight website

Static site. No build step. Deployed on Vercel from this repository.

## Structure
- `index.html` — homepage
- `peter-hillis.html`, `brendan-gladman.html` — partner biographies
- `insights/` — Insights archive (`insights/index.html`) and articles (`insights/<slug>.html`, served at `/insights/<slug>`)
- `assets/` — Open Graph share images, favicon
- `vercel.json` — clean URLs (`/peter-hillis` serves `peter-hillis.html`), cache and security headers
- `robots.txt`, `sitemap.xml`

## Before the first public deploy
1. Replace `BREAKPOINT_DOMAIN` in every `.html`, `robots.txt` and `sitemap.xml` with the real domain, e.g. `breakpointinsight.com`:
   `grep -rl BREAKPOINT_DOMAIN . | xargs sed -i "s/BREAKPOINT_DOMAIN/breakpointinsight.com/g"`
2. Replace the two portrait placeholders (`<div class="portrait">…</div>`) with `<img>` tags pointing at photos in `assets/`.
3. Complete `brendan-gladman.html` (amber placeholder spans).
4. Check product status labels on `index.html`.

## Contact form (Web3Forms)
The enquiry form posts to Web3Forms, which emails each submission to peter.hillis@ph2oconsult.com. No server code and no secret in the repo.
1. Go to https://web3forms.com, enter peter.hillis@ph2oconsult.com, and confirm the email they send. They reply with an access key.
2. Replace `WEB3FORMS_ACCESS_KEY` in `index.html` with that key. The key is safe to publish: it can only deliver to the registered address.
3. Optional: in the Web3Forms dashboard, turn on spam filtering and set a redirect or autoresponder. The form already includes a honeypot field.
Alternative if you would rather not use a third party: a Vercel serverless function with Resend or SendGrid, which needs an API key stored as a Vercel environment variable. Ask if you want that version.

## WhatsApp
The contact card links to https://wa.me/61429202851 with a pre-filled opening message. Change the number in `index.html` if a different WhatsApp account is used.

## Deploy
The remote is already configured: `origin` = https://github.com/ph2oconsult-pixeldiffboho/BreakPointInsights.git

First push: `git push -u origin main`

Then, import the repository in Vercel (Framework preset: Other; no build command; output directory: `.`), add the domain under Project → Settings → Domains, and set the DNS records Vercel shows at the registrar.

## Versioning
Every page carries `<meta name="version">` and a footer line "Site version X.Y.Z". `VERSION` holds the current number and `CHANGELOG.md` lists what changed. When you change the site: bump `VERSION`, update the version string in every `.html` (search for "Site version"), add a changelog entry, commit, push. Then check the footer of the live site to confirm the deployment.

## Editing
Each page is self-contained (CSS inline). Shared elements (nav, footer, tokens) are duplicated per page; change them in every file or keep them in sync with a search-and-replace. Design tokens are frozen; see the `:root` block at the top of each file.

## Adding an Insight
Copy `insights/not-demonstrated.html`, replace the head metadata, kicker, title, body and "Read next" block, add an OG image to `assets/`, add the page to `sitemap.xml`, and add a row to `insights/index.html` and, if featured, to the Insights section of `index.html`.
