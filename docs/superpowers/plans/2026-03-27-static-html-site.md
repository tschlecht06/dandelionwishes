# Dandelion Wishes Counseling — Static HTML Site Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a complete 6-page static HTML site matching all approved mockups, ready to deploy on Cloudflare Pages.

**Architecture:** Pure HTML5/CSS3, no build tools or framework. CSS custom properties for the design system. Native `<details>`/`<summary>` for FAQ accordion. CSS-only checkbox hamburger for mobile nav. Each page is a complete HTML5 document; nav and footer are copy-pasted across pages. Images served locally under `images/`.

**Tech Stack:** HTML5, CSS3 (custom properties, CSS Grid, flexbox), Google Fonts (Cormorant Garamond + Source Serif 4), Cloudflare Pages (no build command, root deploy)

**Reference mockups:** `E:/dandelionwishes/.superpowers/brainstorm/922-1774567168/`
**SEO data:** `E:/dandelionwishes/seo/page-seo-reference.md`
**Schema markup:** `E:/dandelionwishes/code-blocks/schema-markup.html`

---

## File Structure (final state)

```
dandelionwishes/
├── index.html
├── about.html
├── services.html
├── faq.html
├── contact.html
├── 404.html
├── robots.txt
├── sitemap.xml
├── blog/
│   ├── index.html
│   └── posts/
│       └── _template.html
├── css/
│   └── dandelion-wishes.css
└── images/
    ├── logo.png
    ├── hero.jpg
    └── cat-headshot.jpg
```

---

## Task 1: CSS Foundation

**Files:**
- Modify: `css/dandelion-wishes.css` (full rewrite — strip Squarespace constraints, expand for full HTML pages)

The existing file was written for Squarespace. Replace it entirely with the stylesheet below, which covers all components across all 6 pages.

- [ ] **Step 1: Replace `css/dandelion-wishes.css` with the following**

```css
/* ============================================================
   Dandelion Wishes Counseling — dandelion-wishes.css
   Google Fonts loaded in <head> via <link> tag on every page:

   <link rel="preconnect" href="https://fonts.googleapis.com">
   <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
   <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,600;0,700;1,400;1,600;1,700&family=Source+Serif+4:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
   ============================================================ */

/* --- Tokens ------------------------------------------------- */
:root {
  --gold:        #f4c430;
  --gold-dark:   #e6b820;
  --sage:        #7a9e7e;
  --sage-dark:   #5a7a58;   /* text use — WCAG AA on light bg  */
  --cream:       #fffdf0;
  --surface:     #f5f9f0;
  --text-dark:   #3d3028;
  --text-body:   #5a4a3a;
  --text-muted:  #8a7a6a;
  --footer-bg:   #2d2218;
  --radius-sm:   8px;
  --radius-md:   12px;
  --radius-lg:   16px;
  --radius-pill: 30px;
  --shadow-card: 0 2px 12px rgba(0,0,0,0.07);
}

/* --- Reset & base ------------------------------------------- */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
body {
  font-family: 'Source Serif 4', Georgia, serif;
  color: var(--text-body);
  background: var(--cream);
  line-height: 1.7;
}
img { max-width: 100%; height: auto; display: block; }
a { color: inherit; text-decoration: none; }
p { margin-bottom: 1em; }
p:last-child { margin-bottom: 0; }

/* --- Typography -------------------------------------------- */
h1, h2, h3, h4 {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-style: italic;
  color: var(--text-dark);
  line-height: 1.25;
}
h1 { font-size: clamp(28px, 5vw, 44px); }
h2 { font-size: clamp(22px, 3.5vw, 32px); }
h3 { font-size: clamp(18px, 2.5vw, 24px); }

/* --- Layout helpers ---------------------------------------- */
.container { max-width: 1100px; margin: 0 auto; padding: 0 32px; }
.section    { padding: 64px 0; }
.section--white   { background: #fff; }
.section--surface { background: var(--surface); }
.section--dark    { background: var(--footer-bg); }

/* --- Eyebrow labels ---------------------------------------- */
.eyebrow {
  font-family: system-ui, sans-serif;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: var(--sage-dark);
  margin-bottom: 10px;
}

/* --- Buttons ----------------------------------------------- */
.btn {
  display: inline-block;
  font-family: system-ui, sans-serif;
  font-size: 13px;
  font-weight: 700;
  letter-spacing: 0.5px;
  padding: 12px 28px;
  border-radius: var(--radius-pill);
  cursor: pointer;
  transition: background 0.2s, color 0.2s, opacity 0.2s;
  text-decoration: none;
  border: none;
}
.btn--gold    { background: var(--gold); color: var(--text-dark); }
.btn--gold:hover { background: var(--gold-dark); }
.btn--outline { background: transparent; color: var(--sage); border: 2px solid var(--sage); }
.btn--outline:hover { background: var(--sage); color: #fff; }

/* --- NAV --------------------------------------------------- */
.nav {
  background: var(--cream);
  border-bottom: 1px solid #f4e8b8;
  position: sticky;
  top: 0;
  z-index: 100;
}
.nav__inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 12px 32px;
  max-width: 1100px;
  margin: 0 auto;
  position: relative;
}
.nav__logo { height: 48px; width: auto; }
.nav__links {
  display: flex;
  align-items: center;
  gap: 24px;
  list-style: none;
}
.nav__link {
  font-family: system-ui, sans-serif;
  font-size: 12px;
  font-weight: 600;
  letter-spacing: 0.5px;
  text-transform: uppercase;
  color: var(--text-dark);
  transition: color 0.2s;
}
.nav__link:hover { color: var(--sage); }
.nav__link--active {
  color: var(--sage);
  border-bottom: 2px solid var(--gold);
  padding-bottom: 2px;
}
.nav__contact {
  background: var(--gold);
  color: var(--text-dark);
  padding: 6px 14px;
  border-radius: var(--radius-pill);
  font-family: system-ui, sans-serif;
  font-size: 12px;
  font-weight: 700;
}
.nav__contact:hover { background: var(--gold-dark); }

/* Mobile nav toggle (CSS-only) */
.nav-toggle   { display: none; }
.nav-hamburger {
  display: none;
  flex-direction: column;
  gap: 5px;
  cursor: pointer;
  padding: 4px;
  background: none;
  border: none;
}
.nav-hamburger span {
  display: block;
  width: 24px;
  height: 2px;
  background: var(--text-dark);
  transition: all 0.2s;
}

/* --- PAGE HERO (inner pages) ------------------------------- */
.page-hero {
  background: linear-gradient(160deg, var(--cream) 0%, var(--surface) 100%);
  padding: 56px 32px;
  text-align: center;
}
.page-hero__eyebrow {
  font-family: system-ui, sans-serif;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: var(--sage-dark);
  margin-bottom: 12px;
}
.page-hero__title {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-style: italic;
  font-size: clamp(26px, 4vw, 38px);
  color: var(--text-dark);
  line-height: 1.3;
}
.page-hero__subtitle {
  font-size: 15px;
  color: var(--text-body);
  margin-top: 14px;
  line-height: 1.7;
  max-width: 520px;
  margin-left: auto;
  margin-right: auto;
}

/* --- HOME HERO --------------------------------------------- */
.hero {
  background: linear-gradient(160deg, var(--cream) 0%, var(--surface) 100%);
  overflow: hidden;
}
.hero__inner {
  display: grid;
  grid-template-columns: 1fr 1fr;
  min-height: 420px;
}
.hero__text {
  padding: 60px 48px 60px 32px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.hero__eyebrow {
  font-family: system-ui, sans-serif;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: var(--sage-dark);
  margin-bottom: 16px;
}
.hero__title {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-style: italic;
  font-size: clamp(28px, 4vw, 42px);
  color: var(--text-dark);
  line-height: 1.2;
  margin-bottom: 20px;
}
.hero__title .accent-sage { color: var(--sage); }
.hero__title .accent-gold { color: var(--gold); }
.hero__body {
  font-size: 15px;
  color: var(--text-body);
  line-height: 1.75;
  margin-bottom: 28px;
  max-width: 340px;
}
.hero__actions { display: flex; gap: 12px; flex-wrap: wrap; }
.hero__image-wrap {
  position: relative;
  overflow: hidden;
}
.hero__image-wrap::before {
  content: '';
  position: absolute;
  left: 0; top: 0;
  width: 35%; height: 100%;
  background: linear-gradient(to right, var(--cream), transparent);
  z-index: 1;
}
.hero__image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
}

/* --- SERVICE CARDS (homepage 3-col grid) ------------------- */
.services-section { background: #fff; padding: 64px 0; }
.services-section__header { text-align: center; margin-bottom: 36px; }
.services-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}
.service-card {
  background: var(--cream);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-card);
  overflow: hidden;
  display: flex;
  flex-direction: column;
}
.service-card--gold { border-top: 3px solid var(--gold); }
.service-card--sage { border-top: 3px solid var(--sage); }
.service-card__img {
  height: 160px;
  background: #f5f0e8;
  overflow: hidden;
}
.service-card__img img { width: 100%; height: 100%; object-fit: cover; }
.service-card__body { padding: 20px 22px 24px; flex: 1; display: flex; flex-direction: column; }
.service-card__title {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-style: italic;
  font-size: 18px;
  color: var(--text-dark);
  margin-bottom: 8px;
}
.service-card__desc { font-size: 13px; color: var(--text-body); line-height: 1.65; flex: 1; }
.service-card__link {
  font-family: system-ui, sans-serif;
  font-size: 12px;
  font-weight: 700;
  color: var(--sage);
  margin-top: 14px;
  display: inline-block;
}
.service-card__link:hover { text-decoration: underline; }

/* --- ABOUT SNIPPET (homepage) ------------------------------ */
.about-snippet { background: var(--surface); padding: 64px 0; }
.about-snippet__inner {
  display: grid;
  grid-template-columns: 260px 1fr;
  gap: 60px;
  align-items: center;
}
.about-snippet__photo-wrap { text-align: center; }
.about-snippet__photo {
  width: 160px;
  height: 160px;
  border-radius: 50%;
  object-fit: cover;
  object-position: center top;
  border: 4px solid var(--gold);
  margin: 0 auto 16px;
  box-shadow: var(--shadow-card);
}
.about-snippet__name {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-style: italic;
  font-size: 18px;
  color: var(--text-dark);
}
.about-snippet__creds {
  font-family: system-ui, sans-serif;
  font-size: 11px;
  color: var(--sage-dark);
  letter-spacing: 1px;
  margin-top: 4px;
}
.about-snippet__eyebrow {
  font-family: system-ui, sans-serif;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--sage-dark);
  margin-bottom: 10px;
}
.about-snippet__bio {
  font-size: 15px;
  color: var(--text-body);
  line-height: 1.75;
  margin-bottom: 20px;
}
.about-snippet__link {
  font-family: system-ui, sans-serif;
  font-size: 13px;
  font-weight: 700;
  color: var(--sage);
}
.about-snippet__link:hover { text-decoration: underline; }

/* --- BOTTOM CTA -------------------------------------------- */
.bottom-cta {
  background: var(--footer-bg);
  padding: 64px 32px;
  text-align: center;
}
.bottom-cta__title {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-style: italic;
  font-size: clamp(24px, 3vw, 36px);
  color: #e8dcc8;
  margin-bottom: 12px;
}
.bottom-cta__sub {
  font-family: system-ui, sans-serif;
  font-size: 14px;
  color: #c4b48a;
  margin-bottom: 28px;
  max-width: 400px;
  margin-left: auto;
  margin-right: auto;
  line-height: 1.7;
}
.bottom-cta__contact {
  margin-top: 20px;
  font-family: system-ui, sans-serif;
  font-size: 13px;
  color: #c8b89a;
}
.bottom-cta__contact a { color: inherit; }
.bottom-cta__contact a:hover { text-decoration: underline; }

/* --- FOOTER ------------------------------------------------ */
.footer { background: var(--footer-bg); padding: 40px 0 28px; }
.footer__inner {
  display: grid;
  grid-template-columns: 1fr auto;
  gap: 40px;
  align-items: start;
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 32px;
}
.footer__brand {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-style: italic;
  font-size: 18px;
  color: #e8dcc8;
  margin-bottom: 8px;
}
.footer__nap {
  font-family: system-ui, sans-serif;
  font-size: 12px;
  color: #c8b89a;
  line-height: 1.8;
}
.footer__nap a { color: inherit; }
.footer__nap a:hover { text-decoration: underline; }
.footer__right { text-align: right; }
.footer__nav {
  list-style: none;
  display: flex;
  gap: 20px;
  justify-content: flex-end;
  margin-bottom: 12px;
}
.footer__nav a {
  font-family: system-ui, sans-serif;
  font-size: 12px;
  color: #c8b89a;
}
.footer__nav a:hover { color: #e8dcc8; }
.footer__copy {
  font-family: system-ui, sans-serif;
  font-size: 11px;
  color: #7a6a5a;
}

/* --- ABOUT PAGE -------------------------------------------- */
.bio-section { background: #fff; padding: 64px 0; }
.bio-section__inner {
  display: grid;
  grid-template-columns: 220px 1fr;
  gap: 48px;
  align-items: start;
}
.bio-section__photo {
  width: 100%;
  border-radius: var(--radius-lg);
  box-shadow: 0 4px 16px rgba(0,0,0,0.12);
  margin-bottom: 16px;
}
.credential-badge {
  display: flex;
  gap: 12px;
  align-items: flex-start;
  background: var(--cream);
  border-radius: var(--radius-sm);
  padding: 12px 14px;
  margin-bottom: 8px;
}
.credential-badge--gold { border-left: 4px solid var(--gold); }
.credential-badge--sage { border-left: 4px solid var(--sage); }
.credential-badge__abbr {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-style: italic;
  font-weight: 700;
  font-size: 17px;
  color: var(--text-dark);
  flex-shrink: 0;
  min-width: 34px;
}
.credential-badge__text { min-width: 0; }
.credential-badge__title {
  font-family: system-ui, sans-serif;
  font-size: 12px;
  font-weight: 700;
  color: var(--text-dark);
  margin-bottom: 2px;
}
.credential-badge__desc {
  font-family: system-ui, sans-serif;
  font-size: 11px;
  color: #4a3a2a;
  line-height: 1.55;
}
.bio-section__quote {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-style: italic;
  font-size: 22px;
  color: var(--text-dark);
  line-height: 1.45;
  margin-bottom: 20px;
  border-left: 3px solid var(--gold);
  padding-left: 20px;
}
.bio-section__text { font-size: 15px; color: var(--text-body); line-height: 1.8; }
.bio-section__license {
  font-family: system-ui, sans-serif;
  font-size: 12px;
  color: var(--text-muted);
  margin-top: 20px;
}

/* Philosophy grid */
.philosophy { background: var(--surface); padding: 64px 0; }
.philosophy__header { text-align: center; margin-bottom: 36px; }
.philosophy__grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
  max-width: 680px;
  margin: 0 auto;
}
.philosophy-card {
  background: #fff;
  border-radius: var(--radius-md);
  padding: 22px 24px;
}
.philosophy-card--gold { border-top: 3px solid var(--gold); }
.philosophy-card--sage { border-top: 3px solid var(--sage); }
.philosophy-card__title {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-style: italic;
  font-size: 17px;
  color: var(--text-dark);
  margin-bottom: 8px;
}
.philosophy-card__desc { font-size: 13px; color: var(--text-body); line-height: 1.65; }

/* --- SERVICES PAGE ----------------------------------------- */
.service-row { padding: 48px 0; border-bottom: 1px solid #f0e8d8; }
.service-row:last-child { border-bottom: none; }
.service-row__inner {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
  align-items: center;
}
.service-row__inner--reverse { direction: rtl; }
.service-row__inner--reverse > * { direction: ltr; }
.service-row__img {
  border-radius: var(--radius-lg);
  overflow: hidden;
  background: #f5f0e8;
}
.service-row__img img {
  width: 100%;
  height: 280px;
  object-fit: cover;
  display: block;
}
.service-row__label {
  font-family: system-ui, sans-serif;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 2px;
  text-transform: uppercase;
  margin-bottom: 10px;
}
.service-row__label--gold { color: var(--gold); border-left: 3px solid var(--gold); padding-left: 10px; }
.service-row__label--sage { color: var(--sage-dark); border-left: 3px solid var(--sage); padding-left: 10px; }
.service-row__title {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-style: italic;
  font-size: 26px;
  color: var(--text-dark);
  margin-bottom: 14px;
}
.service-row__desc { font-size: 15px; color: var(--text-body); line-height: 1.75; margin-bottom: 14px; }
.service-row__may-help {
  font-family: system-ui, sans-serif;
  font-size: 13px;
  color: var(--sage-dark);
  font-style: italic;
}

/* Fees */
.fees { background: var(--surface); padding: 64px 0; }
.fees__header { text-align: center; margin-bottom: 36px; }
.fees__grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
  max-width: 680px;
  margin: 0 auto 16px;
}
.fee-card {
  background: var(--cream);
  border-radius: var(--radius-lg);
  padding: 28px 32px;
  box-shadow: var(--shadow-card);
}
.fee-card--gold { border-top: 3px solid var(--gold); }
.fee-card--sage { border-top: 3px solid var(--sage); }
.fee-card__amount {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-style: italic;
  font-size: 40px;
  color: var(--text-dark);
  line-height: 1;
  margin-bottom: 4px;
}
.fee-card__period {
  font-family: system-ui, sans-serif;
  font-size: 12px;
  color: var(--text-muted);
  margin-bottom: 10px;
}
.fee-card__desc { font-size: 13px; color: var(--text-body); line-height: 1.65; }
.fee-card__subtitle {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-style: italic;
  font-size: 18px;
  color: var(--text-dark);
  margin-bottom: 10px;
}
.gfe-notice {
  background: #fff8dc;
  border: 1px solid rgba(244,196,48,0.4);
  border-left: 4px solid var(--gold);
  border-radius: var(--radius-sm);
  padding: 18px 22px;
  font-family: system-ui, sans-serif;
  font-size: 13px;
  color: #5a3a00;
  line-height: 1.65;
  max-width: 680px;
  margin: 0 auto;
}
.gfe-notice strong { display: block; margin-bottom: 6px; font-size: 14px; }

/* --- FAQ PAGE ---------------------------------------------- */
.faq-content { background: #fff; padding: 48px 0 64px; }
.faq-group { margin-bottom: 40px; }
.faq-group__label {
  font-family: system-ui, sans-serif;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--sage-dark);
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 16px;
}
.faq-group__label::before,
.faq-group__label::after {
  content: '';
  flex: 1;
  height: 1px;
  background: #d4e8d0;
}
details.faq-item { border-bottom: 1px solid #e8dcc8; }
details.faq-item + details.faq-item { margin-top: 2px; }
details.faq-item summary {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-style: italic;
  font-size: 18px;
  color: var(--text-dark);
  padding: 18px 48px 18px 20px;
  cursor: pointer;
  list-style: none;
  position: relative;
  background: var(--cream);
}
details.faq-item summary::-webkit-details-marker { display: none; }
details.faq-item summary::after {
  content: '+';
  position: absolute;
  right: 20px;
  top: 50%;
  transform: translateY(-50%);
  font-family: system-ui, sans-serif;
  font-size: 20px;
  font-style: normal;
  color: var(--gold);
  transition: transform 0.2s;
}
details.faq-item[open] summary::after { content: '−'; }
.faq-item__answer {
  padding: 16px 20px 24px;
  font-size: 15px;
  color: var(--text-body);
  line-height: 1.75;
  background: var(--cream);
}
.faq-still-questions {
  background: var(--surface);
  border: 1px solid #d4e8d0;
  border-radius: var(--radius-lg);
  padding: 28px 32px;
  text-align: center;
  margin-top: 40px;
}
.faq-still-questions h3 {
  font-size: 20px;
  margin-bottom: 10px;
}
.faq-still-questions p {
  font-size: 14px;
  color: var(--text-body);
  margin-bottom: 20px;
  max-width: 400px;
  margin-left: auto;
  margin-right: auto;
}

/* --- CONTACT PAGE ------------------------------------------ */
.contact-section { background: #fff; padding: 48px 0 64px; }
.contact-section__inner {
  display: grid;
  grid-template-columns: 1fr 300px;
  gap: 48px;
  align-items: start;
}
.hipaa-notice {
  background: #fff8dc;
  border: 1px solid rgba(244,196,48,0.4);
  border-radius: var(--radius-sm);
  padding: 14px 16px;
  display: flex;
  gap: 10px;
  align-items: flex-start;
  margin-bottom: 24px;
  font-family: system-ui, sans-serif;
  font-size: 11px;
  color: #5a3a00;
  line-height: 1.65;
}
.hipaa-notice__icon { font-size: 16px; flex-shrink: 0; margin-top: 1px; }
.contact-form-title {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-style: italic;
  font-size: 22px;
  color: var(--text-dark);
  margin-bottom: 20px;
}
.simple-practice-embed {
  background: var(--surface);
  border-radius: var(--radius-sm);
  padding: 28px;
  min-height: 120px;
  font-family: system-ui, sans-serif;
  font-size: 13px;
  color: var(--text-muted);
  text-align: center;
}
.contact-info-card {
  background: var(--cream);
  border-radius: var(--radius-lg);
  padding: 20px 22px;
  margin-bottom: 14px;
}
.contact-info-card--gold { border-top: 3px solid var(--gold); }
.contact-info-card--sage { border-top: 3px solid var(--sage); }
.contact-info-card__label {
  font-family: system-ui, sans-serif;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--sage-dark);
  margin-bottom: 10px;
}
.contact-info-card__phone {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-style: italic;
  font-size: 18px;
  color: var(--text-dark);
  margin-bottom: 4px;
}
.contact-info-card__email { font-size: 13px; color: var(--text-body); margin-bottom: 10px; }
.contact-info-card__crisis { font-size: 11px; color: var(--text-muted); line-height: 1.6; }
.contact-info-card__address { font-size: 13px; color: var(--text-dark); line-height: 1.75; }
.hours-row {
  display: flex;
  justify-content: space-between;
  font-size: 12px;
  font-family: system-ui, sans-serif;
  margin-bottom: 4px;
  color: var(--text-body);
}

/* --- BLOG LISTING ------------------------------------------ */
.blog-listing { background: #fff; padding: 48px 0 64px; }
.blog-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}
.blog-card {
  background: var(--cream);
  border-radius: var(--radius-md);
  overflow: hidden;
  box-shadow: var(--shadow-card);
}
/* Featured post spans full width */
.blog-card:first-child {
  grid-column: 1 / -1;
  display: grid;
  grid-template-columns: 1fr 1fr;
}
.blog-card__img { height: 180px; background: var(--surface); overflow: hidden; }
.blog-card__img img { width: 100%; height: 100%; object-fit: cover; }
.blog-card:first-child .blog-card__img { height: 100%; min-height: 240px; }
.blog-card__body { padding: 20px 22px; }
.blog-card:first-child .blog-card__body {
  padding: 32px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.blog-card__category {
  font-family: system-ui, sans-serif;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--gold);
  margin-bottom: 8px;
}
.blog-card__title {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-style: italic;
  font-size: 17px;
  color: var(--text-dark);
  line-height: 1.35;
  margin-bottom: 8px;
}
.blog-card:first-child .blog-card__title { font-size: 22px; }
.blog-card__excerpt { font-size: 13px; color: var(--text-body); line-height: 1.65; margin-bottom: 12px; }
.blog-card__link {
  font-family: system-ui, sans-serif;
  font-size: 12px;
  font-weight: 700;
  color: var(--sage);
}
.blog-card__link:hover { text-decoration: underline; }

/* --- BLOG POST PAGE ---------------------------------------- */
.post-header {
  background: linear-gradient(160deg, var(--cream) 0%, var(--surface) 100%);
  padding: 56px 32px 40px;
  text-align: center;
}
.post-date {
  font-family: system-ui, sans-serif;
  font-size: 11px;
  color: var(--sage-dark);
  letter-spacing: 1px;
  margin-bottom: 12px;
}
.post-category {
  font-family: system-ui, sans-serif;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--gold);
  margin-bottom: 14px;
}
.post-title {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-style: italic;
  font-size: clamp(26px, 4vw, 38px);
  color: var(--text-dark);
  line-height: 1.3;
  max-width: 700px;
  margin: 0 auto;
}
.post-body {
  max-width: 700px;
  margin: 0 auto;
  padding: 48px 32px 80px;
  font-size: 16px;
  line-height: 1.8;
}
.post-body h2 { margin: 40px 0 16px; }
.post-body h3 { margin: 28px 0 12px; }
.post-body p  { margin-bottom: 1.25em; }
.post-back {
  font-family: system-ui, sans-serif;
  font-size: 13px;
  font-weight: 700;
  color: var(--sage);
  display: inline-block;
  margin-bottom: 36px;
}
.post-back:hover { text-decoration: underline; }

/* --- 404 --------------------------------------------------- */
.not-found { padding: 100px 32px; text-align: center; min-height: 50vh; display: flex; flex-direction: column; align-items: center; justify-content: center; }
.not-found h1 { font-size: clamp(32px, 5vw, 52px); margin-bottom: 16px; }
.not-found p { font-size: 16px; color: var(--text-body); margin-bottom: 32px; max-width: 400px; }

/* --- RESPONSIVE -------------------------------------------- */
@media (max-width: 768px) {
  /* Mobile nav */
  .nav-hamburger { display: flex; }
  .nav__links {
    display: none;
    flex-direction: column;
    align-items: flex-start;
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    background: var(--cream);
    padding: 20px 32px;
    border-bottom: 1px solid #f4e8b8;
    gap: 16px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.08);
  }
  .nav-toggle:checked ~ .nav .nav__links { display: flex; }

  /* Hero */
  .hero__inner { grid-template-columns: 1fr; }
  .hero__image-wrap { height: 260px; }
  .hero__text { padding: 40px 24px; }

  /* Layouts */
  .about-snippet__inner,
  .bio-section__inner,
  .contact-section__inner { grid-template-columns: 1fr; }
  .service-row__inner,
  .service-row__inner--reverse { grid-template-columns: 1fr; direction: ltr; }
  .fees__grid,
  .philosophy__grid,
  .services-grid { grid-template-columns: 1fr; }
  .blog-card:first-child { grid-template-columns: 1fr; }
  .blog-card:first-child .blog-card__img { height: 200px; }
  .blog-grid { grid-template-columns: 1fr; }
  .footer__inner { grid-template-columns: 1fr; }
  .footer__right { text-align: left; }
  .footer__nav { justify-content: flex-start; }
}
```

- [ ] **Step 2: Verify**

Start a local server and open a blank test page linked to the stylesheet:
```bash
cd E:/dandelionwishes
python -m http.server 8080
```
Open `http://localhost:8080` — no 404 errors for the CSS file.

- [ ] **Step 3: Commit**

```bash
cd E:/dandelionwishes
git add css/dandelion-wishes.css
git commit -m "feat: rewrite CSS for full HTML site (no Squarespace constraints)

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"
```

---

## Task 2: Download Images

**Files:**
- Create: `images/logo.png`
- Create: `images/hero.jpg`
- Create: `images/cat-headshot.jpg`

These images currently live on the Squarespace CDN tied to Cat's account. Download them locally so the site works independently.

- [ ] **Step 1: Create the `images/` directory and download**

```bash
mkdir -p E:/dandelionwishes/images

curl -L "https://images.squarespace-cdn.com/content/v1/6945cb2027be636b679bba8a/60025083-9d94-40c4-ad15-e0325361516e/Screenshot+2023-02-05+201258.png" -o "E:/dandelionwishes/images/logo.png"

curl -L "https://images.squarespace-cdn.com/content/v1/6945cb2027be636b679bba8a/dd15c8bd-a84e-44f7-9be4-e1a3fee44b3f/shutterstock_339633185+%281%29.jpg" -o "E:/dandelionwishes/images/hero.jpg"

curl -L "https://images.squarespace-cdn.com/content/v1/6945cb2027be636b679bba8a/282c19c3-c309-483b-aac9-f376ae2fde2a/IMG_2279.png" -o "E:/dandelionwishes/images/cat-headshot.jpg"
```

- [ ] **Step 2: Verify all 3 files downloaded and are non-zero size**

```bash
ls -lh E:/dandelionwishes/images/
```
Expected: `logo.png`, `hero.jpg`, `cat-headshot.jpg` each several KB or larger.

- [ ] **Step 3: Commit**

```bash
cd E:/dandelionwishes
git add images/
git commit -m "feat: add locally-hosted images (logo, hero, headshot)

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"
```

---

## Task 3: Home Page

**Files:**
- Create: `index.html`

The nav and footer HTML in this task are the canonical copy-paste source for all subsequent pages.

- [ ] **Step 1: Create `index.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Child Therapy &amp; Play Therapy in Thornton, CO | Dandelion Wishes Counseling</title>
  <meta name="description" content="Cat Ianni-Schlecht, LPC, RPT offers play therapy and child counseling in Thornton, CO. Serving children, teens &amp; families. Call (303) 656-9362.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,600;0,700;1,400;1,600;1,700&family=Source+Serif+4:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="css/dandelion-wishes.css">
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": ["LocalBusiness", "MedicalClinic"],
    "name": "Dandelion Wishes Counseling",
    "description": "Child counseling, play therapy, and teen therapy in Thornton, Colorado. Serving children, adolescents, and families.",
    "url": "https://dandelionwishescounseling.com",
    "telephone": "(303) 656-9362",
    "email": "Cat@dandelionwishescounseling.com",
    "address": {
      "@type": "PostalAddress",
      "streetAddress": "2090 East 104th Ave, Suite 302",
      "addressLocality": "Thornton",
      "addressRegion": "CO",
      "addressCountry": "US"
    },
    "priceRange": "$125 per session",
    "employee": {
      "@type": "Person",
      "name": "Cat Ianni-Schlecht",
      "jobTitle": "Licensed Professional Counselor, Registered Play Therapist",
      "honorificSuffix": "MA, LPC, NCC, RPT"
    }
  }
  </script>
</head>
<body>

<!-- NAV -->
<input type="checkbox" id="nav-toggle" class="nav-toggle">
<nav class="nav">
  <div class="nav__inner">
    <a href="/"><img src="images/logo.png" alt="Dandelion Wishes Counseling logo" class="nav__logo"></a>
    <label for="nav-toggle" class="nav-hamburger" aria-label="Open navigation">
      <span></span><span></span><span></span>
    </label>
    <ul class="nav__links">
      <li><a href="/about" class="nav__link">About</a></li>
      <li><a href="/services" class="nav__link">Services &amp; Fees</a></li>
      <li><a href="/faq" class="nav__link">FAQ</a></li>
      <li><a href="/blog/" class="nav__link">Blog</a></li>
      <li><a href="/contact" class="nav__contact">Contact</a></li>
    </ul>
  </div>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="hero__inner">
    <div class="hero__text">
      <p class="hero__eyebrow">Child Counseling &amp; Play Therapy · Thornton, CO</p>
      <h1 class="hero__title">A safe place for children to <span class="accent-sage">process, play,</span> learn, and <span class="accent-gold">grow</span></h1>
      <p class="hero__body">Cat Ianni-Schlecht, MA, LPC, RPT — Licensed Professional Counselor &amp; Registered Play Therapist serving children, teens, and families.</p>
      <div class="hero__actions">
        <a href="/contact" class="btn btn--gold">Get in Touch</a>
        <a href="/about" class="btn btn--outline">Learn More</a>
      </div>
    </div>
    <div class="hero__image-wrap">
      <img src="images/hero.jpg" alt="Child blowing dandelion seeds — play therapy in Thornton Colorado" class="hero__image">
    </div>
  </div>
</section>

<!-- SERVICES -->
<section class="services-section">
  <div class="container">
    <div class="services-section__header">
      <p class="eyebrow">How I Can Help</p>
      <h2>Services for children &amp; families</h2>
    </div>
    <div class="services-grid">

      <article class="service-card service-card--gold">
        <div class="service-card__img">
          <!-- TODO: <img src="images/child-therapy.jpg" alt="Child playing during play therapy session" loading="lazy"> -->
        </div>
        <div class="service-card__body">
          <h3 class="service-card__title">Child Therapy</h3>
          <p class="service-card__desc">Play-based therapy for children ages 3–12 to safely explore big emotions, work through challenges, and build lasting coping skills.</p>
          <a href="/services" class="service-card__link">Learn more →</a>
        </div>
      </article>

      <article class="service-card service-card--sage">
        <div class="service-card__img">
          <!-- TODO: <img src="images/teen-therapy.jpg" alt="Teen in counseling session" loading="lazy"> -->
        </div>
        <div class="service-card__body">
          <h3 class="service-card__title">Teen Therapy</h3>
          <p class="service-card__desc">Supportive counseling for adolescents navigating anxiety, identity, school stress, and life transitions in a judgment-free space.</p>
          <a href="/services" class="service-card__link">Learn more →</a>
        </div>
      </article>

      <article class="service-card service-card--gold">
        <div class="service-card__img">
          <!-- TODO: <img src="images/parent-coaching.jpg" alt="Parent and child together" loading="lazy"> -->
        </div>
        <div class="service-card__body">
          <h3 class="service-card__title">Parent Coaching</h3>
          <p class="service-card__desc">Practical, compassionate strategies to strengthen your family's connection and better understand your child's emotional world.</p>
          <a href="/services" class="service-card__link">Learn more →</a>
        </div>
      </article>

    </div>
  </div>
</section>

<!-- ABOUT SNIPPET -->
<section class="about-snippet">
  <div class="container">
    <div class="about-snippet__inner">
      <div class="about-snippet__photo-wrap">
        <img src="images/cat-headshot.jpg" alt="Cat Ianni-Schlecht, Licensed Professional Counselor and Registered Play Therapist in Thornton, CO" class="about-snippet__photo" loading="lazy">
        <p class="about-snippet__name">Cat Ianni-Schlecht</p>
        <p class="about-snippet__creds">MA, LPC, NCC, RPT</p>
      </div>
      <div>
        <p class="about-snippet__eyebrow">Meet Your Therapist</p>
        <p class="about-snippet__bio">Licensed Professional Counselor and Registered Play Therapist dedicated to creating a warm, play-filled space where children can express themselves safely and begin to heal.</p>
        <a href="/about" class="about-snippet__link">Read Cat's full bio →</a>
      </div>
    </div>
  </div>
</section>

<!-- BOTTOM CTA -->
<section class="bottom-cta">
  <h2 class="bottom-cta__title">Ready to take the first step?</h2>
  <p class="bottom-cta__sub">Reach out to schedule a free 15-minute phone consultation. No commitment required — just a conversation.</p>
  <a href="/contact" class="btn btn--gold">Get in Touch</a>
  <p class="bottom-cta__contact">
    <a href="tel:+13036569362">(303) 656-9362</a> &nbsp;·&nbsp;
    <a href="mailto:Cat@dandelionwishescounseling.com">Cat@dandelionwishescounseling.com</a>
  </p>
</section>

<!-- FOOTER -->
<footer class="footer">
  <div class="footer__inner">
    <div>
      <p class="footer__brand">Dandelion Wishes Counseling</p>
      <address class="footer__nap" style="font-style:normal;">
        2090 East 104th Ave, Suite 302, Thornton, CO<br>
        <a href="tel:+13036569362">(303) 656-9362</a> ·
        <a href="mailto:Cat@dandelionwishescounseling.com">Cat@dandelionwishescounseling.com</a>
      </address>
    </div>
    <div class="footer__right">
      <ul class="footer__nav">
        <li><a href="/faq">FAQ</a></li>
        <li><a href="/services">Fees</a></li>
        <li><a href="/contact">Contact</a></li>
      </ul>
      <p class="footer__copy">© 2026 Dandelion Wishes Counseling · Thornton, CO</p>
    </div>
  </div>
</footer>

</body>
</html>
```

- [ ] **Step 2: Open in browser and verify**

```bash
# server already running from Task 1, or restart:
python -m http.server 8080
```
Open `http://localhost:8080`. Check:
- Logo renders in nav
- Hero image shows (child + dandelion)
- Cat's headshot shows in about snippet
- Service cards show cream placeholder (no broken images)
- Gold and sage colors match design
- Mobile: resize to <768px — hamburger appears, nav collapses

- [ ] **Step 3: Commit**

```bash
cd E:/dandelionwishes
git add index.html
git commit -m "feat: add home page

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"
```

---

## Task 4: About Page

**Files:**
- Create: `about.html`

Copy nav and footer from `index.html`. Set `class="nav__link--active"` on the About nav link.

- [ ] **Step 1: Create `about.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>About Cat Ianni-Schlecht, LPC, RPT | Dandelion Wishes Counseling</title>
  <meta name="description" content="Meet Cat Ianni-Schlecht, Licensed Professional Counselor &amp; Registered Play Therapist in Thornton, CO. Compassionate, child-centered therapy.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,600;0,700;1,400;1,600;1,700&family=Source+Serif+4:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="css/dandelion-wishes.css">
</head>
<body>

<!-- NAV (copy from index.html — set nav__link--active on About) -->
<input type="checkbox" id="nav-toggle" class="nav-toggle">
<nav class="nav">
  <div class="nav__inner">
    <a href="/"><img src="images/logo.png" alt="Dandelion Wishes Counseling logo" class="nav__logo"></a>
    <label for="nav-toggle" class="nav-hamburger" aria-label="Open navigation">
      <span></span><span></span><span></span>
    </label>
    <ul class="nav__links">
      <li><a href="/about" class="nav__link nav__link--active">About</a></li>
      <li><a href="/services" class="nav__link">Services &amp; Fees</a></li>
      <li><a href="/faq" class="nav__link">FAQ</a></li>
      <li><a href="/blog/" class="nav__link">Blog</a></li>
      <li><a href="/contact" class="nav__contact">Contact</a></li>
    </ul>
  </div>
</nav>

<!-- PAGE HERO -->
<div class="page-hero">
  <p class="page-hero__eyebrow">Licensed Professional Counselor · Registered Play Therapist</p>
  <h1 class="page-hero__title">Meet Cat Ianni-Schlecht</h1>
</div>

<!-- BIO SECTION -->
<section class="bio-section">
  <div class="container">
    <div class="bio-section__inner">

      <!-- Left: photo + credentials -->
      <div>
        <img src="images/cat-headshot.jpg" alt="Cat Ianni-Schlecht, Licensed Professional Counselor and Registered Play Therapist in Thornton, CO" class="bio-section__photo" loading="lazy">

        <div class="credential-badge credential-badge--gold">
          <span class="credential-badge__abbr">MA</span>
          <div class="credential-badge__text">
            <p class="credential-badge__title">Master of Arts in Counseling</p>
            <p class="credential-badge__desc">Graduate-level training in counseling theory and practice</p>
          </div>
        </div>
        <div class="credential-badge credential-badge--sage">
          <span class="credential-badge__abbr">LPC</span>
          <div class="credential-badge__text">
            <p class="credential-badge__title">Licensed Professional Counselor</p>
            <p class="credential-badge__desc">Licensed by the Colorado Department of Regulatory Agencies to practice counseling</p>
          </div>
        </div>
        <div class="credential-badge credential-badge--gold">
          <span class="credential-badge__abbr">NCC</span>
          <div class="credential-badge__text">
            <p class="credential-badge__title">Nationally Certified Counselor</p>
            <p class="credential-badge__desc">National certification demonstrating advanced counseling competency</p>
          </div>
        </div>
        <div class="credential-badge credential-badge--sage">
          <span class="credential-badge__abbr">RPT</span>
          <div class="credential-badge__text">
            <p class="credential-badge__title">Registered Play Therapist</p>
            <p class="credential-badge__desc">Advanced certification in child-centered play therapy from the Association for Play Therapy</p>
          </div>
        </div>
      </div>

      <!-- Right: bio text -->
      <div>
        <blockquote class="bio-section__quote">I believe every child deserves a space where they feel truly seen.</blockquote>
        <div class="bio-section__text">
          <p>Cat Ianni-Schlecht is a Licensed Professional Counselor and Registered Play Therapist based in Thornton, Colorado. She specializes in working with children, adolescents, and families using play therapy — a research-supported approach that meets children where they are, using play as their natural language.</p>
          <p>Cat approaches every session with warmth, curiosity, and a deep respect for each child's unique experience. She works collaboratively with parents throughout the process, helping families build stronger connections and lasting skills.</p>
        </div>
        <p class="bio-section__license">License #LPC.0019452 · Serving Thornton, CO and surrounding areas</p>
      </div>

    </div>
  </div>
</section>

<!-- PHILOSOPHY -->
<section class="philosophy">
  <div class="container">
    <div class="philosophy__header">
      <p class="eyebrow">My Approach</p>
      <h2>Why play therapy?</h2>
    </div>
    <div class="philosophy__grid">
      <div class="philosophy-card philosophy-card--gold">
        <h3 class="philosophy-card__title">Play is a child's language</h3>
        <p class="philosophy-card__desc">Children naturally express thoughts and feelings through play. It's how they make sense of the world — and how therapy can reach them most effectively.</p>
      </div>
      <div class="philosophy-card philosophy-card--sage">
        <h3 class="philosophy-card__title">Safety comes first</h3>
        <p class="philosophy-card__desc">A child can only grow when they feel truly safe. Cat creates a consistent, accepting environment where kids can explore without fear of judgment.</p>
      </div>
      <div class="philosophy-card philosophy-card--gold">
        <h3 class="philosophy-card__title">Parents as partners</h3>
        <p class="philosophy-card__desc">Healing happens beyond the playroom too. Cat works closely with parents, sharing insights and tools to extend growth into everyday family life.</p>
      </div>
      <div class="philosophy-card philosophy-card--sage">
        <h3 class="philosophy-card__title">Every child is different</h3>
        <p class="philosophy-card__desc">No two children or families are the same. Cat tailors her approach to each child's needs, temperament, and goals — never one-size-fits-all.</p>
      </div>
    </div>
  </div>
</section>

<!-- BOTTOM CTA -->
<section class="bottom-cta">
  <h2 class="bottom-cta__title">Ready to connect?</h2>
  <p class="bottom-cta__sub">Reach out to schedule a free 15-minute phone consultation.</p>
  <a href="/contact" class="btn btn--gold">Get in Touch</a>
</section>

<!-- FOOTER (copy from index.html) -->
<footer class="footer">
  <div class="footer__inner">
    <div>
      <p class="footer__brand">Dandelion Wishes Counseling</p>
      <address class="footer__nap" style="font-style:normal;">
        2090 East 104th Ave, Suite 302, Thornton, CO<br>
        <a href="tel:+13036569362">(303) 656-9362</a> ·
        <a href="mailto:Cat@dandelionwishescounseling.com">Cat@dandelionwishescounseling.com</a>
      </address>
    </div>
    <div class="footer__right">
      <ul class="footer__nav">
        <li><a href="/faq">FAQ</a></li>
        <li><a href="/services">Fees</a></li>
        <li><a href="/contact">Contact</a></li>
      </ul>
      <p class="footer__copy">© 2026 Dandelion Wishes Counseling · Thornton, CO</p>
    </div>
  </div>
</footer>

</body>
</html>
```

- [ ] **Step 2: Open `http://localhost:8080/about` and verify**

- Cat's headshot renders, credential badges show with alternating gold/sage left borders
- Philosophy grid is 2×2 on desktop, stacks on mobile
- Active nav state: "About" has underline

- [ ] **Step 3: Commit**

```bash
git add about.html
git commit -m "feat: add About page

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"
```

---

## Task 5: Services & Fees Page

**Files:**
- Create: `services.html`

- [ ] **Step 1: Create `services.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Play Therapy Services &amp; Fees | Dandelion Wishes Counseling</title>
  <meta name="description" content="Child therapy, teen counseling &amp; parent coaching in Thornton, CO. Sessions $125. Learn about Cat's play therapy approach and service offerings.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,600;0,700;1,400;1,600;1,700&family=Source+Serif+4:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="css/dandelion-wishes.css">
</head>
<body>

<!-- NAV -->
<input type="checkbox" id="nav-toggle" class="nav-toggle">
<nav class="nav">
  <div class="nav__inner">
    <a href="/"><img src="images/logo.png" alt="Dandelion Wishes Counseling logo" class="nav__logo"></a>
    <label for="nav-toggle" class="nav-hamburger" aria-label="Open navigation">
      <span></span><span></span><span></span>
    </label>
    <ul class="nav__links">
      <li><a href="/about" class="nav__link">About</a></li>
      <li><a href="/services" class="nav__link nav__link--active">Services &amp; Fees</a></li>
      <li><a href="/faq" class="nav__link">FAQ</a></li>
      <li><a href="/blog/" class="nav__link">Blog</a></li>
      <li><a href="/contact" class="nav__contact">Contact</a></li>
    </ul>
  </div>
</nav>

<!-- PAGE HERO -->
<div class="page-hero">
  <p class="page-hero__eyebrow">Play Therapy · Counseling · Coaching</p>
  <h1 class="page-hero__title">How I can help your family</h1>
  <p class="page-hero__subtitle">Every child is unique. Services are tailored to meet your child and family where you are.</p>
</div>

<!-- SERVICE ROWS -->
<section class="section section--white">
  <div class="container">

    <!-- Child Therapy -->
    <div class="service-row">
      <div class="service-row__inner">
        <div class="service-row__img">
          <!-- TODO: <img src="images/child-therapy.jpg" alt="Child playing during play therapy session" loading="lazy"> -->
        </div>
        <div>
          <p class="service-row__label service-row__label--gold">Ages 3–12</p>
          <h2 class="service-row__title">Child Therapy (Play Therapy)</h2>
          <p class="service-row__desc">Using games, toys, art, movement, and storytelling as the primary way children express their thoughts and feelings. Play therapy helps children process difficult emotions, work through trauma, and build lasting coping skills in a way that feels natural and safe.</p>
          <p class="service-row__may-help">May help with: anxiety, ADHD, trauma, grief, behavioral challenges, school refusal, social skills, life transitions</p>
        </div>
      </div>
    </div>

    <!-- Teen Therapy -->
    <div class="service-row">
      <div class="service-row__inner service-row__inner--reverse">
        <div class="service-row__img">
          <!-- TODO: <img src="images/teen-therapy.jpg" alt="Teen in counseling session" loading="lazy"> -->
        </div>
        <div>
          <p class="service-row__label service-row__label--sage">Adolescents &amp; Teens</p>
          <h2 class="service-row__title">Teen Therapy</h2>
          <p class="service-row__desc">A supportive, judgment-free space for adolescents to explore what they're going through. Using a mix of talk therapy and age-appropriate creative approaches, Cat helps teens develop emotional regulation, self-awareness, and coping strategies they can carry into adulthood.</p>
          <p class="service-row__may-help">May help with: anxiety, depression, identity, peer relationships, academic stress, family conflict, self-esteem</p>
        </div>
      </div>
    </div>

    <!-- Parent Coaching -->
    <div class="service-row">
      <div class="service-row__inner">
        <div class="service-row__img">
          <!-- TODO: <img src="images/parent-coaching.jpg" alt="Parent and child together" loading="lazy"> -->
        </div>
        <div>
          <p class="service-row__label service-row__label--gold">For Parents</p>
          <h2 class="service-row__title">Parent Coaching</h2>
          <p class="service-row__desc">Practical, compassionate support for parents navigating their child's emotional and behavioral challenges. Parent coaching sessions focus on strengthening your connection with your child, understanding their needs, and building confidence in your parenting approach.</p>
          <p class="service-row__may-help">May help with: communication, behavioral strategies, attachment, co-parenting, understanding your child's emotional world</p>
        </div>
      </div>
    </div>

  </div>
</section>

<!-- FEES -->
<section class="fees">
  <div class="container">
    <div class="fees__header">
      <p class="eyebrow">Investment</p>
      <h2>Fees &amp; Insurance</h2>
    </div>
    <div class="fees__grid">
      <div class="fee-card fee-card--gold">
        <p class="fee-card__amount">$125</p>
        <p class="fee-card__period">per 50-minute session</p>
        <p class="fee-card__desc">Individual therapy and parent coaching sessions. Payment is due at the time of service.</p>
      </div>
      <div class="fee-card fee-card--sage">
        <h3 class="fee-card__subtitle">Insurance &amp; Superbills</h3>
        <p class="fee-card__desc">Currently accepting [insurance list — to be confirmed]. A superbill can be provided for out-of-network reimbursement requests.</p>
      </div>
    </div>
    <div class="gfe-notice">
      <strong>Good Faith Estimate</strong>
      Under the No Surprises Act, you have the right to receive a Good Faith Estimate of expected costs before beginning services. Please ask for one at any time — there is no obligation to continue services after receiving an estimate.
    </div>
  </div>
</section>

<!-- BOTTOM CTA -->
<section class="bottom-cta">
  <h2 class="bottom-cta__title">Questions about getting started?</h2>
  <p class="bottom-cta__sub">Reach out — Cat is happy to answer any questions before your first session.</p>
  <a href="/contact" class="btn btn--gold">Get in Touch</a>
</section>

<!-- FOOTER -->
<footer class="footer">
  <div class="footer__inner">
    <div>
      <p class="footer__brand">Dandelion Wishes Counseling</p>
      <address class="footer__nap" style="font-style:normal;">
        2090 East 104th Ave, Suite 302, Thornton, CO<br>
        <a href="tel:+13036569362">(303) 656-9362</a> ·
        <a href="mailto:Cat@dandelionwishescounseling.com">Cat@dandelionwishescounseling.com</a>
      </address>
    </div>
    <div class="footer__right">
      <ul class="footer__nav">
        <li><a href="/faq">FAQ</a></li>
        <li><a href="/services">Fees</a></li>
        <li><a href="/contact">Contact</a></li>
      </ul>
      <p class="footer__copy">© 2026 Dandelion Wishes Counseling · Thornton, CO</p>
    </div>
  </div>
</footer>

</body>
</html>
```

- [ ] **Step 2: Open `http://localhost:8080/services` and verify**

- 3 service rows render (photo placeholder + text alternating)
- Fees grid shows $125 card and insurance card side by side
- GFE notice has amber background and gold left border
- Active nav: "Services & Fees" underlined

- [ ] **Step 3: Commit**

```bash
git add services.html
git commit -m "feat: add Services & Fees page

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"
```

---

## Task 6: FAQ Page

**Files:**
- Create: `faq.html`

Uses native `<details>`/`<summary>` — no JavaScript. The CSS handles the +/− toggle.

- [ ] **Step 1: Create `faq.html`**

FAQ answers are placeholder text. Cat will provide final answers before launch. Add `<!-- TODO: replace with Cat's answer -->` comments.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Play Therapy FAQ | Dandelion Wishes Counseling Thornton CO</title>
  <meta name="description" content="Answers to common questions about play therapy, child counseling, and getting started with Cat Ianni-Schlecht, LPC, RPT in Thornton, Colorado.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,600;0,700;1,400;1,600;1,700&family=Source+Serif+4:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="css/dandelion-wishes.css">
</head>
<body>

<!-- NAV -->
<input type="checkbox" id="nav-toggle" class="nav-toggle">
<nav class="nav">
  <div class="nav__inner">
    <a href="/"><img src="images/logo.png" alt="Dandelion Wishes Counseling logo" class="nav__logo"></a>
    <label for="nav-toggle" class="nav-hamburger" aria-label="Open navigation">
      <span></span><span></span><span></span>
    </label>
    <ul class="nav__links">
      <li><a href="/about" class="nav__link">About</a></li>
      <li><a href="/services" class="nav__link">Services &amp; Fees</a></li>
      <li><a href="/faq" class="nav__link nav__link--active">FAQ</a></li>
      <li><a href="/blog/" class="nav__link">Blog</a></li>
      <li><a href="/contact" class="nav__contact">Contact</a></li>
    </ul>
  </div>
</nav>

<!-- PAGE HERO -->
<div class="page-hero">
  <p class="page-hero__eyebrow">Common Questions</p>
  <h1 class="page-hero__title">We're glad you asked</h1>
  <p class="page-hero__subtitle">Starting therapy can feel like a big step. Here are answers to the questions families ask most.</p>
</div>

<!-- FAQ CONTENT -->
<section class="faq-content">
  <div class="container" style="max-width: 760px;">

    <!-- Group 1 -->
    <div class="faq-group">
      <h2 class="faq-group__label">About Play Therapy</h2>

      <details class="faq-item" open>
        <summary>What is play therapy, exactly?</summary>
        <div class="faq-item__answer">
          <!-- TODO: replace with Cat's answer -->
          Play therapy is a research-supported approach to counseling that uses play — toys, games, art, movement, and storytelling — as the primary way children communicate. Just as adults talk through problems, children use play to express what they can't yet put into words. The therapist creates a safe, non-directive environment where the child leads, and healing happens naturally through that play.
        </div>
      </details>

      <details class="faq-item">
        <summary>How is play therapy different from regular therapy?</summary>
        <div class="faq-item__answer">
          <!-- TODO: replace with Cat's answer -->
          Placeholder answer.
        </div>
      </details>

      <details class="faq-item">
        <summary>What ages do you work with?</summary>
        <div class="faq-item__answer">
          <!-- TODO: replace with Cat's answer -->
          Placeholder answer.
        </div>
      </details>
    </div>

    <!-- Group 2 -->
    <div class="faq-group">
      <h2 class="faq-group__label">Getting Started</h2>

      <details class="faq-item">
        <summary>What happens in the first session?</summary>
        <div class="faq-item__answer">
          <!-- TODO: replace with Cat's answer -->
          Placeholder answer.
        </div>
      </details>

      <details class="faq-item">
        <summary>How do I know if my child needs therapy?</summary>
        <div class="faq-item__answer">
          <!-- TODO: replace with Cat's answer -->
          Placeholder answer.
        </div>
      </details>

      <details class="faq-item">
        <summary>How long does therapy typically last?</summary>
        <div class="faq-item__answer">
          <!-- TODO: replace with Cat's answer -->
          Placeholder answer.
        </div>
      </details>
    </div>

    <!-- Group 3 -->
    <div class="faq-group">
      <h2 class="faq-group__label">Practical Questions</h2>

      <details class="faq-item">
        <summary>Do you take insurance?</summary>
        <div class="faq-item__answer">
          <!-- TODO: replace with Cat's answer -->
          Placeholder answer.
        </div>
      </details>

      <details class="faq-item">
        <summary>Where is your office located?</summary>
        <div class="faq-item__answer">
          <!-- TODO: replace with Cat's answer -->
          The office is located at 2090 East 104th Ave, Suite 302, Thornton, CO.
        </div>
      </details>

      <details class="faq-item">
        <summary>Do you offer telehealth sessions?</summary>
        <div class="faq-item__answer">
          <!-- TODO: replace with Cat's answer (yes/no + details) -->
          Placeholder answer.
        </div>
      </details>
    </div>

    <!-- Still have questions -->
    <div class="faq-still-questions">
      <h3>Still have questions?</h3>
      <p>Don't see what you're looking for? Cat is happy to answer any question before your first session — no commitment required.</p>
      <a href="/contact" class="btn btn--gold">Get in Touch</a>
    </div>

  </div>
</section>

<!-- FOOTER -->
<footer class="footer">
  <div class="footer__inner">
    <div>
      <p class="footer__brand">Dandelion Wishes Counseling</p>
      <address class="footer__nap" style="font-style:normal;">
        2090 East 104th Ave, Suite 302, Thornton, CO<br>
        <a href="tel:+13036569362">(303) 656-9362</a> ·
        <a href="mailto:Cat@dandelionwishescounseling.com">Cat@dandelionwishescounseling.com</a>
      </address>
    </div>
    <div class="footer__right">
      <ul class="footer__nav">
        <li><a href="/faq">FAQ</a></li>
        <li><a href="/services">Fees</a></li>
        <li><a href="/contact">Contact</a></li>
      </ul>
      <p class="footer__copy">© 2026 Dandelion Wishes Counseling · Thornton, CO</p>
    </div>
  </div>
</footer>

</body>
</html>
```

- [ ] **Step 2: Open `http://localhost:8080/faq` and verify**

- First accordion item is open (shows answer)
- Click another question — it opens, others close (browser default `<details>` behavior — each item is independent, multiple can be open; that's fine)
- Group labels have sage divider lines on each side
- "Still have questions?" box has sage border

- [ ] **Step 3: Commit**

```bash
git add faq.html
git commit -m "feat: add FAQ page with native details/summary accordion

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"
```

---

## Task 7: Contact Page

**Files:**
- Create: `contact.html`

- [ ] **Step 1: Create `contact.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contact | Dandelion Wishes Counseling Thornton CO</title>
  <meta name="description" content="Reach Cat Ianni-Schlecht for child therapy &amp; play therapy in Thornton, CO. Call (303) 656-9362 or email Cat@dandelionwishescounseling.com.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,600;0,700;1,400;1,600;1,700&family=Source+Serif+4:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="css/dandelion-wishes.css">
</head>
<body>

<!-- NAV -->
<input type="checkbox" id="nav-toggle" class="nav-toggle">
<nav class="nav">
  <div class="nav__inner">
    <a href="/"><img src="images/logo.png" alt="Dandelion Wishes Counseling logo" class="nav__logo"></a>
    <label for="nav-toggle" class="nav-hamburger" aria-label="Open navigation">
      <span></span><span></span><span></span>
    </label>
    <ul class="nav__links">
      <li><a href="/about" class="nav__link">About</a></li>
      <li><a href="/services" class="nav__link">Services &amp; Fees</a></li>
      <li><a href="/faq" class="nav__link">FAQ</a></li>
      <li><a href="/blog/" class="nav__link">Blog</a></li>
      <li><a href="/contact" class="nav__contact">Contact</a></li>
    </ul>
  </div>
</nav>

<!-- PAGE HERO -->
<div class="page-hero">
  <p class="page-hero__eyebrow">Let's Connect</p>
  <h1 class="page-hero__title">Reach out — we'd love to hear from you</h1>
  <p class="page-hero__subtitle">Whether you have questions or you're ready to get started, send a message and Cat will be in touch as soon as possible.</p>
</div>

<!-- CONTACT SECTION -->
<section class="contact-section">
  <div class="container">
    <div class="contact-section__inner">

      <!-- Left: form -->
      <div>
        <h2 class="contact-form-title">Send a message</h2>

        <!-- HIPAA notice -->
        <div class="hipaa-notice">
          <span class="hipaa-notice__icon">⚠</span>
          <span><strong>Please do not include sensitive health information in this form.</strong> This contact form is not a HIPAA-secure channel. For confidential communication, please call or email directly.</span>
        </div>

        <!-- Simple Practice embed placeholder -->
        <div class="simple-practice-embed">
          <!-- SIMPLE PRACTICE EMBED: paste your embed code here -->
          <!-- Remove this placeholder div and replace with the embed script/iframe from Simple Practice -->
          <p style="margin:0; color: #8a7a6a;">Contact form loading...</p>
        </div>

        <p style="font-size:12px; color: #8a7a6a; margin-top: 14px; font-family: system-ui, sans-serif; line-height: 1.6;">Submitting this form does not create a therapist-client relationship.</p>
      </div>

      <!-- Right: contact info -->
      <div>
        <div class="contact-info-card contact-info-card--gold">
          <p class="contact-info-card__label">Phone &amp; Email</p>
          <p class="contact-info-card__phone"><a href="tel:+13036569362">(303) 656-9362</a></p>
          <p class="contact-info-card__email"><a href="mailto:Cat@dandelionwishescounseling.com">Cat@dandelionwishescounseling.com</a></p>
          <p class="contact-info-card__crisis">For urgent mental health needs, please call 988 (Suicide &amp; Crisis Lifeline) or visit your nearest emergency room.</p>
        </div>

        <div class="contact-info-card contact-info-card--sage">
          <p class="contact-info-card__label">Office Location</p>
          <address class="contact-info-card__address" style="font-style:normal;">
            2090 East 104th Ave<br>Suite 302<br>Thornton, CO
          </address>
        </div>

        <div class="contact-info-card contact-info-card--gold">
          <p class="contact-info-card__label">Office Hours</p>
          <div class="hours-row">
            <span>Monday – Friday</span>
            <span style="font-weight:600;"><!-- TODO: add hours --></span>
          </div>
          <div class="hours-row">
            <span>Saturday</span>
            <span style="color:#9a8a7a;">By arrangement</span>
          </div>
        </div>
      </div>

    </div>
  </div>
</section>

<!-- FOOTER -->
<footer class="footer">
  <div class="footer__inner">
    <div>
      <p class="footer__brand">Dandelion Wishes Counseling</p>
      <address class="footer__nap" style="font-style:normal;">
        2090 East 104th Ave, Suite 302, Thornton, CO<br>
        <a href="tel:+13036569362">(303) 656-9362</a> ·
        <a href="mailto:Cat@dandelionwishescounseling.com">Cat@dandelionwishescounseling.com</a>
      </address>
    </div>
    <div class="footer__right">
      <ul class="footer__nav">
        <li><a href="/faq">FAQ</a></li>
        <li><a href="/services">Fees</a></li>
        <li><a href="/contact">Contact</a></li>
      </ul>
      <p class="footer__copy">© 2026 Dandelion Wishes Counseling · Thornton, CO</p>
    </div>
  </div>
</footer>

</body>
</html>
```

- [ ] **Step 2: Open `http://localhost:8080/contact` and verify**

- HIPAA notice shows amber background above form area
- Contact info cards show on the right with gold/sage top borders
- Two-column layout on desktop, stacked on mobile

- [ ] **Step 3: Commit**

```bash
git add contact.html
git commit -m "feat: add Contact page with HIPAA notice and Simple Practice embed placeholder

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"
```

---

## Task 8: Blog Section

**Files:**
- Create: `blog/index.html`
- Create: `blog/posts/_template.html`

- [ ] **Step 1: Create `blog/` directory and `blog/index.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Resources for Families | Dandelion Wishes Counseling</title>
  <meta name="description" content="Articles on child development, play therapy, and supporting your family's emotional wellbeing — from Cat Ianni-Schlecht, LPC, RPT in Thornton, CO.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,600;0,700;1,400;1,600;1,700&family=Source+Serif+4:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="../css/dandelion-wishes.css">
</head>
<body>

<!-- NAV (note: href paths use ../ for blog subdirectory) -->
<input type="checkbox" id="nav-toggle" class="nav-toggle">
<nav class="nav">
  <div class="nav__inner">
    <a href="/"><img src="../images/logo.png" alt="Dandelion Wishes Counseling logo" class="nav__logo"></a>
    <label for="nav-toggle" class="nav-hamburger" aria-label="Open navigation">
      <span></span><span></span><span></span>
    </label>
    <ul class="nav__links">
      <li><a href="/about" class="nav__link">About</a></li>
      <li><a href="/services" class="nav__link">Services &amp; Fees</a></li>
      <li><a href="/faq" class="nav__link">FAQ</a></li>
      <li><a href="/blog/" class="nav__link nav__link--active">Blog</a></li>
      <li><a href="/contact" class="nav__contact">Contact</a></li>
    </ul>
  </div>
</nav>

<!-- PAGE HERO -->
<div class="page-hero">
  <p class="page-hero__eyebrow">Articles &amp; Insights</p>
  <h1 class="page-hero__title">Resources for families</h1>
  <p class="page-hero__subtitle">Practical insights on child development, play therapy, and supporting your family's emotional wellbeing.</p>
</div>

<!-- BLOG LISTING -->
<section class="blog-listing">
  <div class="container">
    <div class="blog-grid">

      <!-- FEATURED POST (first card spans full width) -->
      <!-- When adding a new post, move this featured card to the grid below and make the new post the featured one -->
      <article class="blog-card">
        <div class="blog-card__img">
          <!-- TODO: add post cover image -->
        </div>
        <div class="blog-card__body">
          <p class="blog-card__category">Featured · Play Therapy</p>
          <h2 class="blog-card__title">What to expect in your child's first play therapy session</h2>
          <p class="blog-card__excerpt">Starting therapy can feel uncertain. Here's a warm, honest look at what the first few sessions look like — for your child and for you.</p>
          <a href="/blog/posts/first-play-therapy-session" class="blog-card__link">Read more →</a>
        </div>
      </article>

      <!-- GRID POSTS (add new cards here as posts are published) -->
      <article class="blog-card">
        <div class="blog-card__img"></div>
        <div class="blog-card__body">
          <p class="blog-card__category">For Parents</p>
          <h3 class="blog-card__title">5 signs your child might benefit from therapy</h3>
          <a href="#" class="blog-card__link">Read more →</a>
        </div>
      </article>

      <article class="blog-card">
        <div class="blog-card__img"></div>
        <div class="blog-card__body">
          <p class="blog-card__category">Child Development</p>
          <h3 class="blog-card__title">How play builds emotional intelligence in young children</h3>
          <a href="#" class="blog-card__link">Read more →</a>
        </div>
      </article>

      <article class="blog-card">
        <div class="blog-card__img"></div>
        <div class="blog-card__body">
          <p class="blog-card__category">Anxiety</p>
          <h3 class="blog-card__title">Helping anxious children feel safe at school</h3>
          <a href="#" class="blog-card__link">Read more →</a>
        </div>
      </article>

    </div>
  </div>
</section>

<!-- FOOTER -->
<footer class="footer">
  <div class="footer__inner">
    <div>
      <p class="footer__brand">Dandelion Wishes Counseling</p>
      <address class="footer__nap" style="font-style:normal;">
        2090 East 104th Ave, Suite 302, Thornton, CO<br>
        <a href="tel:+13036569362">(303) 656-9362</a> ·
        <a href="mailto:Cat@dandelionwishescounseling.com">Cat@dandelionwishescounseling.com</a>
      </address>
    </div>
    <div class="footer__right">
      <ul class="footer__nav">
        <li><a href="/faq">FAQ</a></li>
        <li><a href="/services">Fees</a></li>
        <li><a href="/contact">Contact</a></li>
      </ul>
      <p class="footer__copy">© 2026 Dandelion Wishes Counseling · Thornton, CO</p>
    </div>
  </div>
</footer>

</body>
</html>
```

- [ ] **Step 2: Create `blog/posts/_template.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>POST TITLE HERE | Dandelion Wishes Counseling</title>
  <meta name="description" content="POST META DESCRIPTION HERE (max 160 chars)">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,600;0,700;1,400;1,600;1,700&family=Source+Serif+4:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="../../css/dandelion-wishes.css">
</head>
<body>

<!-- NAV -->
<input type="checkbox" id="nav-toggle" class="nav-toggle">
<nav class="nav">
  <div class="nav__inner">
    <a href="/"><img src="../../images/logo.png" alt="Dandelion Wishes Counseling logo" class="nav__logo"></a>
    <label for="nav-toggle" class="nav-hamburger" aria-label="Open navigation">
      <span></span><span></span><span></span>
    </label>
    <ul class="nav__links">
      <li><a href="/about" class="nav__link">About</a></li>
      <li><a href="/services" class="nav__link">Services &amp; Fees</a></li>
      <li><a href="/faq" class="nav__link">FAQ</a></li>
      <li><a href="/blog/" class="nav__link nav__link--active">Blog</a></li>
      <li><a href="/contact" class="nav__contact">Contact</a></li>
    </ul>
  </div>
</nav>

<!-- POST HEADER -->
<header class="post-header">
  <p class="post-category">CATEGORY HERE</p>
  <p class="post-date">MONTH DD, YYYY</p>
  <h1 class="post-title">POST TITLE HERE</h1>
</header>

<!-- POST BODY -->
<article class="post-body">
  <a href="/blog/" class="post-back">← Back to Resources</a>

  <p>POST BODY CONTENT HERE. Write using standard HTML — paragraphs with &lt;p&gt;, subheadings with &lt;h2&gt; and &lt;h3&gt;.</p>

  <h2>Subheading example</h2>
  <p>Continue writing here.</p>

</article>

<!-- FOOTER -->
<footer class="footer">
  <div class="footer__inner">
    <div>
      <p class="footer__brand">Dandelion Wishes Counseling</p>
      <address class="footer__nap" style="font-style:normal;">
        2090 East 104th Ave, Suite 302, Thornton, CO<br>
        <a href="tel:+13036569362">(303) 656-9362</a> ·
        <a href="mailto:Cat@dandelionwishescounseling.com">Cat@dandelionwishescounseling.com</a>
      </address>
    </div>
    <div class="footer__right">
      <ul class="footer__nav">
        <li><a href="/faq">FAQ</a></li>
        <li><a href="/services">Fees</a></li>
        <li><a href="/contact">Contact</a></li>
      </ul>
      <p class="footer__copy">© 2026 Dandelion Wishes Counseling · Thornton, CO</p>
    </div>
  </div>
</footer>

</body>
</html>
```

- [ ] **Step 3: Open `http://localhost:8080/blog/` and verify**

- Featured post card spans full width (2-column layout)
- 3 smaller cards below in a grid
- On mobile all cards stack to 1 column

- [ ] **Step 4: Commit**

```bash
git add blog/
git commit -m "feat: add Blog listing page and post template

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"
```

---

## Task 9: Utility Files

**Files:**
- Create: `404.html`
- Create: `robots.txt`
- Create: `sitemap.xml`

- [ ] **Step 1: Create `404.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Not Found | Dandelion Wishes Counseling</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,600;0,700;1,400;1,600;1,700&family=Source+Serif+4:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="css/dandelion-wishes.css">
</head>
<body>

<input type="checkbox" id="nav-toggle" class="nav-toggle">
<nav class="nav">
  <div class="nav__inner">
    <a href="/"><img src="images/logo.png" alt="Dandelion Wishes Counseling logo" class="nav__logo"></a>
    <label for="nav-toggle" class="nav-hamburger" aria-label="Open navigation">
      <span></span><span></span><span></span>
    </label>
    <ul class="nav__links">
      <li><a href="/about" class="nav__link">About</a></li>
      <li><a href="/services" class="nav__link">Services &amp; Fees</a></li>
      <li><a href="/faq" class="nav__link">FAQ</a></li>
      <li><a href="/blog/" class="nav__link">Blog</a></li>
      <li><a href="/contact" class="nav__contact">Contact</a></li>
    </ul>
  </div>
</nav>

<main class="not-found">
  <h1>Page not found</h1>
  <p>The page you're looking for doesn't exist. Let's get you back on track.</p>
  <a href="/" class="btn btn--gold">Go to Home</a>
</main>

<footer class="footer">
  <div class="footer__inner">
    <div>
      <p class="footer__brand">Dandelion Wishes Counseling</p>
      <address class="footer__nap" style="font-style:normal;">
        2090 East 104th Ave, Suite 302, Thornton, CO<br>
        <a href="tel:+13036569362">(303) 656-9362</a> ·
        <a href="mailto:Cat@dandelionwishescounseling.com">Cat@dandelionwishescounseling.com</a>
      </address>
    </div>
    <div class="footer__right">
      <ul class="footer__nav">
        <li><a href="/faq">FAQ</a></li>
        <li><a href="/services">Fees</a></li>
        <li><a href="/contact">Contact</a></li>
      </ul>
      <p class="footer__copy">© 2026 Dandelion Wishes Counseling · Thornton, CO</p>
    </div>
  </div>
</footer>

</body>
</html>
```

- [ ] **Step 2: Create `robots.txt`**

```
User-agent: *
Disallow:
Sitemap: https://dandelionwishescounseling.com/sitemap.xml
```

- [ ] **Step 3: Create `sitemap.xml`**

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

- [ ] **Step 4: Verify**

Open `http://localhost:8080/404.html` — branded page with nav and "Go to Home" button.
Open `http://localhost:8080/robots.txt` — plain text, no HTML wrapper.
Open `http://localhost:8080/sitemap.xml` — valid XML.

- [ ] **Step 5: Commit**

```bash
git add 404.html robots.txt sitemap.xml
git commit -m "feat: add 404 page, robots.txt, and sitemap.xml

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"
```

---

## Final Verification Checklist

After all tasks are complete, open each page and verify:

- [ ] All 6 pages load without console errors
- [ ] Logo renders in nav on every page
- [ ] Active nav state correct on each page
- [ ] Hero image and Cat's headshot load from `images/`
- [ ] Mobile nav: hamburger visible at <768px, nav links collapse/expand
- [ ] FAQ accordion: click questions to open/close
- [ ] `http://localhost:8080/blog/` — featured post spans full width
- [ ] `http://localhost:8080/404.html` — branded error page
- [ ] Validate `index.html` at https://validator.w3.org — 0 errors

---

## Cloudflare Pages Setup (after all tasks complete)

1. Push this repo to GitHub
2. In Cloudflare Pages: Connect Git > select repo
3. Build settings: **Build command** = (leave blank), **Output directory** = (leave blank)
4. Deploy
5. Add custom domain `dandelionwishescounseling.com` in Cloudflare DNS
