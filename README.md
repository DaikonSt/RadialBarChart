# Arcform — deploy to Vercel

Arcform is a single static page (`index.html`). There is no build step, no
framework and no dependencies, so Vercel just serves the file.

```
arcform-vercel/
├── index.html    the whole app (HTML + CSS + JS)
├── vercel.json   small config (clean URLs + basic headers)
├── .gitignore
└── README.md     this guide
```

## Option A — Vercel CLI (no GitHub needed, ~2 minutes)

1. **Install Node.js** (v18+) from https://nodejs.org if you don't have it.
2. **Unzip** this folder and open a terminal inside it:
   ```
   cd arcform-vercel
   ```
3. **Install the Vercel CLI:**
   ```
   npm install -g vercel
   ```
4. **Deploy a preview:**
   ```
   vercel
   ```
   On first run it asks you to log in (it opens your browser or emails you a
   link — use a free Vercel account). Then answer the prompts:
   - *Set up and deploy?* → `Y`
   - *Which scope?* → your personal account
   - *Link to existing project?* → `N`
   - *Project name?* → e.g. `arcform`
   - *In which directory is your code located?* → press Enter (`./`)
   - If it offers to override build settings → `N` (nothing to build)
5. **Promote to production** (gives you the clean `arcform.vercel.app` URL):
   ```
   vercel --prod
   ```
6. **Open the URL** it prints. Done.

To update later: edit `index.html`, run `vercel --prod` again.

## Option B — GitHub + Vercel dashboard (auto-deploys on every push)

1. Create a new repository on GitHub (e.g. `arcform`).
2. Upload this folder's contents to it — either drag the files into the repo
   page on github.com ("Add file → Upload files"), or from a terminal:
   ```
   cd arcform-vercel
   git init
   git add .
   git commit -m "Arcform"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/arcform.git
   git push -u origin main
   ```
3. Go to https://vercel.com/new and sign in (use "Continue with GitHub").
4. Click **Import** next to your `arcform` repo.
5. On the configure screen leave everything at its defaults:
   - Framework Preset: **Other**
   - Build Command: *(empty)*
   - Output Directory: *(empty)*
   - Root Directory: `./`
6. Click **Deploy**. Wait ~20 seconds, then click the preview to open your site.

From now on, every `git push` to `main` redeploys automatically.

## Optional: custom domain

Vercel dashboard → your project → **Settings → Domains → Add**, then follow
the DNS instructions it shows for your domain.

## Good to know

- **SVG export** downloads `arcform-chart.svg` straight from the browser — no
  server involved. Your data never leaves the visitor's machine.
- **Saved settings** (data, colors, arc) are kept in each visitor's own browser
  via localStorage; they aren't shared between people or devices.
- **Fonts** (Archivo, Work Sans, IBM Plex Mono) load from Google Fonts, so the
  UI needs an internet connection to look exactly right. Exported SVGs use
  system font fallbacks so they open correctly anywhere.
- To test locally without deploying: just double-click `index.html`.
