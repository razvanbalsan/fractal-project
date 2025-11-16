# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a professional IT services website for **Fractal IT SRL**, a laptop repair and data recovery business based in Cluj-Napoca, Romania. The site is built with **Jekyll 4.x** using the **Minimal Mistakes** theme (gem-based, skin: `air`). All content is in Romanian and structured around core services: laptop repairs, data recovery, consultation, and contact.

## Development Commands

### Local Development
```bash
# Install dependencies
bundle install

# Serve locally with live reload
bundle exec jekyll serve

# Build for production
bundle exec jekyll build

# Build with specific baseurl (matches GitHub Actions)
bundle exec jekyll build --baseurl ""
```

### Deployment
- **Platform**: GitHub Pages via GitHub Actions
- **Workflow**: `.github/workflows/jekyl.yaml`
- **Trigger**: Push to `master` branch
- **Custom Domain**: `fractal.ro` (configured via `CNAME`)
- **Ruby Version**: 3.3 (pinned in workflow)
- **Runner**: ubuntu-22.04

## Architecture Overview

### Theme Configuration
- **Theme**: `minimal-mistakes-jekyll` (gem-based, NOT remote theme)
- **Skin**: `air` (defined in `_config.yml`)
- **Locale**: `ro` (Romanian)
- **Permalink Structure**: `/:categories/:title/`

### Key Configuration Points (`_config.yml`)
- Business metadata: title, email, phone, address embedded in config
- Pagination is **DISABLED** (no blog page exists yet)
- To enable blog: create `blog/index.md` with `layout: home`, add `paginate: 5` and `paginate_path: "blog/page:num"` to config
- Social sharing: Facebook and email only
- Footer includes copyright and business info

### Content Structure
- **Homepage** (`index.markdown`): `layout: single`, service-oriented landing page with FAQ and CTAs
- **Service Pages**:
  - `servicii.markdown` - IT services overview
  - `laptop.markdown` - Laptop repair and maintenance
  - `recuperare-date.markdown` - Data recovery (HDD/SSD/RAID/Flash)
  - `contact.markdown` - Contact form (mailto) + business details + emergencies
  - `about.markdown` - Company description (14+ years experience)
- **Blog Posts**: `_posts/` directory (currently one active post; `.bak` files should NOT be committed)
- **Navigation**: `_data/navigation.yml` - main menu (Acasă, Servicii, Laptop, Recuperare Date, Contact)

### Custom Includes & Assets
- **Custom head**: `_includes/head/custom.html` - for favicon, og:image, schema.org markup
- **Custom footer**: `_includes/footer.html`
- **Custom social share**: `_includes/social-share-custom.html`
- **CSS**: `assets/css/main.scss` compiles to `main.css` (do NOT maintain both source and compiled versions)
- **Critical CSS**: `assets/css/critical.css` for performance

### Excluded Files (from build)
- `*.bak` files (avoid committing these from `_posts/`)
- Standard Jekyll excludes: vendor, node_modules, etc.
- Source JS/CSS assets that are compiled

## Business Information (Consistency Required)

All instances must match these exact values:
- **Company**: Fractal IT SRL
- **Established**: 2011 (reference as "peste 14 ani de experiență")
- **Phone**: 0747-99.66.77 (use `tel:0747996677` for links)
- **Email**: office@fractal.ro
- **Address**: Ilie Măcelaru 26, Cluj-Napoca
- **Hours**: Luni – Vineri 8:30 - 17:00 | Sâmbătă Închis
- **Evaluation Fee**: 50 lei (fixed, deducted from service cost if accepted)

## Romanian Content Standards

### Language Requirements
- All customer-facing content MUST be in Romanian
- Use proper Romanian IT terminology (e.g., "laptop" not "notebook", "placă de bază" not "motherboard")
- Professional but accessible tone suitable for both B2B and B2C
- Technical descriptions should be clear and specific

### Service Presentation Patterns
- Emphasize transparency and repair-focused approach (not unnecessary replacement)
- Highlight board-level repair capabilities (reballing BGA, SMD component replacement)
- Include specific symptoms and solutions
- Call-to-action blocks at end of technical pages

## SEO and Content Optimization

### SEO Expert Mode (from copilot instructions)
When writing or optimizing content, adopt this three-part analysis:
1. **Keyword and Intent Strategy**: Identify primary/secondary keywords and user intent
2. **On-Page Content Optimization**: H1/title tags, meta descriptions (<155 chars), internal linking, content depth
3. **Technical & Off-Page**: Core Web Vitals, indexation, backlinks, E-E-A-T signals

### Human Voice Writing Guidelines
- **Variable style**: Mix long complex sentences with short punchy ones (high "burstiness")
- **Conversational tone**: Use contractions, natural flow (avoid robotic uniformity)
- **Authentic emotion**: Full spectrum including ambivalence and sarcasm where appropriate
- **Unique phrasing**: Prioritize less probable word choices to increase "perplexity"
- Avoid clichés, corporate jargon, repetition

### Content Standards
- Proper heading hierarchy (H1, H2, H3)
- Romanian meta descriptions and titles
- Alt text for images in Romanian
- TOC can be enabled per-page with `toc: true` in front matter

## Layout Patterns

### Page Layouts
- **Homepage**: `layout: single` (or optionally `splash` for marketing)
- **Static pages**: `layout: single` or fallback to `page` (default)
- **Blog posts**: `layout: post` (default via config)
- **TOC activation**: Set `toc: true` in front matter + use proper H2/H3 structure

### Feature Rows
For prominent CTAs, use Minimal Mistakes `feature_row` includes:
- Add YAML section to front matter defining features
- Insert `{% include feature_row %}` in content
- See Minimal Mistakes documentation for syntax

## Important Operational Notes

### File Management
1. **CSS**: Keep only `assets/css/main.scss` as source; do NOT maintain both `.scss` and `.css` versions
2. **Backup files**: NEVER commit `*.bak` files from `_posts/` (causes warnings)
3. **Remote theme**: Do NOT reintroduce `jekyll-remote-theme` - use gem-based theme only (avoids SSL fetch errors)

### Blog/Pagination Setup (Currently Inactive)
To activate:
1. Create `blog/index.md` with `layout: home`
2. Add to `_config.yml`:
   ```yaml
   paginate: 5
   paginate_path: "blog/page:num"
   ```
3. `jekyll-paginate` plugin is already included but inactive without these settings

### Performance & Security Headers
- Custom headers defined in `_headers` file
- See `performance-optimization-headers.md` for implementation details

## Plugins

### Active Plugins (in Gemfile and _config.yml)
- `jekyll-paginate` (inactive until blog page created)
- `jekyll-sitemap`
- `jekyll-gist`
- `jemoji`
- `jekyll-include-cache`

### Previously Removed (Do Not Re-Add)
- `jekyll-remote-theme` (switched to gem-based theme)
- `jekyll-algolia` (unused)

### Optional Future Additions
- `jekyll-feed` (for RSS if blog becomes active)
- Favicon + og:image setup via `_includes/head/custom.html`
- Schema.org LocalBusiness JSON-LD in same custom.html

## Git Workflow

- **Main branch**: `master`
- **Deployment**: Automatic via GitHub Actions on push to master
- **Domain**: Custom domain `fractal.ro` configured via CNAME
- Commit messages should be concise and in English

## Key Technical Patterns

### Email Obfuscation
Homepage uses JavaScript-based email obfuscation:
```javascript
// Splits email into data attributes to prevent scraping
data-u="office" data-d="fractal.ro"
// Reconstructed on page load
```

### Contact Forms
- Uses `mailto:` links (no backend form processing)
- Emergency contact section emphasizes phone calls
- Form includes all business details and hours

### Image Optimization
- Use WebP format where possible (e.g., `IMG_1376.webp`, `IMG_1378.webp` in root)
- Store images in `/assets/images/`
- Include Romanian alt text for accessibility

## Specialized Service Focus

### Board-Level Repair Expertise
This business specializes in **electronic board-level repairs**, not just component replacement:
- BGA reballing/rework (GPU, PCH, chipsets)
- Power rail diagnostics (buck/boost circuits, short isolation)
- SMD component replacement (MOSFETs, regulators, controllers)
- BIOS/EC firmware reprogramming
- Thermal profiling and stability validation

When writing content about services, emphasize these advanced capabilities and the diagnostic methodology.

### Service Pricing Model
- **Evaluation fee**: Fixed 50 lei
- **Policy**: Fee is deducted from repair cost if customer accepts the work
- **Transparency**: No hidden fees; quotes provided before work begins
- **Warranty**: 90 days standard for labor

## Dependencies Management

### Critical Dependency Notes
- Jekyll version is NOT pinned in Gemfile (uses latest)
- Theme version is NOT pinned (uses latest gem)
- Ruby 3.3 is pinned in GitHub Actions workflow
- All plugins are in `group :jekyll_plugins` block

### When Adding New Dependencies
1. Add to Gemfile in appropriate group
2. If it's a Jekyll plugin, also add to `plugins:` array in `_config.yml`
3. Run `bundle install` locally
4. Test with `bundle exec jekyll serve` before committing
