# Dandelion Wishes Counseling — Squarespace Setup Guide

This guide walks you through setting up your new website design in Squarespace, step by step. You'll be switching to a new template and applying custom code that gives your site its look and feel.

**Before you start:** Make a note of your Squarespace login credentials. All steps below happen inside your Squarespace account at squarespace.com.

---

## Step 1 — Switch to a New Template

Your current template will be replaced with a Squarespace 7.1 template. **Your pages and content are safe** — Squarespace preserves all content when you switch templates.

1. Log in to Squarespace
2. Go to **Design > Template**
3. Click **Switch Template**
4. Search for **Clove** (recommended) or **Farro**
5. Click **Select** and confirm

---

## Step 2 — Add the Google Fonts

Your site uses two custom fonts (Cormorant Garamond for headings, Source Serif 4 for body text). These must be loaded before the CSS is applied.

1. Go to **Settings > Advanced > Code Injection**
2. In the **Header** field, paste the following at the very top (before anything else already there):

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,600;0,700;1,400;1,600;1,700&family=Source+Serif+4:ital,wght@0,400;1,400&display=swap" rel="stylesheet">
```

3. Click **Save**

---

## Step 3 — Apply the Custom CSS

1. Go to **Design > Custom CSS**
2. Delete any existing CSS in the panel (or select all and replace)
3. Open the file `css/dandelion-wishes.css` from your design files
4. Copy the entire contents and paste into the Custom CSS panel
5. Click **Save**

Your site colors, fonts, and spacing will update immediately.

---

## Step 4 — Add the Schema Markup (SEO)

This adds invisible structured data that helps Google understand your business.

1. Go to **Settings > Advanced > Code Injection**
2. In the **Header** field, paste the contents of `code-blocks/schema-markup.html` after the font links from Step 2
3. Click **Save**

> **Note:** Update the schema once you have confirmed office hours — see the TODO comments inside that file.

---

## Step 5 — Set Up Your Pages

Add the following pages in **Pages** (left sidebar). Use these exact URL slugs.

| Page Name | URL Slug | Type |
|-----------|----------|------|
| Home | *(default)* | Regular page |
| About | `about` | Regular page |
| Services & Fees | `services` | Regular page |
| FAQ | `faq` | Regular page |
| Blog | `blog` | **Blog page** (see note below) |
| Contact | `contact` | Regular page |

> **Blog page note:** The Blog page must be added as a **Blog** page type (not a regular page). In the Pages panel, click the **+** button and choose **Blog** from the list. Name it "Blog" and set the URL slug to `blog`.

---

## Step 6 — Set Page SEO Titles & Meta Descriptions

For each page:
1. Click the page in the Pages panel
2. Click the **gear icon** (Settings)
3. Go to the **SEO** tab
4. Enter the title and meta description from `seo/page-seo-reference.md`
5. Click **Save**

---

## Step 7 — Add Code Blocks to Each Page

Each page section below lists which code block file to use. In Squarespace, add a **Code Block** to the page and paste the file contents.

### Home Page

| Section | Code Block File |
|---------|----------------|
| Hero (split layout) | `code-blocks/hero-section.html` |
| Services (3 cards) | `code-blocks/services-cards.html` |
| About snippet | `code-blocks/about-snippet.html` |
| Bottom CTA | `code-blocks/bottom-cta.html` |

> **Service card photos:** The service cards are currently showing a plain background. Once you have photos for child therapy, teen therapy, and parent coaching, upload them to Squarespace and add the image URLs to `services-cards.html` where indicated by the `⚠` comments.

### About Page

| Section | Code Block File |
|---------|----------------|
| Credential badges (sidebar) | `code-blocks/credential-badges.html` |
| Bottom CTA | `code-blocks/bottom-cta.html` |

### Services & Fees Page

| Section | Code Block File |
|---------|----------------|
| Bottom CTA | `code-blocks/bottom-cta.html` |

### Contact Page

| Section | Code Block File |
|---------|----------------|
| HIPAA notice (above form) | `code-blocks/hipaa-notice.html` |

### FAQ Page

Use Squarespace's native **Accordion Block** for the FAQ questions. Add one Accordion Block per group:
- Group 1: About Play Therapy
- Group 2: Getting Started
- Group 3: Practical Questions

### Blog Page

The Blog page layout is handled automatically by Squarespace once the Custom CSS is applied. The custom CSS features your first (most recent) post in a larger card. No code block needed.

---

## Step 8 — Add a Google Map to the Contact Page

1. On the Contact page, add a **Map Block**
2. Enter the address: `2090 East 104th Ave, Suite 302, Thornton, CO`
3. Squarespace will display an embedded Google Map

---

## Step 9 — Configure the Contact Form

Use Squarespace's native **Form Block** on the Contact page. Add these fields:
- First Name (Short Answer, required)
- Last Name (Short Answer, required)
- Email (Email, required)
- Phone (Phone, optional)
- What brings you here? (Long Answer, required)

Set the submit button label to **Send Message**.

In the form settings, set the **Post-submit message** to something like:
> "Thank you for reaching out. Cat will be in touch as soon as possible."

Configure the **Email Notifications** in form settings to send responses to `Cat@dandelionwishescounseling.com`.

---

## Step 10 — Upload Images

Upload these images to Squarespace's asset library or set them directly in the image blocks:

| Image | Where Used |
|-------|-----------|
| Logo (PNG) | Nav — set under Design > Logo & Title |
| Child blowing dandelion (hero photo) | Home page hero section |
| Cat's headshot | About page, Home page About snippet |
| Child therapy photo *(to be sourced)* | Services & Fees page, Home service cards |
| Teen therapy photo *(to be sourced)* | Services & Fees page, Home service cards |
| Parent coaching photo *(to be sourced)* | Services & Fees page, Home service cards |

---

## Step 11 — Set Global SEO Settings

1. Go to **Settings > SEO**
2. Set **Site Title:** `Dandelion Wishes Counseling`
3. Set **Site Description:** `Child counseling, play therapy, and teen therapy in Thornton, Colorado.`
4. Click **Save**

---

## Step 12 — Pre-Launch Checklist

Before making the site live, verify each item:

- [ ] All 6 pages created with correct URL slugs
- [ ] Page SEO titles and meta descriptions entered for all pages
- [ ] Google Fonts loading correctly (headings display in italic serif)
- [ ] Custom CSS applied (warm cream background, gold and sage accents)
- [ ] Schema markup added to header injection
- [ ] Contact form submits and triggers email to Cat
- [ ] Google Map loads on Contact page
- [ ] HIPAA notice visible above contact form
- [ ] Logo displays correctly in nav on desktop and mobile
- [ ] Nav collapses correctly on mobile (Squarespace handles this)
- [ ] All links in nav and footer resolve correctly
- [ ] Blog page set up as Blog type (not regular page)
- [ ] At least one blog post published before launch
- [ ] Google Business Profile claimed and NAP matches site
- [ ] Connect Google Search Console (Settings > Connected Accounts)

---

## Content Still Needed

Before the site can launch, provide:

- [ ] Updated bio text for the About page
- [ ] Office hours (for Contact page and schema markup)
- [ ] 3 service photos (child therapy, teen therapy, parent coaching)
- [ ] Insurance accepted list (for Services & Fees page)
- [ ] FAQ answers for all 9 questions
- [ ] Telehealth availability (yes or no)
- [ ] At least 1 blog post
- [ ] Psychology Today profile URL (for schema `sameAs` field)

---

## File Reference

```
dandelionwishes/
├── css/
│   └── dandelion-wishes.css          ← Paste into Design > Custom CSS
├── code-blocks/
│   ├── hero-section.html             ← Home: hero
│   ├── services-cards.html           ← Home: service cards
│   ├── about-snippet.html            ← Home: about preview
│   ├── bottom-cta.html               ← Home, About, Services: bottom CTA
│   ├── credential-badges.html        ← About: credential sidebar
│   ├── hipaa-notice.html             ← Contact: form warning
│   └── schema-markup.html            ← Header injection (global, all pages)
└── seo/
    └── page-seo-reference.md         ← Page titles, meta descriptions, slugs
```
