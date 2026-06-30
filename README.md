# nambik-ai.com

Static marketing site for Nambik AI — consultancy for bespoke AI solutions and IT services.

Plain HTML/CSS/JS. No build step. Hosted on GitHub Pages with custom domain `nambik-ai.com`.

## Local preview

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

Or just open `index.html` directly in a browser.

## Structure

```
index.html          # Hero, services, about, contact (single-page anchors)
case-studies.html   # Placeholder list of past work
blog/index.html     # Placeholder insights index
styles.css          # All styling
favicon.svg
CNAME               # Custom domain for GH Pages
.nojekyll           # Skip Jekyll processing
robots.txt
sitemap.xml
```

## Deploying to GitHub Pages

### 1. Create the repo

```bash
cd /Users/navnita/dev/nambikai-site
git init
git add .
git commit -m "Initial site"
gh repo create nambikai-site --public --source=. --remote=origin --push
```

### 2. Enable Pages

```bash
gh api -X POST /repos/:owner/nambikai-site/pages \
  -f source[branch]=main -f source[path]=/
```

Or in GitHub UI: **Settings → Pages → Source: Deploy from a branch → Branch: main / (root)**.

### 3. Point the domain

The `CNAME` file already declares `nambik-ai.com`. Next, configure DNS at your registrar:

**Apex domain (`nambik-ai.com`)** — add four `A` records pointing to GitHub's IPs:

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

**`www` subdomain** — add a `CNAME` record pointing to `<your-gh-user>.github.io`.

### 4. Enforce HTTPS

In **Settings → Pages**, tick **Enforce HTTPS** once the cert provisions (can take an hour).

## Editing

- Copy is in the HTML files directly — no CMS.
- Colours live in `:root` at the top of `styles.css`.
- To add a real blog post, drop a new HTML page in `/blog/` and link it from `blog/index.html`.

## Email

The site links to `support@nambik-ai.com`. Set that up via your domain registrar's email forwarding (e.g. Cloudflare Email Routing, free) pointing to your real inbox.
