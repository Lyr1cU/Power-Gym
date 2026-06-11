# Power Gym

**Demo website for a fitness gym** — a single-page landing with a bilingual interface (UA / EN), responsive layout, and a backend-free content management panel.

**Live:** [lyr1cu.github.io/Power-Gym](https://lyr1cu.github.io/Power-Gym/)

---

## About the project

Power Gym is a portfolio project: a full website for a real gym in Dnipro, Ukraine (1b Mira Ave). The goal was to turn a universal template into a convincing product for a specific business — new palette, content, section structure, and a CMS for the owner.

The site has no application server: content lives in JSON files, deployment is static hosting on GitHub Pages.

> Photos and some copy are demo placeholders (stock). In production they are replaced with the client’s own assets.

---

## For site visitors

| Section | Contents |
|---------|----------|
| **Hero** | Main screen with a free trial call-to-action |
| **About** | Four feature cards highlighting the gym |
| **Memberships** | Plans, coaches, and programs — tabbed layout |
| **Gallery** | Gym photos with lightbox |
| **Reviews** | Client testimonial slider |
| **Contact** | Address, hours, map, booking form, social links |

Language switch **UA / EN** is in the header, with no full page reload.

---

## For recruiters and clients

### What’s included

- Responsive layout: desktop, tablet, mobile (burger menu)
- Dark UI theme aligned with the gym brand (graphite + `#FFD400` accent)
- Content separated from markup — JSON + i18n
- **Decap CMS** — edit memberships, gallery, reviews, and contacts in the browser
- CI/CD: push to `main` → GitHub Actions → GitHub Pages
- OAuth via a Vercel proxy for production admin login
- Form with client-side validation, Google Maps embed for the address

### Stack

| Layer | Technologies |
|-------|----------------|
| Markup / styles | HTML5, CSS3 (custom properties, Grid, Flexbox) |
| Logic | Vanilla JavaScript (ES modules) |
| Content | JSON, Decap CMS |
| Deployment | GitHub Pages, GitHub Actions |
| Media | WebP |

No React, Vue, or bundlers — a deliberate choice for a lightweight, fast static site.

### Architecture (overview)

```
index.html          — sections + data-i18n for UI strings
content/*.json      — memberships, gallery, reviews, contacts
js/i18n/            — UA / EN translations
js/render/          — JSON-to-DOM rendering
admin/              — Decap CMS
.github/workflows/  — auto-deploy
```

---

## Links

| | URL |
|---|-----|
| Website | https://lyr1cu.github.io/Power-Gym/ |
| Admin (CMS) | https://lyr1cu.github.io/Power-Gym/admin/ |

---

## Local development

```bash
python -m http.server 8080
```

→ http://localhost:8080

For the admin panel locally: `npx decap-server` plus the same HTTP server → `/admin/`

---

## Author

[GitHub — Lyr1cU](https://github.com/Lyr1cU)
