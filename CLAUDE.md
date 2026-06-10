# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A single-file static landing page for an Investment Strategy consultancy. Everything — HTML, CSS, and JavaScript — lives in one file: `index.html`. There is no build step, no package manager, and no framework dependencies.

## Running the Page

Open `index.html` directly in a browser. No server is required.

For live-reload during development, use any static file server, for example:

```
npx serve .
# or
python -m http.server 8080
```

## File Structure

`index.html` is organized in strict top-to-bottom order:

1. `<head>` — meta tags, inline `<style>` block
2. `<nav id="navbar">` — sticky navigation with hamburger toggle
3. `<section id="hero">` — full-viewport hero
4. `<section id="why-us">` — 6-card benefits grid
5. `<section id="process">` — 4-step timeline
6. `<section id="testimonials">` — 3-column testimonial grid
7. `<section id="lead-magnet">` — checklist offer with mockup visual
8. `<section id="enquiry">` — FormSubmit enquiry form
9. `<section id="faq">` — accordion FAQ
10. `<section id="final-cta">` — conversion banner
11. `<footer id="footer">` — contact, social links, disclaimer
12. Inline `<script>` block at end of `<body>`

## CSS Architecture

All styles are in a single `<style>` block. Key conventions:

- **CSS variables** defined in `:root` control the entire colour palette — edit only these to retheme the page: `--primary`, `--secondary`, `--accent`, `--background`, `--text`, `--light-bg`.
- **Responsive breakpoints**: `max-width: 1024px` (tablet), `max-width: 768px` (mobile), `max-width: 480px` (small mobile). All breakpoints are at the bottom of the style block.
- **Scroll animations** use the class pair `.animate-on-scroll` (initial hidden state) and `.visible` (revealed state) — JavaScript's `IntersectionObserver` adds `.visible` when elements enter the viewport.
- **Button variants**: `.btn` (base) + `.btn-primary`, `.btn-outline`, `.btn-accent`, `.btn-lg`.

## JavaScript Architecture

All JS is in a single `<script>` tag at the bottom of `<body>`, organized into clearly commented sections:

- **Sticky nav** — adds `.scrolled` to `#navbar` after 50 px of scroll, triggering background and shadow via CSS.
- **Mobile menu** — toggles `.open` on `#navLinks` and `#hamburger`; locks `document.body.overflow` when open.
- **Smooth scroll** — intercepts all `a[href^="#"]` clicks and uses `window.scrollTo` with an 80 px offset for the fixed nav.
- **Scroll animations** — `IntersectionObserver` on `.animate-on-scroll` elements with a staggered `setTimeout` delay per batch.
- **Active nav link** — second `IntersectionObserver` on each `<section id>` highlights the matching nav anchor.
- **FAQ accordion** — click handler on `.faq-question`; animates `max-height` via CSS transition; enforces single-open-item.
- **Form validation & submission** — `submit` handler on `#enquiryForm`: validates name, email (regex), and phone (regex) with inline field errors; on success submits via `fetch` to FormSubmit; falls back to native `form.submit()` on network error.

## Form Integration

The enquiry form posts to [FormSubmit](https://formsubmit.co). Before deploying, replace the placeholder in the `action` attribute:

```html
<form action="https://formsubmit.co/YOUR-EMAIL@example.com" method="POST">
```

The three hidden control fields (`_subject`, `_captcha`, `_template`) are already configured. FormSubmit requires an email confirmation click on first submission from a new domain.

## Hero Background Image

The hero uses a direct Unsplash URL (no API key):

```
https://images.unsplash.com/photo-1611974789855-9c2a0a7236a3?auto=format&fit=crop&w=1920&q=80
```

To change it, update the `background` property on `#hero` in the CSS.
