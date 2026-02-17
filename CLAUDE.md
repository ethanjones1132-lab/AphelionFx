# CLAUDE.md — AphelionFx

## Project Overview

AphelionFx is a static marketing website for a boutique audio plugin studio that builds professional-grade VST3 effects for music producers and engineers. The site is hosted via **GitHub Pages** and contains product information, brand storytelling, and purchase flows.

**Live products:** CORVUS FX (multi-effect VST3 plugin — $15)
**Upcoming products:** Perihelion, Solstice (both listed as "coming soon")

## Repository Structure

```
AphelionFx/
├── .github/
│   └── workflows/
│       ├── deploy-pages.yml    # GitHub Pages deployment (with enablement flag)
│       └── static.yml          # GitHub Pages deployment (original)
├── .nojekyll                   # Disables Jekyll processing on GitHub Pages
├── README.md                   # Minimal project description
├── index.html                  # Main landing page (warm earthy theme)
├── corvus-fx.html              # CORVUS FX product page (dark space theme)
└── CLAUDE.md                   # This file
```

There is **no build step**, no package.json, no bundler, and no external dependencies. The entire site is plain HTML, CSS, and vanilla JavaScript served directly as static files.

## Tech Stack

| Layer        | Technology                                      |
|--------------|--------------------------------------------------|
| Markup       | HTML5 (semantic)                                 |
| Styling      | CSS3 (embedded `<style>` blocks, CSS variables)  |
| Scripting    | Vanilla JavaScript (embedded `<script>` blocks)  |
| Fonts        | Google Fonts CDN (Cormorant Garamond, DM Sans, Outfit, JetBrains Mono) |
| Animation    | CSS keyframes, Canvas API, IntersectionObserver  |
| Hosting      | GitHub Pages                                     |
| CI/CD        | GitHub Actions (auto-deploy on push to `main`)   |

**Zero npm dependencies.** No build tools, transpilers, or bundlers.

## Development Workflow

### Local Development

1. Clone the repository
2. Open `index.html` or `corvus-fx.html` directly in a browser, or use any local HTTP server:
   ```bash
   python3 -m http.server 8000
   ```
3. Edit the HTML files directly — changes are visible on reload

### Deployment

Pushing to the `main` branch triggers automatic deployment via GitHub Actions. Both workflow files (`.github/workflows/static.yml` and `.github/workflows/deploy-pages.yml`) perform the same job:

1. Checkout code
2. Configure GitHub Pages
3. Upload the entire repository root as an artifact
4. Deploy to GitHub Pages

There are two nearly identical workflow files. `deploy-pages.yml` includes `enablement: true` in the Pages setup step; `static.yml` does not. Both target the `main` branch.

### No Build or Test Steps

There is no build process, linting, type checking, or test suite. Changes to HTML files are deployed as-is.

## File Details

### `index.html` (~715 lines)

The main landing page for the AphelionFx brand.

- **Design:** Warm, earthy color palette (gold `#c9a227`, ivory, amber gradients)
- **Fonts:** Cormorant Garamond (serif headings), DM Sans (body text)
- **Sections:** Hero with animated sun SVG, product grid, philosophy principles, about section, newsletter CTA, footer
- **JS features:** Scroll reveal via IntersectionObserver, mobile hamburger menu toggle, newsletter email validation (`subEmail()`)

### `corvus-fx.html` (~400 lines)

Dedicated product page for the CORVUS FX plugin.

- **Design:** Deep space dark theme (purples, dark blues, glowing accents)
- **Fonts:** Outfit (headings), JetBrains Mono (technical specs)
- **Sections:** Hero, features grid, signal chain, 12 curated presets, technical specs, FAQ accordion, purchase modal
- **JS features:** Canvas starfield animation, FAQ accordion (`togFaq()`), purchase modal with email validation (`openModal()`, `closeModal()`, `confirmBuy()`), scroll-based nav background, mobile menu

## Code Conventions

### CSS

- All styles are embedded in `<style>` blocks within each HTML file (no external stylesheets)
- CSS custom properties (`--variable-name`) are used for theming
- Mobile-first responsive design with `@media` breakpoints
- Heavy use of gradients, `backdrop-filter`, and glassmorphism effects
- Keyframe animations for visual elements (sun breathing, corona pulse, starfield)

### JavaScript

- All scripts are embedded in `<script>` blocks at the bottom of each HTML file
- No modules, imports, or external JS libraries
- Functions use short, descriptive names: `toggleMenu()`, `goTo()`, `togFaq()`, `subEmail()`
- IntersectionObserver pattern for scroll-triggered reveal animations
- Canvas `requestAnimationFrame` loop for procedural starfield animation
- Event listeners attached inline (`onclick`) or via `addEventListener`

### HTML

- Semantic HTML5 elements (`<header>`, `<nav>`, `<section>`, `<footer>`)
- Sections use descriptive `id` attributes for anchor navigation
- Accessibility: keyboard-navigable modals (Escape to close), proper heading hierarchy
- Each page is self-contained (all CSS + JS embedded, no shared resources between pages)

## Design System

The site uses two distinct visual themes:

| Aspect         | index.html (Brand)            | corvus-fx.html (Product)        |
|----------------|-------------------------------|---------------------------------|
| Mood           | Warm, organic, earthy         | Dark, cosmic, technical         |
| Background     | Light/warm gradients          | Near-black (`#0a0a12`)          |
| Accent color   | Gold (`#c9a227`)              | Purple/violet glows             |
| Serif font     | Cormorant Garamond            | —                               |
| Sans font      | DM Sans                       | Outfit                          |
| Mono font      | —                             | JetBrains Mono                  |
| Animations     | CSS-only (sun SVG)            | Canvas starfield + CSS          |

## Key Patterns for AI Assistants

1. **No build pipeline** — edit HTML files directly; there is nothing to compile or bundle.
2. **Self-contained pages** — each HTML file includes all its own CSS and JS. There are no shared stylesheets or script files.
3. **No testing infrastructure** — there are no tests to run. Validate changes visually or by reviewing the HTML structure.
4. **Deployment is automatic** — any push to `main` deploys the site. Be careful with commits to `main`.
5. **Two deployment workflows exist** — they are near-duplicates. If modifying CI/CD, consider whether both need updating.
6. **CSS variables are the theming mechanism** — use existing CSS custom properties when adding or modifying styles.
7. **Keep it dependency-free** — the project intentionally uses zero external libraries. Do not introduce npm, webpack, or framework dependencies unless explicitly requested.
8. **Inline everything** — follow the existing pattern of embedding CSS and JS within HTML files rather than creating separate `.css` or `.js` files.
9. **Preserve the two-theme approach** — the brand page and product page have deliberately distinct visual identities.
10. **Google Fonts are the only external resource** — loaded via `<link>` tags in `<head>`.
