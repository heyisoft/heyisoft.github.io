# heyisoft.github.io

Static site hosted on GitHub Pages. Houses public-facing pages for heyisoft apps —
landing, legal, support.

Multi-app aware: each app lives in its own subdirectory.

## URL map

| Path | File | Purpose |
|---|---|---|
| `/` | `index.html` | Studio landing, lists apps |
| `/taslak/` | `taslak/index.html` | Taslak app landing + legal index |
| `/taslak/privacy/` | `taslak/privacy/index.html` | Taslak Privacy Policy |
| `/taslak/terms/` | `taslak/terms/index.html` | Taslak Terms of Use |
| `/taslak/contact/` | `taslak/contact/index.html` | Taslak Contact & Support |

## Adding a new app

1. Create `<app>/` at the root.
2. Add `<app>/index.html`, `<app>/privacy/index.html`, `<app>/terms/index.html`, `<app>/contact/index.html`.
3. Reuse `/assets/style.css` — no per-app stylesheet required.
4. Link from root `index.html` under the **Apps** section.

## Stack

- Plain HTML — no build, no framework.
- Single shared stylesheet at `assets/style.css`.
- Google Fonts: Bricolage Grotesque (headings), IBM Plex Sans (body), IBM Plex Mono (code).
- Subtle CSS-only animations (fade-up on load, hover lifts).
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
