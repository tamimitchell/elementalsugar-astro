# Elemental Sugar Creative Studio

> Calm, modern software crafted with a little sparkle

One-page portfolio site built with Astro 5.x, showcasing energy-aware design and soft tech principles.

---

## Quick Start

```bash
# Install dependencies
npm install

# Run dev server (http://localhost:4321)
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

---

## Why Astro?

**Next.js was too heavy for a 1-page static site.**

- **Astro:** 10-50KB bundle, zero JavaScript by default
- **Next.js:** 200-500KB bundle with React hydration overhead

For content-focused sites, Astro is the better choice.

---

## Design System

Complete design token system with:
- **Colors:** Enchanted forest + japandi aesthetic
- **Typography:** Cardo (serif) + Comfortaa (sans) + Atkinson Hyperlegible (body)
- **Spacing:** 8px base grid
- **Animation:** Calm, respects `prefers-reduced-motion`
- **Accessibility:** WCAG 2.1 AA compliant

All tokens available as CSS custom properties in `src/styles/global.css`

---

## Stack

- **Astro 5.17.1** — Static site generator
- **TypeScript** — Type safety
- **CSS Custom Properties** — Design tokens
- **Cloudflare Pages** — Global edge deployment (planned)

---

## Project Structure

```
elementalsugar-astro/
├── public/
│   └── fonts/              # Self-hosted Atkinson Hyperlegible
├── src/
│   ├── layouts/
│   │   └── BaseLayout.astro
│   ├── pages/
│   │   └── index.astro
│   └── styles/
│       └── global.css      # Design tokens
└── docs/
    └── README.md           # Full documentation
```

---

## Documentation

**Full documentation:** [`docs/README.md`](./docs/README.md)

Includes:
- Complete design system reference
- Accessibility guidelines
- Stack decision rationale
- Deployment instructions
- Migration notes from Next.js

---

## Development

### Commands

| Command | Action |
|---------|--------|
| `npm install` | Install dependencies |
| `npm run dev` | Start dev server at `localhost:4321` |
| `npm run build` | Build production site to `./dist/` |
| `npm run preview` | Preview production build |

### Design Tokens

```css
/* Access all design tokens via CSS custom properties */
background: var(--color-parchment);
color: var(--color-ink);
font-family: var(--font-serif);
padding: var(--space-lg);
```

See `src/styles/global.css` for complete token reference.

---

## Deployment

**Target:** Cloudflare Pages (global edge network, automatic HTTPS)

**Build settings:**
- Build command: `npm run build`
- Output directory: `dist`
- Node version: 20.x

---

## Links

- **GitHub:** [tamimitchell/elementalsugar-astro](https://github.com/tamimitchell/elementalsugar-astro)
- **Linear Project:** TAM-67 (ElementalSugar Portfolio Site)
- **One Page Love:** [onepagelove.com](https://onepagelove.com) (target directory)
- **Design Reference:** See `docs/README.md`

---

## License

Private project — All rights reserved

---

*Built with Astro 5.x • Last updated: 2026-02-04*
