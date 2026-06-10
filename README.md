# Finance Consultancy Landing Page

A single-file static landing page for an Investment Strategy consultancy. Built with plain HTML, CSS, and JavaScript — no build step, no framework, no dependencies.

## Preview

![Landing page screenshot](screenshot.png)

## Live Demo

Deployed via GitHub Pages.

## Features

- Sticky navigation with mobile hamburger menu
- Full-viewport hero section
- Benefits grid, process timeline, testimonials
- Lead magnet section with checklist offer
- Enquiry form with client-side validation (posted via [FormSubmit](https://formsubmit.co))
- Accordion FAQ
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

Everything lives in a single file:

```
index.html   ← all HTML, CSS, and JavaScript
```

The file is organised top-to-bottom: `<head>` styles → nav → hero → why-us → process → testimonials → lead-magnet → enquiry form → FAQ → final CTA → footer → `<script>`.

## Customisation

### Colours

Edit the CSS variables in `:root` to retheme the entire page:

```css
:root {
  --primary:    /* main brand colour */
  --secondary:  /* secondary brand colour */
  --accent:     /* call-to-action colour */
  --background: /* page background */
  --text:       /* body text */
  --light-bg:   /* subtle section backgrounds */
}
```

### Hero Image

Update the `background` property on `#hero` in the `<style>` block. The current image is sourced from Unsplash (no API key required).

### Enquiry Form

Replace the placeholder email in the form's `action` attribute before deploying:

```html
<form action="https://formsubmit.co/YOUR-EMAIL@example.com" method="POST">
```

FormSubmit requires a one-time email confirmation on the first submission from a new domain.

## Deployment

The site is deployed automatically to GitHub Pages via a GitHub Actions workflow on every push to `main`.
