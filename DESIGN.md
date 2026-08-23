# Design Document — Portfolio Putra Agustiansyah

## Arsitektur

Static single-page site. Deploy di GitHub Pages (`putragstn.github.io`).

```
Browser → index.html → Bootstrap + AOS + Font Awesome (CDN/local)
                     → css/style.css (custom)
                     → js/script.js (carousel)
                     → Contact form → Google Apps Script
```

Tidak ada build step, tidak ada bundler, tidak ada framework JS.

## Struktur Halaman

```
┌─────────────────────────────────┐
│  Navbar (fixed-top, collapse)   │
├─────────────────────────────────┤
│  Jumbotron — foto, nama, social │
├─────────────────────────────────┤
│  About Me — 2 kolom bio + quote │
├─────────────────────────────────┤
│  My Projects — 3 card carousel  │
├─────────────────────────────────┤
│  TechStack — 7 icon grid        │
├─────────────────────────────────┤
│  Contact — form → GAS           │
├─────────────────────────────────┤
│  Footer — social + copyright    │
└─────────────────────────────────┘
```

Semua section di `index.html`. Anchor nav: `#home`, `#about`, `#my-projects`, `#techstack`, `#contact`. Smooth scroll via `html { scroll-behavior: smooth }`.

## Dependency

| Library | Versi | Load | Fungsi |
|---------|-------|------|--------|
| Bootstrap | 5.3.3 | **Local** (`bootstrap-5.3.3/`) | Grid, navbar, cards, form, alert |
| Font Awesome | 6.5.1 | CDN (CSS + JS) | Icon social, heart |
| AOS | 2.3.4 | CDN (CSS + JS) | Scroll animation (fade-up, zoom-in, fade-right) |
| Google Fonts | — | CDN | IBM Plex Sans Condensed (navbar brand) |
| Popper.js | 2.11.8 | CDN | Bootstrap dropdown dependency |

**Catatan:** Bootstrap di-load lokal, yang lain CDN. Ada duplikasi — Bootstrap juga tersedia via CDN. Bisa migrasi semua ke CDN atau hapus folder lokal.

## Image Carousel

`js/script.js` — mekanisme:

- 3 card, masing-masing punya array gambar (`imageList1/2/3`)
- `setInterval` per card dengan interval berbeda (4s, 3s, 5s)
- Rotate gambar dengan modulo: `currentIndex = (currentIndex + 1) % length`
- Gambar default di HTML di-overwrite oleh JS pada interval pertama

**Flow:**
```
HTML <img id="card-1" src="default.jpg">
  ↓
JS: setInterval(changeImageCard1, 4000)
  ↓
setelah 4s: src = imageList1[0], index = 1
setelah 4s: src = imageList1[1], index = 2
...
setelah 4s: src = imageList1[4], index = 0 (loop)
```

Tidak ada pause on hover, tidak ada manual navigation. Pure auto-rotate.

## Contact Form Flow

```
<form name="putra-contact-form">
  ↓ submit event (preventDefault)
  ↓ toggle: hide btn-kirim, show btn-loading
  ↓ fetch POST → Google Apps Script URL
  ↓ body: new FormData(form)
  ↓ success: toggle buttons back, show alert, reset form
  ↓ error: console.error
```

Backend: Google Apps Script webhook (`script.google.com/macros/s/.../exec`). Form data masuk ke Google Sheets. Tidak ada validasi client-side selain `type="email"`.

## Responsive Strategy

CSS `@media (min-width: 992px)` — satu breakpoint desktop.

| Elemen | Mobile (<992px) | Desktop (≥992px) |
|--------|----------------|------------------|
| Foto jumbotron | 150px | 200px |
| Display-4 (nama) | 30px | 36px |
| Lead (subtitle) | 18px | 24px |
| About text | 18px | 24px |
| Project card img | 250px | 285px |
| Quote box | 300px | 800px |
| Navbar hover | — | border-bottom 3px |

Bootstrap grid handle layout: `col-md-4 col-lg-6` untuk cards, `col-lg-2 col-md-3 col-sm-4 col-6` untuk techstack.

## Asset Organization

```
img/
├── foto/
│   └── 1786961438155.jpg          # Foto profil (jumbotron)
├── icons/
│   ├── favicon.png
│   ├── html.png, css-3.png, js.png, bootstrap-5.png
│   ├── php.png, icon-laravel.png, figma.png
│   └── (social icons via Font Awesome)
├── projects/
│   ├── sistem-informasi-keuangan.jpg, login-sik.png, cb-*.png
│   ├── admin-landing-page.jpg, login-cemerlang-key.png, galeri-ck.png, ...
│   └── landing-page_cemerlang-key.jpg, ck-*.png
└── stevejobs (2).jpg               # Quote section
```

Total: 1 foto profil, 7 tech icons, ~13 project screenshots, 1 quote image.

## Color Scheme

- Primary: `bg-primary` Bootstrap (biru) — navbar, footer
- Section alternating: `#c7ddff` — jumbotron, projects, contact
- Text: default Bootstrap dark
- Cards: white background (Bootstrap default)

## SEO & Meta

- `og:title`, `description`, `canonical` → `putragstn.github.io`
- `robots: index, follow`
- Title: "Portfolio | Putra Agustiansyah"

## Observasi & Potensi Improvements

1. **Bootstrap lokal vs CDN** — folder `bootstrap-5.3.3/` bisa dihapus, ganti ke CDN. Mengurangi repo size.
2. **Carousel tanpa kontrol** — tidak ada pause, prev/next, atau indicator. User tidak bisa explore screenshot secara manual.
3. **Form validation minimal** — hanya `type="email"`. Tidak ada required attribute, tidak ada client-side check.
4. **Duplicate social links** — jumbotron dan footer punya social links yang sama. Bisa extract ke partial atau cukup di footer.
5. **Hardcoded content** — semua data (nama, project, social) hardcoded di HTML. Jika sering update, bisa pertimbangkan data-driven approach (JSON + JS render).
