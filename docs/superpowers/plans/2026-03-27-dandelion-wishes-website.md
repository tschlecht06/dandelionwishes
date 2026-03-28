# Dandelion Wishes Counseling — Squarespace Website Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Produce a complete set of Squarespace-ready assets (custom CSS + HTML code injection blocks + setup guide) that Cat can paste into Squarespace 7.1 to launch the redesigned Dandelion Wishes Counseling website.

**Architecture:** CSS-first approach — a single custom CSS file handles global styles (colors, fonts, spacing, nav, buttons, cards). Individual HTML code injection blocks handle sections where Squarespace's native editor can't achieve the required layout (hero split, credential badges, HIPAA notice, JSON-LD schema). A plain-language setup guide walks Cat through exactly where to paste each piece.

**Tech Stack:** HTML5, CSS3 (custom properties / CSS variables), Google Fonts (Cormorant Garamond, Source Serif 4), Squarespace 7.1 native blocks (Accordion, Blog, Form, Map), JSON-LD schema markup.

**Spec:** `C:\Users\Tyler\.claude\plans\agile-jingling-piglet.md`
**Mockups:** `E:\dandelionwishes\.superpowers\brainstorm\922-1774567168\`

---

## File Structure

```
E:\dandelionwishes\
├── css\
│   └── dandelion-wishes.css           # Paste into Squarespace: Design > Custom CSS
├── code-blocks\
│   ├── hero-section.html              # Homepage: split hero layout
│   ├── services-cards.html            # Homepage: 3 vertical photo cards
│   ├── about-snippet.html             # Homepage: about teaser section
│   ├── bottom-cta.html                # Reusable: dark brown CTA (used on all pages)
│   ├── credential-badges.html         # About page: credential badge sidebar
│   ├── hipaa-notice.html              # Contact page: HIPAA warning banner
│   └── schema-markup.html             # Site-wide: JSON-LD in header injection
├── seo\
│   └── page-seo-reference.md          # Page titles, meta descriptions, slugs — copy/paste for Squarespace SEO panel
└── docs\
    ├── squarespace-setup-guide.md     # Step-by-step setup instructions for Cat
    └── superpowers\
        └── plans\
            └── 2026-03-27-dandelion-wishes-website.md  ← this file
```

---

## Task 1: CSS Foundation — Design Tokens & Global Styles

**Files:**
- Create: `E:\dandelionwishes\css\dandelion-wishes.css`

### What it covers
Font imports, CSS custom properties (design tokens), body/heading resets, nav styling, button styles, section backgrounds, card base styles, footer.

- [ ] **Step 1: Create the CSS file with font imports and design tokens**

```css
/* ============================================================
   DANDELION WISHES COUNSELING — Custom CSS for Squarespace 7.1
   Paste this entire file into: Design > Custom CSS
   ============================================================ */

/* --- Google Fonts --- */
@import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,600;0,700;1,400;1,600;1,700&family=Source+Serif+4:ital,wght@0,400;0,600;1,400&display=swap');

/* --- Design Tokens --- */
:root {
  --gold:        #f4c430;
  --sage:        #7a9e7e;
  --sage-dark:   #4a7c59;
  --cream:       #fffdf0;
  --surface:     #f5f9f0;
  --text-dark:   #3d3028;
  --text-body:   #5a4a3a;
  --text-muted:  #8a7a6a;
  --dark-bg:     #3d3028;
  --border-gold: #f4e8b8;

  --radius-sm:   8px;
  --radius-md:   12px;
  --radius-lg:   16px;
  --radius-pill: 30px;

  --shadow-card: 0 2px 12px rgba(0,0,0,0.07);
  --section-pad: 44px 32px;
}
```

- [ ] **Step 2: Add typography rules**

```css
/* --- Typography --- */
body,
.sqsrte-large,
.sqsrte-small {
  font-family: 'Source Serif 4', Georgia, serif;
  color: var(--text-body);
  line-height: 1.75;
}

h1, h2, h3, h4,
.sqsrte-large strong {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-style: italic;
  color: var(--text-dark);
  line-height: 1.25;
}

h1 { font-size: clamp(28px, 5vw, 42px); }
h2 { font-size: clamp(22px, 3.5vw, 30px); }
h3 { font-size: clamp(16px, 2.5vw, 20px); }

/* Eyebrow labels — small uppercase labels above headings */
.eyebrow {
  font-family: system-ui, sans-serif;
  font-size: 10px;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: var(--sage);
  font-weight: 700;
}
```

- [ ] **Step 3: Add background and section rules**

```css
/* --- Site Background --- */
body { background-color: var(--cream); }

/* Alternating section backgrounds — apply via Squarespace section background color setting */
.page-section--has-background-image + .page-section,
.sqs-layout .sqs-col-12 { background-color: var(--cream); }

/* Surface sections (sage tint) */
.section-surface { background-color: var(--surface) !important; }
```

- [ ] **Step 4: Add navigation styles**

```css
/* --- Navigation --- */
/* Logo sizing */
.header-title-logo img,
.site-navigation--option-logo-only .header-title-logo img {
  height: 52px !important;
  width: auto !important;
  object-fit: contain;
}

/* Nav link styles */
.header-nav-item a {
  font-family: system-ui, sans-serif;
  font-size: 11px;
  letter-spacing: 0.5px;
  text-transform: uppercase;
  color: var(--text-body) !important;
  transition: color 0.2s;
}

.header-nav-item a:hover { color: var(--sage) !important; }

/* Active page nav link */
.header-nav-item--active a {
  color: var(--sage) !important;
  border-bottom: 2px solid var(--gold);
  padding-bottom: 2px;
}

/* Contact nav button — pill style */
.header-nav-item:last-child a {
  background: var(--gold);
  color: var(--text-dark) !important;
  padding: 6px 16px;
  border-radius: var(--radius-pill);
  font-weight: 700;
  border-bottom: none !important;
}

.header-nav-item:last-child a:hover {
  background: #e6b820;
  color: var(--text-dark) !important;
}

/* Nav background */
.header-inner { background-color: var(--cream) !important; }
.header { border-bottom: 1px solid var(--border-gold); }
```

- [ ] **Step 5: Add button styles**

```css
/* --- Buttons --- */
.sqs-block-button-element,
.btn-primary {
  font-family: system-ui, sans-serif !important;
  font-size: 13px !important;
  font-weight: 700 !important;
  border-radius: var(--radius-pill) !important;
  padding: 12px 28px !important;
  letter-spacing: 0.3px;
  transition: all 0.2s;
}

/* Primary button — gold */
.sqs-block-button-element--small,
.sqs-block-button-element--medium {
  background-color: var(--gold) !important;
  color: var(--text-dark) !important;
  border: none !important;
}

.sqs-block-button-element--small:hover,
.sqs-block-button-element--medium:hover {
  background-color: #e6b820 !important;
}

/* Outline button — sage */
.sqs-block-button-element--large {
  background-color: transparent !important;
  color: var(--sage) !important;
  border: 2px solid var(--sage) !important;
}

.sqs-block-button-element--large:hover {
  background-color: var(--sage) !important;
  color: #fff !important;
}
```

- [ ] **Step 6: Add card, footer, and page hero styles**

```css
/* --- Cards --- */
.dw-card {
  background: var(--cream);
  border-radius: var(--radius-lg);
  overflow: hidden;
  box-shadow: var(--shadow-card);
}

.dw-card--gold { border-top: 3px solid var(--gold); }
.dw-card--sage { border-top: 3px solid var(--sage); }

/* --- Page Hero (inner pages) --- */
.dw-page-hero {
  background: linear-gradient(160deg, var(--cream) 0%, var(--surface) 100%);
  padding: var(--section-pad);
  text-align: center;
}

/* --- Footer --- */
footer, .footer-inner {
  background-color: #2d2218 !important;
}

footer a, .footer-nav-item a {
  font-family: system-ui, sans-serif !important;
  font-size: 10px !important;
  color: #7a6a5a !important;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.footer-copyright { color: #7a6a5a; font-size: 10px; font-family: system-ui, sans-serif; }

/* --- Accordion Block (FAQ page) --- */
.sqs-block-accordion .accordion-item {
  border: 1px solid #e8e0d0;
  border-radius: var(--radius-sm);
  margin-bottom: 6px;
  overflow: hidden;
}

.sqs-block-accordion .accordion-item-title {
  font-family: 'Cormorant Garamond', Georgia, serif !important;
  font-style: italic;
  font-size: 14px !important;
  color: var(--text-dark) !important;
  background: var(--cream);
  padding: 14px 18px;
}

.sqs-block-accordion .accordion-item-title::after {
  color: var(--gold);
  font-weight: 700;
}

.sqs-block-accordion .accordion-item-content {
  font-family: system-ui, sans-serif;
  font-size: 12px;
  line-height: 1.75;
  color: var(--text-body);
  padding: 14px 18px;
  background: #fff;
  border-top: 1px solid #e8e0d0;
}

/* --- Blog: Featured first post override --- */
.blog-list-item:first-child {
  grid-column: 1 / -1;  /* span full width */
}

.blog-list-item:first-child .blog-list-item-image-wrapper {
  height: 300px;
}

/* ⚠ Note: Verify selector against live Squarespace 7.1 blog page —
   actual generated class names may differ. Inspect in DevTools. */
```

- [ ] **Step 7: Verify the CSS file renders correctly**

Open `E:\dandelionwishes\css\dandelion-wishes.css` in a browser (or editor with preview). Confirm:
- No syntax errors
- All CSS custom properties are defined before use
- Font imports are at the very top

- [ ] **Step 8: Commit**

```bash
git -C E:/dandelionwishes init
git -C E:/dandelionwishes add css/dandelion-wishes.css
git -C E:/dandelionwishes commit -m "feat: add global custom CSS with design tokens, typography, nav, buttons"
```

---

## Task 2: Homepage Code Injection Blocks

**Files:**
- Create: `E:\dandelionwishes\code-blocks\hero-section.html`
- Create: `E:\dandelionwishes\code-blocks\services-cards.html`
- Create: `E:\dandelionwishes\code-blocks\about-snippet.html`
- Create: `E:\dandelionwishes\code-blocks\bottom-cta.html`

### 2a — Hero Section

- [ ] **Step 1: Write hero-section.html**

```html
<!-- DANDELION WISHES — Homepage Hero
     Squarespace: Home page > Add Block > Code > paste this -->
<style>
.dw-hero {
  background: linear-gradient(160deg, #fffdf0 0%, #f5f9f0 100%);
  display: grid;
  grid-template-columns: 1fr 1fr;
  min-height: 380px;
  overflow: hidden;
}
.dw-hero__text {
  padding: 48px 40px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: relative;
}
.dw-hero__eyebrow {
  font-family: system-ui, sans-serif;
  font-size: 10px;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: #7a9e7e;
  font-weight: 700;
  margin-bottom: 14px;
}
.dw-hero__headline {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-size: clamp(26px, 4vw, 38px);
  font-style: italic;
  color: #3d3028;
  line-height: 1.25;
  margin-bottom: 16px;
}
.dw-hero__headline .accent-sage { color: #7a9e7e; }
.dw-hero__headline .accent-gold { color: #f4c430; }
.dw-hero__sub {
  font-family: system-ui, sans-serif;
  font-size: 13px;
  color: #6a5a4a;
  line-height: 1.7;
  margin-bottom: 28px;
  max-width: 300px;
}
.dw-hero__ctas { display: flex; gap: 12px; flex-wrap: wrap; }
.dw-btn-primary {
  display: inline-block;
  background: #f4c430;
  color: #3d3028;
  padding: 12px 28px;
  border-radius: 30px;
  font-family: system-ui, sans-serif;
  font-size: 13px;
  font-weight: 700;
  text-decoration: none;
  transition: background 0.2s;
}
.dw-btn-primary:hover { background: #e6b820; }
.dw-btn-outline {
  display: inline-block;
  background: transparent;
  color: #7a9e7e;
  padding: 12px 28px;
  border-radius: 30px;
  border: 2px solid #7a9e7e;
  font-family: system-ui, sans-serif;
  font-size: 13px;
  font-weight: 600;
  text-decoration: none;
  transition: all 0.2s;
}
.dw-btn-outline:hover { background: #7a9e7e; color: #fff; }
.dw-hero__photo {
  position: relative;
  overflow: hidden;
}
.dw-hero__photo img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
}
.dw-hero__photo::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(to right, #fffdf0 0%, transparent 28%);
  z-index: 1;
}
@media (max-width: 767px) {
  .dw-hero { grid-template-columns: 1fr; }
  .dw-hero__photo { height: 240px; }
  .dw-hero__text { padding: 36px 24px; }
}
</style>

<div class="dw-hero">
  <div class="dw-hero__text">
    <div class="dw-hero__eyebrow">Child Counseling &amp; Play Therapy · Thornton, CO</div>
    <div class="dw-hero__headline">
      A safe place for children to
      <span class="accent-sage">process, play,</span>
      learn, and <span class="accent-gold">grow</span>
    </div>
    <div class="dw-hero__sub">
      Cat Ianni-Schlecht, MA, LPC, RPT — Licensed Professional Counselor &amp;
      Registered Play Therapist serving children, teens, and families.
    </div>
    <div class="dw-hero__ctas">
      <a href="/contact" class="dw-btn-primary">Get in Touch</a>
      <a href="/about" class="dw-btn-outline">Learn More</a>
    </div>
  </div>
  <div class="dw-hero__photo">
    <img
      src="https://images.squarespace-cdn.com/content/v1/6945cb2027be636b679bba8a/dd15c8bd-a84e-44f7-9be4-e1a3fee44b3f/shutterstock_339633185+%281%29.jpg"
      alt="Child blowing dandelion seeds — play therapy in Thornton Colorado"
    />
  </div>
</div>
```

- [ ] **Step 2: Open hero-section.html in a browser and visually verify**

Check:
- Split layout renders (text left, photo right)
- Gradient fade on left edge of photo
- Gold and sage headline accents appear
- Both buttons render correctly
- Collapses to single column below 767px

### 2b — Services Cards

- [ ] **Step 3: Write services-cards.html**

```html
<!-- DANDELION WISHES — Homepage Services Cards
     Squarespace: Home page > Add Block > Code > paste this
     ⚠ Replace Unsplash image URLs with final licensed photos before launch -->
<style>
.dw-services { background: #fff; padding: 44px 32px; }
.dw-services__header { text-align: center; margin-bottom: 28px; }
.dw-services__label {
  font-family: system-ui, sans-serif;
  font-size: 10px;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: #7a9e7e;
  font-weight: 700;
  margin-bottom: 8px;
}
.dw-services__title {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-size: 24px;
  font-style: italic;
  color: #3d3028;
}
.dw-services__grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
  max-width: 900px;
  margin: 0 auto;
}
.dw-service-card {
  background: #fffdf0;
  border-radius: 14px;
  overflow: hidden;
  box-shadow: 0 2px 12px rgba(0,0,0,0.07);
  display: flex;
  flex-direction: column;
}
.dw-service-card__img {
  height: 180px;
  overflow: hidden;
  background: #f5f0e8; /* fallback while photos are pending */
}
.dw-service-card__img img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s;
}
.dw-service-card:hover .dw-service-card__img img { transform: scale(1.04); }
.dw-service-card__body {
  padding: 18px 16px 20px;
  flex: 1;
  display: flex;
  flex-direction: column;
}
.dw-service-card--gold { border-top: 3px solid #f4c430; }
.dw-service-card--sage { border-top: 3px solid #7a9e7e; }
.dw-service-card__title {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-size: 16px;
  font-style: italic;
  font-weight: 700;
  color: #3d3028;
  margin-bottom: 8px;
}
.dw-service-card__desc {
  font-family: system-ui, sans-serif;
  font-size: 12px;
  color: #6a5a4a;
  line-height: 1.65;
  flex: 1;
}
.dw-service-card__link {
  display: inline-block;
  margin-top: 14px;
  font-family: system-ui, sans-serif;
  font-size: 12px;
  font-weight: 700;
  color: #7a9e7e;
  text-decoration: none;
}
.dw-service-card__link:hover { text-decoration: underline; }
@media (max-width: 767px) {
  .dw-services__grid { grid-template-columns: 1fr; }
}
</style>

<div class="dw-services">
  <div class="dw-services__header">
    <div class="dw-services__label">How I Can Help</div>
    <div class="dw-services__title">Services for children &amp; families</div>
  </div>
  <div class="dw-services__grid">

    <div class="dw-service-card dw-service-card--gold">
      <div class="dw-service-card__img">
        <!-- ⚠ Replace with final licensed photo -->
        <img src="REPLACE_WITH_CHILD_THERAPY_PHOTO" alt="Child playing during play therapy session" />
      </div>
      <div class="dw-service-card__body">
        <div class="dw-service-card__title">Child Therapy</div>
        <div class="dw-service-card__desc">Play-based therapy for children ages 3–12 to safely explore big emotions, work through challenges, and build lasting coping skills.</div>
        <a href="/services" class="dw-service-card__link">Learn more →</a>
      </div>
    </div>

    <div class="dw-service-card dw-service-card--sage">
      <div class="dw-service-card__img">
        <!-- ⚠ Replace with final licensed photo -->
        <img src="REPLACE_WITH_TEEN_THERAPY_PHOTO" alt="Teen in counseling session" />
      </div>
      <div class="dw-service-card__body">
        <div class="dw-service-card__title">Teen Therapy</div>
        <div class="dw-service-card__desc">Supportive counseling for adolescents navigating anxiety, identity, school stress, and life transitions in a judgment-free space.</div>
        <a href="/services" class="dw-service-card__link">Learn more →</a>
      </div>
    </div>

    <div class="dw-service-card dw-service-card--gold">
      <div class="dw-service-card__img">
        <!-- ⚠ Replace with final licensed photo -->
        <img src="REPLACE_WITH_PARENT_COACHING_PHOTO" alt="Parent and child together" />
      </div>
      <div class="dw-service-card__body">
        <div class="dw-service-card__title">Parent Coaching</div>
        <div class="dw-service-card__desc">Practical, compassionate strategies to strengthen your family's connection and better understand your child's emotional world.</div>
        <a href="/services" class="dw-service-card__link">Learn more →</a>
      </div>
    </div>

  </div>
</div>
```

- [ ] **Step 4: Write about-snippet.html**

```html
<!-- DANDELION WISHES — Homepage About Snippet
     Squarespace: Home page > Add Block > Code > paste this -->
<style>
.dw-about-snippet {
  background: #f5f9f0;
  padding: 44px 32px;
  display: flex;
  gap: 32px;
  align-items: center;
  max-width: 900px;
  margin: 0 auto;
}
.dw-about-snippet__photo {
  width: 110px;
  height: 110px;
  border-radius: 50%;
  overflow: hidden;
  flex-shrink: 0;
  border: 4px solid #fff;
  box-shadow: 0 2px 12px rgba(0,0,0,0.12);
}
.dw-about-snippet__photo img { width: 100%; height: 100%; object-fit: cover; object-position: center top; }
.dw-about-snippet__label {
  font-family: system-ui, sans-serif;
  font-size: 10px;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: #7a9e7e;
  font-weight: 700;
  margin-bottom: 6px;
}
.dw-about-snippet__name {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-size: 20px;
  font-style: italic;
  color: #3d3028;
  margin-bottom: 10px;
}
.dw-about-snippet__bio {
  font-family: system-ui, sans-serif;
  font-size: 13px;
  color: #5a4a3a;
  line-height: 1.7;
  max-width: 480px;
  margin-bottom: 14px;
}
.dw-about-snippet__link {
  font-family: system-ui, sans-serif;
  font-size: 13px;
  font-weight: 700;
  color: #7a9e7e;
  text-decoration: underline;
}
@media (max-width: 600px) {
  .dw-about-snippet { flex-direction: column; text-align: center; }
}
</style>

<div class="dw-about-snippet">
  <div class="dw-about-snippet__photo">
    <img
      src="https://images.squarespace-cdn.com/content/v1/6945cb2027be636b679bba8a/282c19c3-c309-483b-aac9-f376ae2fde2a/IMG_2279.png"
      alt="Cat Ianni-Schlecht, Licensed Professional Counselor and Registered Play Therapist in Thornton, CO"
    />
  </div>
  <div>
    <div class="dw-about-snippet__label">Meet Your Therapist</div>
    <div class="dw-about-snippet__name">Cat Ianni-Schlecht, MA, LPC, NCC, RPT</div>
    <div class="dw-about-snippet__bio">
      Licensed Professional Counselor and Registered Play Therapist dedicated to creating
      a warm, play-filled space where children can express themselves safely and begin to heal.
    </div>
    <a href="/about" class="dw-about-snippet__link">Read Cat's full bio →</a>
  </div>
</div>
```

- [ ] **Step 5: Write bottom-cta.html (reusable across all pages)**

```html
<!-- DANDELION WISHES — Bottom CTA Section (reusable)
     Squarespace: Any page > Add Block > Code > paste this
     Customize headline/subtext per page as needed -->
<style>
.dw-bottom-cta {
  background: #3d3028;
  padding: 44px 32px;
  text-align: center;
}
.dw-bottom-cta__headline {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-size: clamp(20px, 3vw, 26px);
  font-style: italic;
  color: #fff8dc;
  margin-bottom: 10px;
}
.dw-bottom-cta__sub {
  font-family: system-ui, sans-serif;
  font-size: 13px;
  color: #c4b48a;
  line-height: 1.7;
  max-width: 400px;
  margin: 0 auto 24px;
}
.dw-bottom-cta__btn {
  display: inline-block;
  background: #f4c430;
  color: #3d3028;
  padding: 13px 36px;
  border-radius: 30px;
  font-family: system-ui, sans-serif;
  font-size: 13px;
  font-weight: 700;
  text-decoration: none;
  transition: background 0.2s;
}
.dw-bottom-cta__btn:hover { background: #e6b820; }
.dw-bottom-cta__contact {
  margin-top: 18px;
  font-family: system-ui, sans-serif;
  font-size: 11px;
  color: #8a7a5a;
}
</style>

<div class="dw-bottom-cta">
  <div class="dw-bottom-cta__headline">Ready to take the first step?</div>
  <div class="dw-bottom-cta__sub">
    Reach out to schedule a free 15-minute phone consultation.
    No commitment required — just a conversation.
  </div>
  <a href="/contact" class="dw-bottom-cta__btn">Get in Touch</a>
  <div class="dw-bottom-cta__contact">
    (303) 656-9362 &nbsp;·&nbsp; Cat@dandelionwishescounseling.com
  </div>
</div>
```

- [ ] **Step 6: Open each .html file in a browser and visually verify**

Check against approved mockup at `E:\dandelionwishes\.superpowers\brainstorm\922-1774567168\homepage-layout-v3.html`.

- [ ] **Step 7: Commit**

```bash
git -C E:/dandelionwishes add code-blocks/
git -C E:/dandelionwishes commit -m "feat: add homepage code injection blocks (hero, services, about snippet, bottom CTA)"
```

---

## Task 3: Inner Page Code Injection Blocks

**Files:**
- Create: `E:\dandelionwishes\code-blocks\credential-badges.html`
- Create: `E:\dandelionwishes\code-blocks\hipaa-notice.html`

### 3a — Credential Badges (About page)

- [ ] **Step 1: Write credential-badges.html**

```html
<!-- DANDELION WISHES — Credential Badges (About page)
     Squarespace: About page > left column > Add Block > Code > paste this -->
<style>
.dw-credentials { display: flex; flex-direction: column; gap: 8px; margin-top: 16px; }
.dw-credential {
  background: #fffdf0;
  border-radius: 8px;
  padding: 10px 12px;
  font-family: system-ui, sans-serif;
  font-size: 11px;
  font-weight: 600;
  color: #3d3028;
}
.dw-credential--gold { border-left: 3px solid #f4c430; }
.dw-credential--sage { border-left: 3px solid #7a9e7e; }
</style>

<div class="dw-credentials">
  <div class="dw-credential dw-credential--gold">MA — Master of Arts</div>
  <div class="dw-credential dw-credential--sage">LPC — Licensed Professional Counselor</div>
  <div class="dw-credential dw-credential--gold">NCC — Nationally Certified Counselor</div>
  <div class="dw-credential dw-credential--sage">RPT — Registered Play Therapist</div>
</div>
```

### 3b — HIPAA Notice (Contact page)

- [ ] **Step 2: Write hipaa-notice.html**

```html
<!-- DANDELION WISHES — HIPAA Notice (Contact page)
     Squarespace: Contact page > above the form > Add Block > Code > paste this -->
<style>
.dw-hipaa-notice {
  background: #fff8dc;
  border: 1px solid rgba(244,196,48,0.4);
  border-radius: 10px;
  padding: 14px 16px;
  display: flex;
  gap: 12px;
  align-items: flex-start;
  margin-bottom: 20px;
  max-width: 560px;
}
.dw-hipaa-notice__icon { font-size: 16px; flex-shrink: 0; }
.dw-hipaa-notice__text {
  font-family: system-ui, sans-serif;
  font-size: 11px;
  color: #6a4a10;
  line-height: 1.65;
}
.dw-hipaa-notice__text strong { font-weight: 700; }
</style>

<div class="dw-hipaa-notice">
  <div class="dw-hipaa-notice__icon">⚠️</div>
  <div class="dw-hipaa-notice__text">
    <strong>Please do not include sensitive personal health information in this form.</strong>
    This contact form is not a HIPAA-secure channel. For confidential communication,
    please call or email directly.
  </div>
</div>
```

- [ ] **Step 3: Open both files in a browser and verify appearance**

- [ ] **Step 4: Commit**

```bash
git -C E:/dandelionwishes add code-blocks/credential-badges.html code-blocks/hipaa-notice.html
git -C E:/dandelionwishes commit -m "feat: add About credential badges and Contact HIPAA notice blocks"
```

---

## Task 4: Schema Markup (SEO)

**Files:**
- Create: `E:\dandelionwishes\code-blocks\schema-markup.html`

- [ ] **Step 1: Write schema-markup.html**

```html
<!-- DANDELION WISHES — LocalBusiness JSON-LD Schema
     Squarespace: Settings > Advanced > Code Injection > HEADER > paste this
     ⚠ Fill in openingHoursSpecification once Cat confirms office hours
     ⚠ Add sameAs URLs (Psychology Today, etc.) when available -->
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
  },
  "sameAs": []
}
</script>
```

- [ ] **Step 2: Validate the JSON-LD**

Paste the `<script>` block contents into Google's Rich Results Test:
`https://search.google.com/test/rich-results`

Expected: No errors. Warnings about missing `openingHoursSpecification` are acceptable — add once Cat confirms hours.

- [ ] **Step 3: Commit**

```bash
git -C E:/dandelionwishes add code-blocks/schema-markup.html
git -C E:/dandelionwishes commit -m "feat: add LocalBusiness JSON-LD schema markup for header injection"
```

---

## Task 5: SEO Reference Document

**Files:**
- Create: `E:\dandelionwishes\seo\page-seo-reference.md`

- [ ] **Step 1: Write the SEO reference doc**

```markdown
# Dandelion Wishes Counseling — Page SEO Reference

Copy/paste these values into Squarespace for each page:
**Pages > [Page Name] > Settings > SEO**

---

## Home
- **Page Title:** Child Therapy & Play Therapy in Thornton, CO | Dandelion Wishes Counseling
- **Meta Description:** Cat Ianni-Schlecht, LPC, RPT offers play therapy and child counseling in Thornton, CO. Serving children, teens & families. Call (303) 656-9362.
- **URL Slug:** / (homepage — no slug needed)
- **Social Image:** Upload the dandelion child photo

## About
- **Page Title:** About Cat Ianni-Schlecht, LPC, RPT | Dandelion Wishes Counseling
- **Meta Description:** Meet Cat Ianni-Schlecht, Licensed Professional Counselor & Registered Play Therapist in Thornton, CO. Compassionate, child-centered therapy.
- **URL Slug:** about
- **Social Image:** Cat's headshot

## Services & Fees
- **Page Title:** Play Therapy Services & Fees | Dandelion Wishes Counseling
- **Meta Description:** Child therapy, teen counseling & parent coaching in Thornton, CO. Sessions $125. Learn about Cat's play therapy approach and service offerings.
- **URL Slug:** services
- **Social Image:** Dandelion child photo

## FAQ
- **Page Title:** Play Therapy FAQ | Dandelion Wishes Counseling | Thornton CO
- **Meta Description:** Answers to common questions about play therapy, child counseling, and getting started with Cat Ianni-Schlecht, LPC, RPT in Thornton, Colorado.
- **URL Slug:** faq

## Blog
- **Page Title:** Resources for Families | Dandelion Wishes Counseling
- **Meta Description:** Articles on child development, play therapy, and supporting your family's emotional wellbeing — from Cat Ianni-Schlecht, LPC, RPT in Thornton, CO.
- **URL Slug:** blog

## Contact
- **Page Title:** Contact | Dandelion Wishes Counseling | Thornton CO
- **Meta Description:** Reach Cat Ianni-Schlecht for child therapy & play therapy in Thornton, CO. Call (303) 656-9362 or email Cat@dandelionwishescounseling.com.
- **URL Slug:** contact

---

## Global SEO Settings
**Settings > SEO:**
- Site Title: Dandelion Wishes Counseling
- Site Description: Child counseling, play therapy, and teen therapy in Thornton, Colorado.

## After Launch
- [ ] Connect Google Search Console (Settings > Connected Accounts)
- [ ] Verify sitemap at dandelionwishescounseling.com/sitemap.xml
- [ ] Claim/verify Google Business Profile at Thornton, CO address
- [ ] Set Google Business category: Mental Health Service (primary)
```

- [ ] **Step 2: Commit**

```bash
git -C E:/dandelionwishes add seo/page-seo-reference.md
git -C E:/dandelionwishes commit -m "feat: add page SEO reference doc with titles, meta descriptions, slugs"
```

---

## Task 6: Squarespace Setup Guide

**Files:**
- Create: `E:\dandelionwishes\docs\squarespace-setup-guide.md`

- [ ] **Step 1: Write the setup guide**

The guide must be plain-language enough for Cat to follow without a developer. Cover:

```markdown
# Dandelion Wishes Counseling — Squarespace Setup Guide

## Before You Start
- [ ] Back up the current site (Squarespace: Settings > Advanced > Export)
- [ ] Confirm you have login access to dandelionwishescounseling.com on Squarespace

---

## Step 1: Switch to a New Template
1. In Squarespace editor: **Design > Template**
2. Click **"Switch Template"**
3. Search for **"Clove"** or **"Farro"** — select either one
4. Confirm the switch (your content is preserved)

---

## Step 2: Add the Custom CSS
1. Go to **Design > Custom CSS**
2. Delete any existing CSS
3. Open `css/dandelion-wishes.css` from this folder
4. Copy the entire file contents and paste it in
5. Click **Save**

---

## Step 3: Add the Header Schema (SEO)
1. Go to **Settings > Advanced > Code Injection**
2. In the **Header** field, paste the contents of `code-blocks/schema-markup.html`
3. Click **Save**

---

## Step 4: Set Up Pages

### Add the Blog page (important — must be Blog type, not regular page)
1. In **Pages**, click **+** to add a new page
2. Choose **Blog** (not Blank or Layout)
3. Name it "Blog"
4. Set slug to `blog` in page settings
5. In Blog Settings, set layout to **Grid**

### Set up all other pages
Add or rename pages to match:
- Home (already exists)
- About
- Services & Fees → slug: `services`
- FAQ → slug: `faq`
- Blog (created above)
- Contact → slug: `contact`

---

## Step 5: Add Code Blocks to Each Page

For each code block, go to the page in the editor and add a **Code Block**:
Click **+** > **More** > **Code**

| File | Page | Position |
|------|------|----------|
| `hero-section.html` | Home | Top of page, first block |
| `services-cards.html` | Home | After hero |
| `about-snippet.html` | Home | After services |
| `bottom-cta.html` | Home, About, Services, FAQ, Contact | Bottom of each page |
| `credential-badges.html` | About | Left column, below headshot image |
| `hipaa-notice.html` | Contact | Above the contact form |

---

## Step 6: Add Photos

Photos needed (upload via **Media > Images** or directly in each block):
- [ ] Service card — Child Therapy
- [ ] Service card — Teen Therapy
- [ ] Service card — Parent Coaching
- [ ] Cat's headshot (higher resolution if available)

After uploading, update the `src` URLs in `services-cards.html` with the new Squarespace CDN URLs.

---

## Step 7: Fill In Content Placeholders

- [ ] Update bio text on About page
- [ ] Add insurance list to Services & Fees page
- [ ] Add office hours to Contact page
- [ ] Add FAQ answers to all 9 questions
- [ ] Confirm telehealth availability (yes/no) for FAQ

---

## Step 8: Apply SEO Settings

Follow `seo/page-seo-reference.md` — set the title, meta description, and slug for each page in:
**Pages > [Page] > Settings (gear icon) > SEO tab**

---

## Step 9: Configure the Contact Form
1. On the Contact page, add a **Form Block**
2. Add fields: First Name, Last Name, Email, Phone (optional), Message
3. In Form settings, set the notification email to Cat@dandelionwishescounseling.com
4. Set a confirmation message: "Thank you! Cat will be in touch as soon as possible."

---

## Step 10: Before Publishing
- [ ] Preview every page on mobile (use Squarespace's mobile preview)
- [ ] Click every nav link — confirm all pages load
- [ ] Submit the contact form as a test
- [ ] Check that the logo displays correctly in the header
- [ ] Verify the Google Map loads on the Contact page
- [ ] Connect Google Search Console (Settings > Connected Accounts)
```

- [ ] **Step 2: Commit**

```bash
git -C E:/dandelionwishes add docs/squarespace-setup-guide.md
git -C E:/dandelionwishes commit -m "feat: add Squarespace setup guide for Cat"
```

---

## Task 7: Final Review & Handoff

- [ ] **Step 1: Open all approved mockups and compare against deliverables**

Open side-by-side:
- Approved mockup: `E:\dandelionwishes\.superpowers\brainstorm\922-1774567168\homepage-layout-v3.html`
- Implemented block: open `code-blocks\hero-section.html` + `services-cards.html` in browser

Verify visual parity for: colors, typography, layout, button styles, spacing.

- [ ] **Step 2: Validate schema markup**

Paste `code-blocks/schema-markup.html` contents into `https://search.google.com/test/rich-results`
Expected: Valid LocalBusiness entity, no errors.

- [ ] **Step 3: Spell-check all copy in code blocks**

Read through every `.html` file. Fix any typos before handoff.

- [ ] **Step 4: Replace placeholder image URLs**

Search for `REPLACE_WITH_` in `code-blocks/services-cards.html`.
If Cat has not yet provided photos, leave as-is and add a clear comment. Do not use Unsplash URLs in production (licensing).

- [ ] **Step 5: Final commit and zip for handoff**

```bash
git -C E:/dandelionwishes add -A
git -C E:/dandelionwishes commit -m "chore: final review pass — ready for Squarespace handoff"
```

Then zip the `E:\dandelionwishes` folder and share with Cat alongside the setup guide.

---

## Content Blockers (cannot launch without these from Cat)

| Item | Needed For |
|------|-----------|
| 3 service card photos | services-cards.html, services page |
| Insurance list | Services & Fees page |
| Office hours | Contact page + schema markup |
| FAQ answers (9 questions) | FAQ page |
| Telehealth yes/no | FAQ page |
| Updated bio text | About page |
