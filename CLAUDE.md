# CLAUDE.md — Aurora Dynamics Website

> This file provides context for Claude Code when working on this project.

## Project Overview

This is the website for **Aurora Dynamics**, an internet marketing consultancy for biotech and life science companies. The site is a static HTML/CSS/JS multi-page website designed to be hosted on **Vercel**.

**Owner:** Ben
**Business:** Helping biotech companies close the gap between sales and marketing through shared projects.
**Target audience:** CCOs and commercial leads at mid-size biotech companies.

## Brand & Design Direction

The full brand reference is in `docs/aurora-dynamics-brand.md`. Key points:

- **Design direction:** Editorial & Warm — like a quality publication, not a tech startup
- **Typography:** Fraunces (serif) for headings, DM Sans (sans-serif) for body. Both loaded from Google Fonts.
- **Color palette:** Aurora Blue (#5c6baf), Biotech Green (#72b452), Deep Charcoal (#2a3132), Warm White (#f7f5f2), Warm Amber (#d4883e) for CTAs
- **Illustration style:** Hand-drawn mixed media biotech illustrations on transparent backgrounds. These sit on light surfaces. The artwork brings energy; the typography stays composed.
- **Voice:** Clear, human, warm, consultative. Confident when it matters but never a know-it-all. "Clear beats clever."
- **Buttons:** Pill-shaped (border-radius: 50px)
- **Headlines:** Use italic Fraunces `<em>` for emphasis on key phrases

## File Structure

```
aurora-dynamics-site/
├── index.html          # Home page
├── services.html       # Services page (4 services)
├── about.html          # About page (Ben's story + principles)
├── contact.html        # Contact page with form
├── styles.css          # Global stylesheet
├── main.js             # Navigation, animations, form handling
├── assets/
│   └── images/
│       ├── Aurora_Dynamics_1.png              # Logo (light background)
│       ├── Aurora_Dynamics_1_dark_transp.png  # Logo (dark background)
│       ├── B006_TB.png                        # Illustration 1
│       └── B025_TB.png                        # Illustration 2
└── docs/
    ├── aurora-dynamics-brand.md               # Brand reference
    └── aurora-dynamics-business-context.md    # Business context
```

## Before Launch Checklist

These items need to be completed before the site goes live:

### Required
- [ ] Add logo files to `assets/images/` (Aurora_Dynamics_1.png and Aurora_Dynamics_1_dark_transp.png)
- [ ] Connect Kit (formerly ConvertKit) — replace placeholder `action="#"` on all `.optin__form` elements with the Kit form action URL
- [ ] Connect contact form backend — options: Formspree (easiest), Netlify Forms, or custom. Update `#contact-form` action and method accordingly
- [ ] Update LinkedIn URL — replace all `href="#"` links labelled "LinkedIn" with Ben's actual profile URL
- [ ] Update Substack URL — replace all `href="#"` links labelled "The Life Science Lead Gap on Substack" with the actual Substack URL
- [ ] Confirm email address on contact page (currently placeholder: ben@auroradynamics.com)
- [ ] Add CookieYes script for GDPR cookie consent — insert before closing `</head>` on all pages. Only load Google Analytics after consent is given.
- [ ] Add Google Analytics script (behind CookieYes consent)
- [ ] Set up custom domain in Vercel dashboard

### Optional / Future
- [ ] Add Vercel Web Analytics (`@vercel/analytics` package — free tier)
- [ ] Add client testimonials to the social proof section on the home page
- [ ] Add client logos to the social proof section
- [ ] Add a blog section when ready
- [ ] Add a favicon (can extract from the logo triangle mark)
- [ ] Add Open Graph meta tags for social sharing
- [ ] Add a privacy policy page (linked from footer)

## Deployment Instructions

### First-time setup

1. **Create a GitHub repository:**
   ```bash
   cd aurora-dynamics-site
   git init
   git add .
   git commit -m "Initial site build"
   gh repo create aurora-dynamics-site --public --source=. --push
   ```

2. **Deploy to Vercel:**
   ```bash
   npm i -g vercel
   vercel login
   vercel --prod
   ```
   
   Or connect via the Vercel dashboard:
   - Go to vercel.com and sign in
   - Click "Add New Project"
   - Import the GitHub repository
   - Framework: Other
   - Build command: (leave empty — static site)
   - Output directory: `.` (root)
   - Click Deploy

3. **Custom domain:**
   - In Vercel dashboard → Project → Settings → Domains
   - Add your domain and follow DNS instructions

### Making updates

After any file changes:
```bash
git add .
git commit -m "Description of changes"
git push
```
Vercel auto-deploys on every push to the main branch.

## Tech Stack

- **Hosting:** Vercel (free tier)
- **Email marketing:** Kit (formerly ConvertKit)
- **Analytics:** Vercel Web Analytics + Google Analytics (with GDPR consent via CookieYes)
- **Cookie consent:** CookieYes (free tier, styled to match brand)
- **Fonts:** Google Fonts (Fraunces + DM Sans)
- **No build step** — pure HTML/CSS/JS, no framework dependencies

## Code Conventions

- CSS uses custom properties (variables) defined in `:root` — always use these rather than hardcoding colors
- All colors follow the brand palette — never use pure white (#fff) or pure black (#000) except in the `.section--white` background
- Animations use the `.fade-up` class with Intersection Observer in main.js
- Navigation active state is set automatically in main.js based on the current filename
- Mobile menu uses `.nav__toggle` and `.nav__links.open` classes
- Newsletter forms use `.optin__form` class — main.js handles the placeholder submit behaviour
- Contact form uses `#contact-form` ID — main.js handles placeholder submit behaviour

## Common Tasks

**Change copy on a page:** Edit the relevant HTML file directly. Keep the voice warm and consultative per the brand guide.

**Add a new service:** Follow the pattern in services.html — alternating `two-col` and `two-col--reverse` layouts with alternating white/light-grey backgrounds.

**Add a testimonial:** Uncomment and populate the `.proof__logos` section in index.html. Add quote cards as needed.

**Change a color:** Update the CSS variable in `:root` in styles.css. It will cascade everywhere.

**Add a new page:** Copy the structure from about.html as a template. Update the nav links on all pages to include the new page.
