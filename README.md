# savvy.website

A portfolio showcase for [www.savvy.website](https://www.savvy.website) — the
websites and projects built by [HelloSavvy](https://hellosavvy.design), in the
Hello Savvy design aesthetic. The hero is a horizontally scrollable gallery of
projects. It starts with one — [Haka Decks](https://www.hakadecks.com) — and is
built to grow.

## Stack

Zero build step — a self-contained static `index.html` (design tokens mirror
`hello-savvy/apps/marketing/app/globals.css`). Deploys anywhere that serves
static files; Vercel is the default to match the rest of the Savvy stack.

```
index.html        hero + scroll-snap project gallery (progressive-enhancement JS)
favicon.svg       gradient rounded-square "S" mark
assets/           project screenshots (e.g. hakadecks.jpg, 1600px-wide site capture)
vercel.json       static hosting config (clean URLs, asset caching)
```

## Add a project

Each project is one `<article class="project">` block in the `#track` element.
To add one:

1. **Capture a screenshot** of the site (~1600px wide) and drop it in `assets/`.
   The capture used for Haka Decks (no local Chrome needed):
   ```bash
   curl -sL "https://api.microlink.io/?url=https%3A%2F%2Fexample.com&screenshot=true&meta=false&embed=screenshot.url&viewport.width=1366&viewport.height=854&viewport.deviceScaleFactor=2" -o assets/raw.png
   sips -s format jpeg -s formatOptions 82 -Z 1600 assets/raw.png --out assets/example.jpg && rm assets/raw.png
   ```
2. **Duplicate** the commented `<article class="project">` block in `index.html`
   and update the `href` (×2), `<img src/alt>`, the URL pill, the `<h2>` name,
   the blurb, and the discipline `<li>` tags.

The dot + arrow scroll controls appear automatically once there's more than one
card; with a single project they stay hidden.

## Preview locally

```bash
cd savvy-website
python3 -m http.server 8000   # → http://localhost:8000
```

## Deploy to www.savvy.website (Vercel)

1. **Ship it** (from this directory):
   ```bash
   npx vercel            # link/create the project
   npx vercel --prod     # deploy to production
   ```
2. **Attach the domain** — Vercel dashboard → Project → *Settings → Domains*:
   - Add `www.savvy.website` (canonical) and `savvy.website` (redirects to www).
   - Set the DNS records Vercel shows at your registrar:
     - `www` → `CNAME` → `cname.vercel-dns.com`
     - apex `savvy.website` → `A` `76.76.21.21` (or ALIAS → `cname.vercel-dns.com`)
