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
| `/kalender/` | `kalender/index.html` | Kalender landing + legal index (EN) |
| `/kalender/privacy/` | `kalender/privacy/index.html` | Kalender Privacy Policy (EN) |
| `/kalender/terms/` | `kalender/terms/index.html` | Kalender Terms of Use (EN) |
| `/kalender/contact/` | `kalender/contact/index.html` | Kalender Contact & Support (EN) |
| `/kalender/tr/` | `kalender/tr/index.html` | Kalender tanıtım + hukuki dizin (TR) |
| `/kalender/tr/privacy/` | `kalender/tr/privacy/index.html` | Kalender Gizlilik Politikası ve KVKK Aydınlatma Metni (TR) |
| `/kalender/tr/terms/` | `kalender/tr/terms/index.html` | Kalender Kullanım Koşulları (TR) |
| `/kalender/tr/contact/` | `kalender/tr/contact/index.html` | Kalender İletişim ve destek (TR) |
| `/kalender/assets/style.css` | — | Kalender-only stylesheet |

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
- **Kalender** (`/kalender/*`) uses `kalender/assets/style.css` — the app's own
  tokens (indigo thread `#27307A`, morning-glass `#EEF2F7`, saffron / sage /
  lavender energy beads), light and dark; thread-and-bead SVG motif; Gambarino
  headings (Fontshare CSS API, unmodified per the ITF Free Font License) + system UI body.

## Bilingual apps (TR + EN)

An app that needs Turkish and English keeps English at `/<app>/...` and mirrors
every page under `/<app>/tr/...` with the same slugs. Each page links its twin
with `rel="alternate" hreflang` and a language switch in the header nav, so each
language has its own URL for the store listing (e.g. App Store privacy URL per
locale). Kalender is the first app using this pattern.

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
  - Kalender: Gambarino (headings, from Fontshare), system UI (body).
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
