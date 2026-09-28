# Manne Sandeep — Portfolio

Personal finance & analytics portfolio site.

## Tech stack

This is a **static site** — plain HTML5, CSS and vanilla JavaScript. There is no
React/Next.js/Vite/TypeScript involved and there is no build step.

- **Styling:** [Tailwind CSS](https://tailwindcss.com) via the Play CDN (`cdn.tailwindcss.com`),
  plus a small block of hand-written CSS in `index.html` for effects Tailwind doesn't cover
  (3D tilt cards, the flip-card ID badge, the shimmer text, etc.)
- **Fonts:** Google Fonts (Plus Jakarta Sans, JetBrains Mono), loaded from `fonts.googleapis.com`.
- **JavaScript:** vanilla JS, inline in `index.html` — card tilt/flip physics, the animated
  lanyard, the impact-metric counters, and small UI helpers (toast, clipboard copy).
- **No API calls, no backend, no database, no authentication.**

## Project structure

```
.
├── index.html                          # Intro / entry screen (animated pen trace) -> links to portfolio.html
├── portfolio.html                      # The main portfolio site (single page, in-page anchor nav)
├── assets/
│   ├── images/
│   │   ├── manne-sandeep.jpg           # Profile photo
│   │   ├── favicon.svg                 # Browser-tab icon
│   │   └── apple-touch-icon.png        # iOS home-screen icon
│   └── documents/
│       └── Manne_Sandeep_Resume.pdf    # Downloadable resume
├── package.json                        # No dependencies — scripts are for local preview only
├── vercel.json                         # Static deployment config (clean URLs)
├── .gitignore
└── README.md
```

## Pages

| URL            | File             | What it is                                                                 |
| -------------- | ---------------- | -------------------------------------------------------------------------- |
| `/`            | `index.html`     | Intro screen. "Enter Portfolio" and "Skip intro" both go to `/portfolio`.  |
| `/portfolio`   | `portfolio.html` | The full portfolio. (On Vercel, `/portfolio.html` redirects to `/portfolio`.) |

## Run locally

No install step is required. Any static file server works. For convenience:

```bash
npm run dev
# serves the site at http://localhost:3000  (intro first, then /portfolio)
```

(`npm run dev` shells out to `npx serve`, which Node.js fetches on first run — no dependency
is committed to the repo for it.)

Alternatively, with Python already installed:

```bash
python3 -m http.server 3000
# note: Python's server needs the full filename: http://localhost:3000/portfolio.html
```

## Deploy to Vercel

This project needs **zero configuration** — Vercel detects it as a static site automatically.

1. Push this repository to GitHub (see below).
2. In Vercel: **Add New → Project → Import** the GitHub repo.
3. Use these settings (all left at their defaults):
   - **Framework Preset:** Other
   - **Build Command:** *(empty)*
   - **Output Directory:** *(empty)*
   - **Install Command:** *(empty)*
   - **Root Directory:** `./`
   - **Environment Variables:** none
4. Click **Deploy**.

> There is intentionally **no `build` script** in `package.json`. If one existed, Vercel would run it
> and then look for an output folder named `public`, which this project doesn't have — that would
> fail the deployment. Leave Build Command and Output Directory empty.

## Push to GitHub

```bash
git init
git add .
git commit -m "Initial commit: portfolio site"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

## Known, non-blocking notes

- Tailwind is loaded from its **Play CDN** rather than compiled locally. It works correctly in
  production (every visitor's browser fetches it directly), but Tailwind's own script logs a
  console warning that the CDN build "should not be used in production." Functionally this is
  harmless for a site of this size. If you'd like it removed, the fix is to compile Tailwind
  with the `tailwindcss` CLI into a static `styles.css` and drop the `<script>` tag — happy to
  do that as a follow-up.
- The site is two static pages (intro + portfolio). The portfolio itself uses in-page anchor
  navigation (`#about`, `#projects`, etc.), so there is no client-side router and nothing extra
  to configure for direct navigation — every URL is a real file.
