# Magan Sundar Oram — Portfolio

A single-page portfolio. Pure HTML/CSS/JS, no build step, no dependencies.

```
Portfolio/
├── index.html
├── style.css
├── script.js
├── robots.txt
├── sitemap.xml
├── site.webmanifest
├── vercel.json
└── assets/
    ├── images/
    │   └── og-image.png        ← social-preview image (LinkedIn/WhatsApp/Twitter)
    ├── icons/
    │   ├── favicon.svg
    │   ├── favicon-32.png
    │   └── apple-touch-icon.png
    └── fonts/
```

---

## 1. Deploy: GitHub → Vercel

1. Push this folder to a new GitHub repo (e.g. `portfolio`).
2. On [vercel.com](https://vercel.com), **Add New → Project**, import that repo.
3. Framework preset: **Other** (it's static HTML — no build command, no install command, output directory is the repo root). Vercel usually detects this automatically.
4. Deploy. You'll get a URL like `https://portfolio-yourname.vercel.app`.
5. *(Optional)* Add a custom domain under Project → Settings → Domains.

## 2. ⚠️ One required edit: set your real URL

Search engines need a real, final URL in a few places. Right now they're filled in with a **placeholder**:

```
https://magan-sundar-oram.vercel.app/
```

Once you know your actual Vercel URL (or custom domain), replace every occurrence of that placeholder with your real one. It appears in:

- `index.html` — `<link rel="canonical">`, the Open Graph (`og:url`, `og:image`) and Twitter tags, and the JSON-LD structured data block
- `robots.txt` — the `Sitemap:` line
- `sitemap.xml` — the `<loc>` value

**Quickest way** (run from inside the `Portfolio` folder, after editing the value below):

```bash
# macOS
find . -type f \( -name "*.html" -o -name "*.xml" -o -name "*.txt" \) \
  -exec sed -i '' 's#https://magan-sundar-oram.vercel.app#https://YOUR-REAL-DOMAIN.com#g' {} +

# Linux
find . -type f \( -name "*.html" -o -name "*.xml" -o -name "*.txt" \) \
  -exec sed -i 's#https://magan-sundar-oram.vercel.app#https://YOUR-REAL-DOMAIN.com#g' {} +
```

Commit and redeploy after this change.

## 3. Get indexed: Google Search Console

1. Go to [search.google.com/search-console](https://search.google.com/search-console) and **Add Property** using your real domain (URL-prefix method is simplest for a Vercel URL).
2. Verify ownership using the **HTML tag** method:
   - Search Console gives you a `<meta name="google-site-verification" ...>` tag.
   - Open `index.html`, find the commented-out line near the top of `<head>`:
     ```html
     <!-- <meta name="google-site-verification" content="PASTE_YOUR_VERIFICATION_CODE_HERE" /> -->
     ```
   - Uncomment it and paste in your code. Redeploy, then click **Verify** in Search Console.
3. In Search Console, go to **Sitemaps** (left sidebar) and submit:
   ```
   sitemap.xml
   ```
4. Go to **URL Inspection**, paste your homepage URL, and click **Request Indexing**. This nudges Google to crawl it right away instead of waiting.

Indexing isn't instant — it can take anywhere from a few hours to a couple of weeks. Requesting indexing speeds it up but doesn't guarantee a specific timeline.

## 4. What was added to help you rank for your name

- **Title & meta description** rewritten to lead with your name and role (what shows up in the Google result snippet).
- **JSON-LD structured data** (`Person` + `WebSite` schema) — explicitly tells Google "this page is about a person named Magan Sundar Oram," which is what makes name-search results more likely to surface this site, and is also the basis for things like Google's sitelinks search box or a knowledge panel down the line.
- **Open Graph / Twitter Card tags + a custom social image** (`assets/images/og-image.png`) — when you share the link on LinkedIn, WhatsApp, or X, it now shows a proper branded preview card instead of a blank or broken one.
- **`sameAs` links** to your GitHub and LinkedIn in the structured data — this helps Google connect your name to those other profiles as the same entity.
- **`robots.txt` + `sitemap.xml`** — tells search engines they're allowed to crawl the whole site and exactly which URL to index.
- **Favicons + web manifest** — small trust/quality signal, and makes the site look correct when bookmarked or added to a home screen.
- **Single `<h1>` (your name) and clean heading order** — already correct in the markup, which matters for how Google parses page topic and hierarchy.

## 5. A few things beyond this codebase that matter just as much

Google ranking name-searches is heavily about **entity association**, not just on-page tags:

- Make sure your **GitHub** and **LinkedIn** profiles link back to this portfolio URL — backlinks from those high-authority profiles are one of the strongest signals tying your name to this site.
- Use the **same name spelling** consistently everywhere (GitHub bio, LinkedIn headline, resume, etc.).
- The more your name is *uniquely* searched (i.e. you're not competing with someone famous sharing your name), the faster a personal site tends to rank for it.
