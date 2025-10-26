# Copilot Instructions for Fractal IT Website

## Project Overview
This is a Jekyll-based professional IT services website for Fractal IT SRL, a laptop repair and IT consulting company in Cluj-Napoca, Romania. Built using the Minimal Mistakes theme with a "neon" skin, the site features comprehensive Romanian-language content for IT services, laptop repairs, data recovery, and business consulting.

## Architecture & Key Components

### Jekyll Configuration (`_config.yml`)
- Uses `minimal-mistakes-jekyll` theme with "neon" skin
- Custom branding: Fractal IT with logo at `/assets/images/fractal_logo.png`
- Site URL: `https://fractal.ro`
- Feed disabled (`atom_feed.hide: true`)
- Romanian language content with business contact information
- Custom footer with company details and contact info

### Content Structure
- **Homepage** (`index.markdown`): Main business landing page with services overview and contact CTA
- **Services** (`servicii.markdown`): Comprehensive IT services listing with technical details
- **Laptop Repairs** (`laptop.markdown`): Specialized laptop repair services and hardware fixes
- **Data Recovery** (`recuperare-date.markdown`): Professional data recovery for HDD/SSD/RAID systems
- **Contact** (`contact.markdown`): Multi-modal contact page with business hours and location
- **About** (`about.markdown`): Company history and team expertise
- **Posts** (`_posts/`): Business announcements and IT service updates
- **Navigation** (`_data/navigation.yml`): Multi-page business navigation structure

### Key Features & Patterns

#### Romanian Business Content
All content is in Romanian with technical terminology properly localized:
- Service descriptions use Romanian IT terminology
- Contact forms and CTAs in Romanian
- Business hours and location information in local format
- Professional tone suitable for B2B and B2C clients

#### Service-Oriented Structure
- Detailed service pages with technical specifications
- Clear pricing transparency (50 lei evaluation fee)
- Professional consultation and emergency service options
- Hardware repair specializations (reballing, component replacement)

#### Contact Integration
- Multiple contact methods (phone, email, physical location)
- Business hours clearly displayed
- Emergency contact options for urgent repairs
- Physical address: "Ilie Măcelaru 26, Cluj-Napoca"

## Development Workflows

### Local Development
```bash
bundle exec jekyll serve
```

### Deployment
- GitHub Actions workflow (`.github/workflows/jekyl.yaml`)
- Deploys to GitHub Pages on `master` branch pushes
- Uses Ruby 3.3 with ubuntu-22.04 runner
- Build command: `bundle exec jekyll build --baseurl "${{ steps.pages.outputs.base_path }}"`

### Dependencies (Gemfile)
- Core: `jekyll` + `minimal-mistakes-jekyll`
- Plugins: `jekyll-paginate`, `jekyll-sitemap`, `jekyll-gist`, `jemoji`, `jekyll-include-cache`, `jekyll-algolia`
- Note: `jekyll-feed` is commented out (matches config)

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

### Page Structure Patterns
- All main pages use `layout: single` with header overlays
- Service pages include table of contents (`toc: true`)
- Contact CTAs consistently placed at page bottoms
- Footer includes complete business information and copyright

### Service Presentation
- Evaluation fee clearly stated: "50 lei"
- Emergency services highlighted for urgent repairs
- Technical services grouped by expertise (hardware, software, data recovery)
- Professional consultation available for both individuals and businesses

### Image Management
- Business photos stored in `/assets/images/`
- Header overlays for professional appearance
- Consistent image sizing and optimization for web

### SEO and Accessibility
- Romanian meta descriptions and titles
- Proper heading hierarchy (H1, H2, H3)
- Alt text for images in Romanian
- Local business schema markup opportunities

When working on this project, prioritize professional Romanian business presentation, maintain accurate contact information, ensure mobile responsiveness for local customers, and preserve the technical credibility needed for IT service trust.