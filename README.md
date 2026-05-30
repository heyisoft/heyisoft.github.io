# heyisoft.github.io

Static site hosted on GitHub Pages. Houses public-facing pages for heyisoft apps —
landing, legal, support.

Multi-app aware: each app lives in its own subdirectory.

## URL map

| Path | File | Purpose |
|---|---|---|
| `/` | `index.html` | Studio landing, lists apps |
| `/assets/heyisoft.css` | — | Root-only stylesheet (studio aesthetic) |
| `/taslak/` | `taslak/index.html` | Taslak app landing + legal index |
| `/taslak/privacy/` | `taslak/privacy/index.html` | Taslak Privacy Policy |
| `/taslak/terms/` | `taslak/terms/index.html` | Taslak Terms of Use |
| `/taslak/contact/` | `taslak/contact/index.html` | Taslak Contact & Support |
| `/taslak/assets/style.css` | — | Taslak-only stylesheet |

## Per-app isolation (important)

Each app is fully self-contained — its own subdirectory, its own pages, **and
its own stylesheet**. There is no shared app stylesheet. This is deliberate:
every app gets a distinct visual identity, and changing one app never touches
another.

- **Root** (`/`) uses `assets/heyisoft.css` — an editorial dark-studio look
  (warm near-black, cream type, gold accent; Fraunces + Inter Tight).
- **Taslak** (`/taslak/*`) uses `taslak/assets/style.css` — matches the Taslak
  app palette (LinkedIn-blue `#0A66C2`, score-ring motif, sparkle accent;
  Bricolage Grotesque + IBM Plex Sans).

## Adding a new app

1. Create `<app>/` at the root.
2. Add `<app>/index.html`, `<app>/privacy/index.html`, `<app>/terms/index.html`, `<app>/contact/index.html`.
3. Create `<app>/assets/style.css` — **its own** stylesheet, designed for that
   app's brand. Do not reuse another app's CSS.
4. Point every `<app>` page's `<link>` at `/<app>/assets/style.css`.
5. Add a new `.app-row` to the root `index.html` **Apps** section and bump the
   `.count`.

## Stack

- Plain HTML — no build, no framework.
- Per-app stylesheets (no shared app CSS). Root has its own.
- Google Fonts loaded per-stylesheet:
  - Root: Fraunces (display), Inter Tight (body).
  - Taslak: Bricolage Grotesque (headings), IBM Plex Sans (body), IBM Plex Mono (code).
- Subtle CSS-only animations (fade-up / lift-in on load, hover transitions).
- Respects `prefers-reduced-motion`.

## Local preview

```sh
# any static server works
python3 -m http.server 8000
# then open http://localhost:8000
```

## Deploy

GitHub Pages serves the `main` branch root automatically. Push to `main` and the
new content is live in 1–2 minutes.

## License

Site content © heyisoft. Source code under MIT-style permissive terms — see
individual files where applicable.
