# Copilot Instructions for Fractal IT Website

## Project Overview
Acesta este un site profesional de servicii IT pentru Fractal IT SRL (service laptop, recuperare date și consultanță IT în Cluj-Napoca) construit cu Jekyll și tema **Minimal Mistakes** (gem `minimal-mistakes-jekyll`, skin `neon`). Conținutul este 100% în limba română și structurat pe servicii principale (reparații, laptop, recuperare date, contact, despre).

## Architecture & Key Components

### Config Jekyll (`_config.yml`)
- Theme: `minimal-mistakes-jekyll` (skin: `neon`)
- `locale: ro`, permalink: `/:categories/:title/`
- Paginare DEZACTIVATĂ momentan (nu există încă pagină blog). Pentru activare: adăugați `paginate` și `paginate_path` + creați pagină cu `layout: home`.
- Plugins: `jekyll-paginate` (inactiv fără cheile paginate), `jekyll-sitemap`, `jekyll-gist`, `jemoji`, `jekyll-include-cache`
- Metadate business (title, email, phone, address) + SEO description în română
- Defaults: `pages -> layout: page`, `posts -> layout: post`

### Structură Conținut
- `index.markdown` – landing principal (layout: `single`, conținut orientat servicii)
- `servicii.markdown` – listă servicii IT (layout: `single` / structură H2/H3 pentru TOC automat dacă se activează plugin JS)
- `laptop.markdown` – reparații și întreținere laptop (hardware + software)
- `recuperare-date.markdown` – recuperare HDD/SSD/RAID/Flash
- `contact.markdown` – formular mailto + detalii business + urgențe
- `about.markdown` – descriere companie, experiență peste 14 ani
- `_posts/` – noutăți (momentan un singur post activ). Fișiere *.bak NU trebuie păstrate.
- `_data/navigation.yml` – meniul principal (Acasă, Servicii, Laptop, Recuperare Date, Contact)

### Key Features & Patterns

#### Romanian Business Content
All content is in Romanian with technical terminology properly localized:
- Service descriptions use Romanian IT terminology
- Contact forms and CTAs in Romanian
- Business hours and location information in local format
- Professional tone suitable for B2B and B2C clients

#### Structură Orientată pe Servicii
- Pagini dedicate pentru categorii majore
- Tarif evaluare vizibil: **50 lei**
- Secțiuni pentru urgențe și consultanță
- Specializări hardware (reballing, recuperare date, înlocuire componente)

#### Integrare Contact
- Telefon, email, adresă, program afișate consecvent
- Formular rapid (mailto) fără backend
- Secțiune urgențe (accent pe telefon)

### Flux Dezvoltare & Deploy
Local:
```bash
bundle install
bundle exec jekyll serve
```
Notă: Dependințe strict locale (fără remote theme) — nu mai există risc de erori SSL la fetch remote.

Deploy (GitHub Pages + Actions):
- Workflow: `.github/workflows/jekyl.yaml` (build + deploy)
- Trigger: push pe `master`
- Domeniu: `CNAME` → `fractal.ro`
- Ruby pinned 3.3, runner `ubuntu-22.04`
- Build: `bundle exec jekyll build --baseurl "${{ steps.pages.outputs.base_path }}"`

### Dependențe (Gemfile)
- Core: `jekyll`
- Theme: `minimal-mistakes-jekyll`
- Plugins: `jekyll-paginate`, `jekyll-sitemap`, `jekyll-gist`, `jemoji`, `jekyll-include-cache` (se poate elimina `jekyll-paginate` dacă nu se folosește blog)
- Eliminat: `jekyll-remote-theme`, `jekyll-algolia` (neutilizat)

## Project-Specific Conventions

### Romanian Content Standards
- All customer-facing content must be in Romanian
- Technical terms should use proper Romanian IT terminology
- Contact information must include Romanian phone format and address
- Service descriptions should be professional but accessible

### Business Information Consistency
- Company name: "Fractal IT SRL" 
- Established: 2011 (reference "peste 14 ani de experiență")
- Phone: "0747-99.66.77" (clickable tel: links)
- Email: "office@fractal.ro" 
- Address: "Ilie Măcelaru 26, Cluj-Napoca"
- Hours: "Luni – Vineri 9:00 – 17:30 | Sâmbătă Închis"

### Pattern Layout Pagini
- Homepage: `layout: single` (marketing + CTA). Alternativ se poate folosi `layout: splash`.
- Pagini statice: `layout: single` sau fallback la default (`page` din defaults) în funcție de nevoie.
- Articole: `layout: post` (default prin `defaults`)
- TOC: se poate activa per pagină cu `toc: true` + structură corectă heading (H2/H3)

### Prezentare Servicii
- Tarif evaluare fix: 50 lei
- Secțiuni separate hardware / software / recuperare date
- Blocuri call-to-action la finalul paginilor tehnice

### Imagini & Media
- Imagini în `/assets/images/`
- `teaser` și `subheadline` pentru homepage
- Se pot adăuga favicon & og:image ulterior

### SEO and Accessibility
- Romanian meta descriptions and titles
- Proper heading hierarchy (H1, H2, H3)
- Alt text for images in Romanian
- Local business schema markup opportunities

Focus: păstrați consistența brandului, corectitudinea termenilor tehnici în română, claritatea serviciilor și integritatea datelor de contact. Evitați reintroducerea configurărilor pentru teme remote inutile.

## Note Operaționale
1. Elimină fișiere CSS redundante: păstrează doar `assets/css/main.scss` (compilează în `main.css`). Nu păstra un `assets/css/main.css` sursă concomitent.
2. Nu comite fișiere *.bak în `_posts/` – pot genera warnings.
3. Pentru blog/paginare: creează `blog/index.md` cu `layout: home` și reactivează cheile paginate.
4. Optimize SEO: asigură meta description concisă (<155 caractere) și alt text descriptiv imaginilor.
5. Pentru CTA mai vizibile se pot folosi include-uri `feature_row` din Minimal Mistakes (adăugă secțiune YAML în front matter și `{% include feature_row %}`).

## Extensii Posibile
- Adaugă `jekyll-feed` dacă se dorește RSS.
- Adaugă favicon + og:image în `/assets/images/` și configurează în `_includes/head/custom.html` (crează fișier dacă lipsește).
- Schema.org LocalBusiness: include JSON-LD în același `custom.html`.

Document actualizat pentru tema Minimal Mistakes (rollback de la Feeling Responsive) – mențineți această versiune sincronizată cu config-ul.