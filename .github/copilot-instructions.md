# Copilot Instructions for Fractal IT Website

## Project Overview
Acesta este un site profesional de servicii IT pentru Fractal IT SRL (service laptop, recuperare date și consultanță IT în Cluj-Napoca) construit cu Jekyll și tema remote **Feeling Responsive** (`remote_theme: Phlow/feeling-responsive`). Conținutul este 100% în limba română și structurat pe servicii principale (reparații, laptop, recuperare date, contact, despre).

## Architecture & Key Components

### Config Jekyll (`_config.yml`)
- Folosește `remote_theme: Phlow/feeling-responsive`
- `language: 'ro'`, permalink pattern: `/:categories/:title/`
- Paginare activă: `paginate: 5` în `blog/page:num`
- Plugins cheie: `jekyll-remote-theme`, `jekyll-paginate`, `jekyll-sitemap`, `jekyll-gist`, `jemoji`, `jekyll-include-cache`
- Metadate business (title, email, phone, address) plus descriere SEO în română
- Layout-uri standard: `page` pentru pagini, `post` pentru articole

### Structură Conținut
- `index.markdown` – landing principal (layout: `default` + subheadline/teaser)
- `servicii.markdown` – listă servicii IT (toc activ)
- `laptop.markdown` – reparații și întreținere laptop
- `recuperare-date.markdown` – recuperare HDD/SSD/RAID/Flash
- `contact.markdown` – formular mailto + detalii business + urgențe
- `about.markdown` – descriere companie, experiență 14+ ani
- `_posts/` – anunțuri și noutăți
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
Notă: Dacă apare eroare SSL la `jekyll-remote-theme`, pe GitHub Actions build-ul trece. Soluții locale: actualizați certificatele sistemului sau vopsiți tema local (clonați repo în `_themes/` și eliminați `remote_theme`).

Deploy (GitHub Pages + Actions):
- Workflow: `.github/workflows/jekyl.yaml` (build + deploy)
- Trigger: push pe `master`
- Domeniu: `CNAME` → `fractal.ro`
- Ruby pinned 3.3, runner `ubuntu-22.04`
- Build: `bundle exec jekyll build --baseurl "${{ steps.pages.outputs.base_path }}"`

### Dependențe (Gemfile)
- Core: `jekyll`
- Teme: remote via `jekyll-remote-theme` (nu există gem theme local)
- Plugin-uri: `jekyll-remote-theme`, `jekyll-paginate`, `jekyll-sitemap`, `jekyll-gist`, `jemoji`, `jekyll-include-cache`
- Eliminat: `minimal-mistakes-jekyll`, `jekyll-algolia` (nefolosit actualmente)

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
- Email: "contact@fractal.ro" 
- Address: "Ilie Măcelaru 26, Cluj-Napoca"
- Hours: "Luni – Vineri 9:00 – 17:30 | Sâmbătă 9:00 – 13:00"

### Pattern Layout Pagini
- `layout: default` pentru homepage
- `layout: page` pentru pagini statice
- `layout: post` pentru articole
- TOC manual prin structură heading (tema nu generează automat ca Minimal Mistakes)

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

Focus: păstrați consistența brandului, corectitudinea termenilor tehnici în română, claritatea serviciilor și integritatea datelor de contact. Evitați reintroducerea elementelor specifice Minimal Mistakes.