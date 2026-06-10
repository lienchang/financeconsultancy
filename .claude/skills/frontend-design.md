# Frontend Design Skill — Finance Investment Landing Page

Apply this design system whenever updating the visual style of `index.html`.

## Brand Identity

Professional, authoritative, trustworthy. Target audience: high-net-worth individuals and institutional investors. Every design decision should communicate stability and expertise.

## Colour Palette (CSS variables in `:root`)

```css
--primary:    #0a1628;   /* deep navy — main brand, nav bg, footers */
--secondary:  #1a3a6b;   /* mid navy — section accents, card borders */
--accent:     #c9a84c;   /* warm gold — CTAs, highlights, icons */
--background: #f8f7f4;   /* warm off-white — page bg */
--text:       #1c2b3a;   /* dark navy-grey — body copy */
--light-bg:   #eef1f7;   /* pale blue-grey — alternate section bg */

/* Additional tokens */
--accent-hover:  #b8903e;   /* gold darker on hover */
--surface:       #ffffff;   /* card / form surfaces */
--border:        #d4dbe8;   /* subtle borders */
--muted:         #6b7a8d;   /* secondary text, captions */
--success:       #2e7d5e;   /* form success states */
```

## Typography

Load via Google Fonts (add to `<head>` if not present):

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600;700&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
```

Usage rules:
- **Headings** (`h1`–`h3`, section titles, hero): `font-family: 'Playfair Display', Georgia, serif;`
- **Body / UI** (nav, paragraphs, buttons, labels): `font-family: 'Inter', system-ui, sans-serif;`
- Hero H1: `font-size: clamp(2.4rem, 5vw, 4rem); font-weight: 700; letter-spacing: -0.02em;`
- Section headings: `font-size: clamp(1.8rem, 3vw, 2.6rem); font-weight: 600;`
- Body: `font-size: 1rem; line-height: 1.7; font-weight: 400;`
- Captions / labels: `font-size: 0.85rem; letter-spacing: 0.06em; text-transform: uppercase;`

## Component Patterns

### Navigation
- Background: `--primary` with `box-shadow: 0 2px 20px rgba(0,0,0,0.15)` when scrolled
- Logo / brand text: gold (`--accent`), Playfair Display
- Nav links: white at 0.85 opacity, gold on hover/active
- CTA button in nav: gold fill, navy text

### Hero
- Full-viewport with darkened overlay: `rgba(10, 22, 40, 0.65)` over background image
- Headline: white, Playfair Display
- Subheadline: white at 0.85 opacity, Inter Light
- Primary CTA: gold background `--accent`, navy text, `border-radius: 4px`
- Secondary CTA: white outline, white text

### Cards (Benefits, Testimonials)
- Background: `--surface` white
- Border: `1px solid var(--border)`
- Border-top accent: `3px solid var(--accent)` on hover
- `border-radius: 8px; box-shadow: 0 4px 24px rgba(10,22,40,0.08);`
- Icon colour: `--accent` gold

### Buttons
```css
.btn-primary  { background: var(--accent); color: var(--primary); }
.btn-outline  { border: 2px solid var(--accent); color: var(--accent); }
.btn-accent   { background: var(--primary); color: white; }
/* All buttons: padding 0.8rem 2rem; border-radius: 4px; font-weight: 600; letter-spacing: 0.03em; */
```

### Dividers / Section breaks
- Use a thin `2px` gold rule `var(--accent)` centered, `width: 60px`, beneath section headings
- Section label above heading: small caps, gold, Inter, letter-spaced

### Process Timeline
- Step numbers: gold circle `var(--accent)`, navy numeral
- Connector line: `var(--border)` dashed

### FAQ Accordion
- Question bar: `--light-bg` background, navy text, gold arrow icon
- Active question: `--primary` navy background, white text

### Footer
- Background: `--primary` deep navy
- Text: white at 0.7 opacity
- Links: gold on hover
- Divider: `rgba(255,255,255,0.1)`

## Spacing & Layout

- Section padding: `padding: 100px 0` desktop, `60px 0` mobile
- Max content width: `1160px`, centred
- Card gap: `2rem`
- Use `gap` on flex/grid rather than margin hacks

## Micro-interactions

- Button hover: `transform: translateY(-2px); box-shadow: 0 6px 20px rgba(201,168,76,0.35);`
- Card hover: `transform: translateY(-4px); box-shadow: 0 12px 40px rgba(10,22,40,0.12);`
- All transitions: `transition: all 0.25s ease;`
- Nav link underline: slide-in from left on hover using `::after` pseudo-element

## Applying This Skill

When asked to restyle, update, or improve the design:
1. Update the CSS variables in `:root` to match the palette above.
2. Add the Google Fonts `<link>` tags to `<head>` if not already present.
3. Update `font-family` on `body`, headings, and nav items.
4. Apply component patterns section by section.
5. Verify responsive breakpoints still look polished at 768 px and 480 px.
6. Run the page in a browser and take a screenshot to confirm before committing.
