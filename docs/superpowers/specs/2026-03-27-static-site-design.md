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
├── blog/
│   ├── index.html          ← Blog listing page (hand-maintained)
│   └── posts/
│       └── (one .html file per blog post)
├── css/
│   └── style.css           ← Unified stylesheet
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
- `<head>`: charset, viewport, title, meta description, Google Fonts `<link>`, `style.css` `<link>`, JSON-LD schema (home page only)
- Nav: logo + 5 nav links + Contact gold pill button, copy-pasted across all pages
- Page content: built from approved mockups in `.superpowers/brainstorm/922-1774567168/`
- Footer: practice name, address, phone, email, nav links, copyright, copy-pasted across all pages

### Page inventory

| File | Source mockup | Notes |
|------|--------------|-------|
| `index.html` | `homepage-layout-v3.html` | Hero, services cards (photo placeholders), about snippet, bottom CTA |
| `about.html` | `about-page-v3.html` | Bio, credential badges, philosophy grid, bottom CTA |
| `services.html` | `services-fees-page.html` | 3 alternating service rows, fees section, GFE disclosure, bottom CTA |
| `faq.html` | `faq-page.html` | 3 accordion groups (native `<details>`/`<summary>` — no JS needed) |
| `contact.html` | `contact-page-v2.html` | HIPAA notice, Simple Practice embed placeholder, contact info sidebar |
| `blog/index.html` | `blog-page.html` | Featured post + 3-column grid, hand-maintained |

## Blog Workflow

Each blog post is a standalone `blog/posts/slug.html` file. When Cat publishes a new post:
1. Create `blog/posts/slug.html` from a post template
2. Add a card to the top of `blog/index.html` (new post becomes the featured post)
3. Push to GitHub → Cloudflare Pages deploys automatically

No CMS, no build step. The post template will be included as `blog/posts/_template.html`.

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

- Per-page `<title>` and `<meta name="description">` from `seo/page-seo-reference.md`
- JSON-LD LocalBusiness schema injected in `<head>` of `index.html` only
- Cloudflare Pages serves a `sitemap.xml` — to be hand-authored at launch
- `robots.txt` permitting all crawlers

## Cloudflare Pages Deployment

- GitHub repo: `dandelionwishes` (to be created)
- Branch: `main`
- Build command: none (static HTML, no build step)
- Output directory: `/` (root)
- Custom domain: `dandelionwishescounseling.com` (configured in Cloudflare DNS)

## What Cat Still Needs to Provide

- 3 service photos (child therapy, teen therapy, parent coaching)
- Office hours
- Insurance accepted list
- FAQ answers (9 questions across 3 groups)
- Telehealth availability (yes/no)
- Updated bio text
- Simple Practice embed code
- At least 1 blog post for launch
