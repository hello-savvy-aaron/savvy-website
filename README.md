# savvy.website

A single-page **coming soon** site for [www.savvy.website](https://www.savvy.website),
built in the [Hello Savvy](https://hellosavvy.design) design aesthetic. It will
grow into a hub that links out to many other websites.

## Stack

Zero build step — a self-contained static `index.html` (design tokens mirror
`hello-savvy/apps/marketing/app/globals.css`). Deploys anywhere that serves
static files; Vercel is the default to match the rest of the Savvy stack.

```
index.html      coming-soon page + a ready-to-fill link-hub grid (commented out)
favicon.svg     gradient rounded-square "S" mark
vercel.json     static hosting config (clean URLs, asset caching)
```

## Preview locally

```bash
cd savvy-website
python3 -m http.server 8000   # → http://localhost:8000
```

## Deploy to www.savvy.website (Vercel)

1. **Create the project** (from this directory, one time):
   ```bash
   npx vercel            # link/create the project
   npx vercel --prod     # ship to production
   ```
2. **Attach the domain** — Vercel dashboard → Project → *Settings → Domains*:
   - Add `www.savvy.website` (canonical) and `savvy.website` (redirects to www).
   - Vercel shows the exact DNS records to set at your registrar:
     - `www` → `CNAME` → `cname.vercel-dns.com`
     - apex `savvy.website` → `A` `76.76.21.21` (or an ALIAS to `cname.vercel-dns.com`)

## Turning on the link hub

When you're ready to launch, edit `index.html`:
1. Fill the `<section class="links">` grid with your sites (one `<a>` each).
2. Remove the surrounding `<!-- ... -->` so the section renders.
3. Soften or remove the "Launching soon" eyebrow + coming-soon copy.

All the link-card styling is already in the `<style>` block.
