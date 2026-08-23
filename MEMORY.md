# Portfolio - Putra Agustiansyah

## Owner
- Nama: Putra Agustiansyah
- Role: Junior Web Developer (Technical Writer | System Administrator | Web Development)
- GitHub: @putragstn
- Email: putraagustiansyah000@gmail.com
- Deploy: https://putragstn.github.io/

## Tech Stack
- HTML5, CSS3, JavaScript (vanilla, no framework)
- Bootstrap 5.3.3 (local)
- Font Awesome 6.5.1 (CDN)
- AOS 2.3.4 (CDN, scroll animation)
- Google Fonts — IBM Plex Sans Condensed (navbar brand)
- Popper.js 2.11.8 (CDN, Bootstrap dependency)

## Struktur File
```
portofolio/
├── index.html          # Single page, semua section
├── css/style.css       # Custom styling + responsive
├── js/script.js        # Image carousel (auto-rotate + pause on hover)
├── img/
│   ├── foto/           # Foto profil (1786961438155.jpg)
│   ├── icons/          # Tech stack icons + favicon
│   └── projects/       # Screenshot project (~13 gambar)
├── bootstrap-5.3.3/    # Bootstrap lokal (css + js)
├── DESIGN.md           # Arsitektur, dependency, flow diagram
└── MEMORY.md           # File ini
```

## Section (urutan di HTML)
1. **Navbar** — fixed-top, responsive collapse, auto-close + smooth scroll di mobile
2. **Jumbotron** (`#home`) — foto profil, nama, subtitle, 4 social links (email, linkedin, instagram, github)
3. **About Me** (`#about`) — 2 kolom bio + Steve Jobs quote
4. **My Projects** (`#my-projects`) — 3 project cards dengan image carousel
5. **TechStack** (`#techstack`) — 7 icon grid (HTML, CSS, JS, Bootstrap, PHP, Laravel, Figma)
6. **My Notes** (`#my-notes`) — 3 card placeholder (belum ada konten)
7. **Footer** — social links + copyright 2026

## Image Carousel (js/script.js)
- 3 card, masing-masing array gambar: card-1 (5 img), card-2 (5 img), card-3 (3 img)
- `setInterval` per card dengan interval berbeda (4s, 3s, 5s)
- Rotate via modulo: `currentIndex = (currentIndex + 1) % length`
- **Pause on hover**: mouseenter clearInterval, mouseleave restart setInterval
- Tidak ada manual navigation (prev/next/indicator)

## Project yang Ditampilkan
1. **Sistem Informasi Keuangan** — Laravel 10, SB Admin template. Kelola keuangan, karyawan, hutang.
2. **Admin Landing Page** — Laravel 10, SB Admin 2. Customisasi konten landing page.
3. **Landing Page Cemerlang Key** — HTML, CSS, Bootstrap 5. Info layanan UMKM.

## Responsive Strategy
- Satu breakpoint: `@media (min-width: 992px)` (desktop)
- Mobile-first sizing: foto 150px, nama 30px, subtitle 18px
- Desktop: foto 200px, nama 36px, subtitle 24px
- Bootstrap grid: `col-md-4 col-lg-6` (cards), `col-lg-2 col-md-3 col-sm-4 col-6` (techstack)
- Smooth scroll + `scroll-padding-top: 80px` (120px di mobile)

## Color Scheme
- Primary: `bg-primary` Bootstrap (biru) — navbar, footer
- Section alternating: `#c7ddff` — jumbotron, projects, notes
- Cards: white (Bootstrap default)

## SEO & Meta
- `og:title`, `description`, `canonical` → `putragstn.github.io`
- `robots: index, follow`

## Local Development
- `python3 -m http.server 8001` → `http://localhost:8001`

## Preferensi User
- Ponytail mode: full
- Bahasa komunikasi: Indonesia
- **Workflow**: Review/rangkuman dulu, tunggu approval, baru eksekusi.
