# Dandelion Wishes Counseling — Static Site Design Spec

## Goal

Convert the approved Squarespace design into a fully self-contained static HTML site hosted on Cloudflare Pages via GitHub.

## Architecture

Pure static HTML — no build tools, no framework, no Node.js. Six content pages plus a blog section. All pages share the same nav and footer via copy-paste (no JS includes). Deployed to Cloudflare Pages by pushing to a GitHub repository's `main` branch.

## File Structure

```
dandelionwishes/
├── index.html              ← Home
├── about.html
├── services.html
├── faq.html
├── contact.html
├── 404.html                ← Custom error page (branded, links home)
├── robots.txt
├── sitemap.xml
├── blog/
│   ├── index.html          ← Blog listing page (hand-maintained)
│   └── posts/
│       ├── _template.html  ← Copy this to create a new post
│       └── (one .html file per blog post)
├── css/
│   └── dandelion-wishes.css  ← Unified stylesheet
└── images/
    ├── logo.png
    ├── hero.jpg
    ├── cat-headshot.jpg
    └── (service photos — to be provided by Cat)
```

## CSS

Based on the existing `css/dandelion-wishes.css` design system, cleaned up for a standard HTML context:

- Google Fonts loaded via `<link>` in `<head>` — no Squarespace workaround needed
- Class names without `dw-` prefix — we control all HTML, no collision risk
- Squarespace-specific overrides removed
- Design tokens preserved exactly: `#f4c430` gold, `#7a9e7e` sage, `#fffdf0` cream, `#3d3028` dark, `#5a4a3a` body

## HTML Pages

Each page is a complete HTML5 document with:
- `<head>`: charset, viewport, title, meta description, Google Fonts `<link>`, `dandelion-wishes.css` `<link>`, JSON-LD schema (home page only)
- Nav: logo + 5 nav links + Contact gold pill button, copy-pasted across all pages
- Page content: built from approved mockups in `.superpowers/brainstorm/922-1774567168/`
- Footer: practice name, address, phone, email, nav links, copyright, copy-pasted across all pages

### Mobile Nav

On screens below 768px, the nav collapses to a CSS-only hamburger menu using a hidden `<input type="checkbox">` toggle — no JavaScript. The nav links stack vertically in a dropdown panel. The Contact pill button remains visible at all widths.

### Page inventory

| File | Source mockup | Notes |
|------|--------------|-------|
| `index.html` | `homepage-layout-v3.html` | Hero, services cards (photo placeholders), about snippet, bottom CTA |
| `about.html` | `about-page-v3.html` | Bio, credential badges, philosophy grid, bottom CTA |
| `services.html` | `services-fees-page.html` | 3 alternating service rows, fees section, GFE disclosure, bottom CTA |
| `faq.html` | `faq-page.html` | 3 accordion groups (native `<details>`/`<summary>` — no JS needed) |
| `contact.html` | `contact-page-v2.html` | HIPAA notice, Simple Practice embed placeholder, contact info sidebar |
| `blog/index.html` | `blog-page.html` | Featured post + 3-column grid, hand-maintained |
| `404.html` | — | Branded error page: warm cream background, nav, "Page not found" message, link home |

## Blog Workflow

Each blog post is a standalone `blog/posts/slug.html` file. When Cat publishes a new post:
1. Copy `blog/posts/_template.html` to `blog/posts/post-slug.html`
2. Fill in: post title, date, category, body content
3. Add a card to the top of `blog/index.html` (new post becomes the featured post, previous featured moves to the grid)
4. Push to GitHub → Cloudflare Pages deploys automatically

### Blog post template sections

`_template.html` contains:
- Full `<head>` with placeholder title/meta description
- Nav (copy-pasted, same as all pages)
- Post header: title (h1), date, category label
- Post body: content area with heading and paragraph styles
- Back link: "← Back to Resources" linking to `/blog/`
- Footer (copy-pasted, same as all pages)

No CMS, no build step.

## Contact Form

Simple Practice embed (or equivalent) goes in `contact.html`. The file will contain a clearly commented placeholder:

```html
<!-- SIMPLE PRACTICE EMBED: paste your embed code here -->
<!-- https://simplepractice.com/embed-instructions -->
```

No custom form backend needed.

## Images

Download from Squarespace CDN and serve locally under `images/`:

| File | Source |
|------|--------|
| `logo.png` | Squarespace CDN (existing asset) |
| `hero.jpg` | Squarespace CDN (child + dandelion photo) |
| `cat-headshot.jpg` | Squarespace CDN (Cat's photo) |
| `child-therapy.jpg` | To be sourced by Cat |
| `teen-therapy.jpg` | To be sourced by Cat |
| `parent-coaching.jpg` | To be sourced by Cat |

## FAQ Accordion

Use native HTML `<details>`/`<summary>` elements — no JavaScript needed. CSS styles the open/close state via `details[open]` selector. Matches the accordion visual from the mockup.

## SEO

Per-page `<title>` and `<meta name="description">` values come from `seo/page-seo-reference.md`. **Note:** that document was written for Squarespace — ignore its setup instructions and Squarespace-specific sitemap note. Use only the title/description/slug/NAP data tables.

- JSON-LD LocalBusiness schema injected in `<head>` of `index.html` only (from `code-blocks/schema-markup.html`)
- `sitemap.xml` hand-authored at launch, standard `<urlset>` format:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url><loc>https://dandelionwishescounseling.com/</loc></url>
  <url><loc>https://dandelionwishescounseling.com/about</loc></url>
  <url><loc>https://dandelionwishescounseling.com/services</loc></url>
  <url><loc>https://dandelionwishescounseling.com/faq</loc></url>
  <url><loc>https://dandelionwishescounseling.com/blog/</loc></url>
  <url><loc>https://dandelionwishescounseling.com/contact</loc></url>
</urlset>
```

Add blog post URLs as posts are published.

- `robots.txt` content:

```
User-agent: *
Disallow:
Sitemap: https://dandelionwishescounseling.com/sitemap.xml
```

## Cloudflare Pages Deployment

- GitHub repo: `dandelionwishes` (to be created)
- Branch: `main`
- Build command: *(leave blank — no build step)*
- Output directory: *(leave blank — deploys from repo root)*
- Custom domain: `dandelionwishescounseling.com` (configured in Cloudflare DNS)

Cloudflare Pages strips `.html` extensions automatically — `about.html` is served at `/about`, `services.html` at `/services`, etc. No redirect rules needed. The sitemap uses these clean URLs.

## What Cat Still Needs to Provide

- 3 service photos (child therapy, teen therapy, parent coaching)
- Office hours
- Insurance accepted list
- FAQ answers (9 questions across 3 groups)
- Telehealth availability (yes/no)
- Updated bio text
- Simple Practice embed code
- At least 1 blog post for launch
