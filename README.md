# AI in Education Daily — publishing site

This folder is a **static site** ready to publish via GitHub Pages (or Netlify, or any static host). Once deployed, the URL never changes and the newsletter refreshes each weekday when the automation regenerates and re-pushes.

## Structure

```
site/
├── index.html            ← always the latest issue
├── archive.html          ← list of every past issue
├── AI in Education Daily - YYYY-MM-DD.pdf
└── issues/
    └── 2026-09-03.html   ← one file per issue
```

## First-time deploy (about 10 minutes)

1. **Create a public GitHub repo** — e.g. `ai-education-weekly`.
2. From the local site folder:
   ```bash
   cd /path/to/site
   git init
   git add .
   git commit -m "Initial site with 2026-09-03 issue"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/ai-education-weekly.git
   git push -u origin main
   ```
3. **Enable Pages** on the repo — GitHub → Settings → Pages → Build from `main` branch, `/` (root).
4. GitHub gives you a URL like `https://YOUR-USERNAME.github.io/ai-education-weekly/`. Share that link in your Teams sandbox — it will always show the latest issue.

## Daily workflow (after first deploy)

The automation will:

1. Generate the new issue as `Weekly Digest - YYYY-MM-DD.html` and `AI in Education Daily - YYYY-MM-DD.pdf`
2. Copy it to `site/index.html` and `site/issues/YYYY-MM-DD.html`
3. Prepend the new entry to the `<ol class="issue-list">` in `site/archive.html`
4. Commit and push:
   ```bash
   cd site && git add . && git commit -m "Issue YYYY-MM-DD" && git push
   ```

GitHub Pages redeploys automatically (usually within 30–60 seconds).

## Notes

- **No backend needed** — everything is static HTML. No JavaScript beyond the newsletter's own styling.
- **The shared URL stays the same forever.** Only the content behind it changes.
- **The archive keeps growing** — every issue lives at a stable `issues/YYYY-MM-DD.html` URL, so links you paste in Teams keep working.
- **Custom domain** (optional) — later, you can point a subdomain (e.g. `ai-edu-weekly.yourdomain.com`) at the GitHub Pages site via a CNAME.
