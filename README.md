# Finance Consultancy Landing Page

A single-file static landing page for an Investment Strategy consultancy. Built with plain HTML, CSS, and JavaScript — no build step, no framework, no dependencies.

## Preview

![Landing page screenshot](screenshot.png)

## Live Demo

[https://lienchang.github.io/financeconsultancy/](https://lienchang.github.io/financeconsultancy/)

## Features

- Deep navy + warm gold design system (Playfair Display headings, Inter body)
- Sticky navigation with mobile hamburger menu
- Full-viewport hero section with local background image
- Benefits grid, process timeline, testimonials
- Lead magnet section with checklist offer
- Enquiry form with client-side validation (posted via [FormSubmit](https://formsubmit.co))
- Accordion FAQ
- Floating WhatsApp chat widget with pre-filled query buttons
- Scroll-reveal animations using `IntersectionObserver`
- Fully responsive (tablet, mobile, small mobile breakpoints)

## Getting Started

Open `index.html` directly in a browser — no server needed.

For live-reload during development:

```bash
npx serve .
# or
python -m http.server 8080
```

Then visit `http://localhost:8080`.

## Project Structure

```
index.html                                      ← all HTML, CSS, and JavaScript
abstract-business-finance-soft-backdrop_*.jpg   ← hero background image
screenshot.png                                  ← README preview
.claude/skills/frontend-design.md               ← design system skill
```

The file is organised top-to-bottom: `<head>` styles → nav → hero → why-us → process → testimonials → lead-magnet → enquiry form → FAQ → final CTA → footer → `<script>`.

## Customisation

### Colours

Edit the CSS variables in `:root` to retheme the entire page:

```css
:root {
  --primary:    #0a1628;   /* deep navy */
  --secondary:  #1a3a6b;   /* mid navy */
  --accent:     #c9a84c;   /* warm gold — CTAs, icons, highlights */
  --background: #f8f7f4;   /* warm off-white */
  --text:       #1c2b3a;   /* dark navy-grey body copy */
  --light-bg:   #eef1f7;   /* pale blue-grey section backgrounds */
}
```

### Typography

Google Fonts are loaded in `<head>`: **Playfair Display** (headings) and **Inter** (body/UI). To change fonts, update the `<link>` tags and the `--font-serif` / `--font-sans` variables.

### Hero Image

The hero background is the local file `abstract-business-finance-soft-backdrop_522560-22343.jpg`. To change it, drop a new image into the project root and update the `url(...)` in the `#hero` CSS rule.

### Enquiry Form

The form `action` is already set to the destination email. FormSubmit requires a one-time email confirmation on the first submission from a new domain. To change the recipient, update the `action` URL on `#enquiryForm` in `index.html`.

### WhatsApp Widget

The floating WhatsApp button is wired to number `96615077`. To change it, find all `wa.me/96615077` occurrences in the `#wa-widget` HTML block and update the number. If a country code is needed, prefix it (e.g. `wa.me/6096615077`).

## Deployment

The site deploys automatically to GitHub Pages via GitHub Actions on every push to `main`. The workflow includes a Gitleaks secret scan before deployment.
