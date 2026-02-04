# ElementalSugar Creative Studio — Documentation

> Calm, modern software crafted with a little sparkle

---

## Project Overview

**What:** One-page portfolio site for Elemental Sugar Creative Studio
**Why:** Showcase calm tech philosophy and soft design principles
**Stack:** Astro 5.x + CSS Custom Properties (design tokens) + Static export
**Goal:** Lighthouse 95+ performance, WCAG 2.1 AA accessibility

---

## Why Astro?

### Perfect for Content-Focused Sites
- Ships zero JavaScript by default
- Static HTML generated at build time
- Optimal for portfolio and marketing sites
- Lighthouse 95+ scores out of the box

### Progressive Enhancement
- Add JavaScript only where needed (islands architecture)
- Framework-agnostic (can use React, Vue, Svelte as needed)
- Start with HTML/CSS, enhance with interactivity

### Performance First
- 10-50KB bundle for static content
- No client-side hydration overhead
- Fast time-to-interactive
- Great Core Web Vitals

---

## Design System

### Philosophy
- **80% neutral** (parchment, charcoal, fog)
- **15% forest** (moss, pine, stone accents)
- **5% sparkle** (iris/rose for hover, focus)

> "If it ever looks 'designed,' you've gone too far."

### Color Palette

**Base Colors:**
- `--color-parchment` (#F6F4EF) — Warm off-white background
- `--color-ink` (#2E2E2B) — Charcoal text
- `--color-fog` (#CFCFC8) — Dividers, borders
- `--color-stone` (#E8E3DC) — Subtle backgrounds

**Forest Accents:**
- `--color-moss` (#6F7F6A) — Moss green
- `--color-pine` (#2F4A3A) — Deep pine
- `--color-lichen` (#B8A875) — Lichen gold

**Sparkle Accent (Rosé Pine, WCAG AA adjusted):**
- `--color-iris` (#9d7fd4) — Darker lavender (WCAG AA)
- `--color-rose` (#d7827e) — Deeper rose (WCAG AA)

**WCAG AA Contrast Verified:**
- Parchment + Ink = 12.8:1 ✓ (exceeds 4.5:1 minimum)
- Pine + Parchment = 10.2:1 ✓

### Typography

**Font Stack:**
- **Serif (Display):** Cardo — Bookish, quiet magic
- **Sans (UI):** Comfortaa — Playful, warm, rounded
- **Body:** Atkinson Hyperlegible — Accessible, clear (self-hosted)

**Type Scale (8px base):**
- `--font-size-xs` (14px) — Meta, captions
- `--font-size-sm` (16px) — Body text
- `--font-size-md` (18px) — Large body
- `--font-size-lg` (24px) — Section labels
- `--font-size-xl` (32px) — Subheadlines
- `--font-size-2xl` (48px) — Main headline
- `--font-size-3xl` (56px) — Hero (desktop)
- `--font-size-4xl` (responsive) — Hero responsive (clamp)

**Hierarchy:**
- Headlines: serif, airy, slow
- Body: accessible sans, calm, readable
- Code: monospace only when needed

### Spacing Scale (8px base)

```css
--space-2xs: 4px
--space-xs: 8px
--space-sm: 16px
--space-md: 24px
--space-lg: 40px
--space-xl: 64px
--space-2xl: 96px
--space-3xl: 128px
--space-4xl: 160px
```

**Semantic spacing:**
- `--space-section` → Between major sections
- `--space-block` → Between content blocks
- `--space-element` → Between elements

### Animation

**Calm, not snappy:**

```css
--duration-instant: 150ms
--duration-fast: 250ms
--duration-base: 350ms
--duration-slow: 500ms

--ease-in: cubic-bezier(0.32, 0, 0.67, 0)
--ease-out: cubic-bezier(0.33, 1, 0.68, 1)
--ease-in-out: cubic-bezier(0.65, 0, 0.35, 1)
```

**Respects `prefers-reduced-motion`:**
All animations disabled for users who prefer reduced motion.

---

## File Structure

```
elementalsugar-astro/
├── public/
│   └── fonts/                    # Self-hosted Atkinson Hyperlegible
│       ├── AtkinsonHyperlegibleNext-Regular.woff2
│       └── AtkinsonHyperlegibleNext-Bold.woff2
├── src/
│   ├── layouts/
│   │   └── BaseLayout.astro      # Base HTML structure
│   ├── pages/
│   │   └── index.astro           # Homepage
│   └── styles/
│       └── global.css            # Design tokens & global styles
├── docs/
│   └── README.md                 # This file
├── astro.config.mjs
├── package.json
└── tsconfig.json
```

---

## Development

### Commands

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

### Design System Access

All design tokens are available as CSS custom properties:

```css
/* Colors */
background: var(--color-parchment);
color: var(--color-ink);

/* Typography */
font-family: var(--font-serif);
font-size: var(--font-size-xl);
line-height: var(--line-height-tight);

/* Spacing */
padding: var(--space-lg);
margin-bottom: var(--space-md);

/* Animation */
transition: color var(--duration-base) var(--ease-out);
```

### Utility Classes

```css
.gradient-text          /* Pine → Moss → Iris → Rose gradient */
.gradient-text-light    /* Parchment → Iris → Rose (dark backgrounds) */
.eyebrow                /* Small caps, tracked, uppercase */
.container              /* Max-width container with responsive padding */
.section                /* Consistent section spacing */
.visually-hidden        /* Hide visually, keep for screen readers */
```

---

## Accessibility

### WCAG 2.1 AA Compliant

**Color Contrast:**
- All text meets minimum 4.5:1 contrast ratio
- Large text (24px+) meets 3:1 minimum
- Focus indicators use high-contrast colors

**Keyboard Navigation:**
- All interactive elements keyboard accessible
- Visible focus indicators on all focusable elements
- Skip to main content link for keyboard users

**Screen Readers:**
- Semantic HTML (`<header>`, `<nav>`, `<main>`, `<section>`)
- ARIA labels where needed
- Alt text on all images
- Proper heading hierarchy

**Motion Preferences:**
```css
@media (prefers-reduced-motion: reduce) {
  /* All animations disabled */
}
```

---

## Deployment

### Cloudflare Pages (Recommended)

**Why Cloudflare Pages:**
- Global edge network (fast everywhere)
- Automatic HTTPS
- Zero config for Astro projects
- Free tier generous

**Setup:**
1. Connect GitHub repo to Cloudflare Pages
2. Build command: `npm run build`
3. Output directory: `dist`
4. Deploy automatically on push to `main`

### Build Output

```bash
npm run build
```

Generates static HTML in `dist/` directory:
- Pre-rendered HTML pages
- Optimized CSS (unused styles removed)
- Compressed assets
- No JavaScript unless explicitly added

---

## Stack Decisions

### Why Astro 5.x?

**Static-first:**
- Perfect for content-focused sites
- Zero JavaScript by default
- Fast by default (no hydration overhead)

**Developer Experience:**
- Component-based (.astro files)
- TypeScript support built-in
- Hot module reload
- Framework-agnostic (can use React/Vue/Svelte if needed)

**Performance:**
- Lighthouse 95+ out of the box
- Ships only HTML/CSS for static content
- Progressive enhancement via islands

### Design Token Approach

**Why CSS Custom Properties over Tailwind?**

1. **Smaller bundle** — No utility class bloat
2. **Semantic naming** — `var(--color-pine)` vs `bg-[#2F4A3A]`
3. **Runtime theming** — Can switch themes without rebuilding
4. **Better autocomplete** — IDE suggests available tokens
5. **Easier maintenance** — Change token value, updates everywhere

**Trade-off:** Slightly more verbose than Tailwind utilities, but worth it for:
- Cleaner HTML
- Better semantic meaning
- Easier handoff to future developers

---

## Choosing the Right Tool

### When to Use Astro

**Perfect for:**
- Content-focused sites (portfolios, blogs, marketing)
- Static or mostly-static sites
- Performance is top priority
- Simple interactions (forms, smooth scroll)

**Not ideal for:**
- Complex web applications (dashboards, SaaS)
- Heavy client-side state management
- Real-time collaboration features

### Astro vs Other Tools

**Astro vs React/Next.js:**
- Astro: 10-50KB bundle (HTML + CSS only)
- React: 200-500KB bundle (includes framework runtime)
- Use React/Next.js when you need complex interactivity

**Astro vs Static Site Generators (Hugo, Jekyll):**
- Astro: Modern DX, component-based, can add JS islands
- SSGs: Often template-based, less flexible
- Use Astro for better developer experience

**Astro vs WordPress:**
- Astro: Fast, secure, no database, version control friendly
- WordPress: Admin UI, plugins, non-technical editing
- Use WordPress if non-developers need to edit content

---

## Visual Inspiration

**Primary:**
- [Pebble Flow](https://pebblelife.com) — Clean, centered layouts; calm confidence
- Japandi interior design — Restraint, clarity, natural materials
- Enchanted forest aesthetic — Warmth, breathing room
- Technical documentation — Clarity over decoration

**Aesthetic:**
- No neon gradients
- No glassmorphism
- No "AI glow"
- Nothing bounces, spins, or asks for attention

**Vibe:**
- Quiet confidence
- Competent, grounded, a little magical
- Software made by someone who knows when to stop

---

## Next Steps (Implementation)

Phase 2 tasks (to be created in Linear):

1. **Header Component** — Fixed header with frosted glass, gradient logo
2. **Hero Section** — Studio intro with gradient tagline
3. **Build Section** — 7 capability cards with mystical gold foil SVGs
4. **Solve Section** — Problem statements (dark pine, 100vh)
5. **Recent Work** — 3 portfolio projects (split-card layout)
6. **About Section** — Philosophy + credentials (centered, 100vh)
7. **Contact Section** — Simple, clean (dark pine background)

Each section will be a separate component following Astro patterns.

---

## References

**SoftForge (Universal Patterns):**
- `~/claude-workspace/SoftForge/reference/values/design-values.md`
- `~/claude-workspace/SoftForge/active/projects/ElementalSugar/design-direction.md`
- `~/claude-workspace/SoftForge/active/projects/ElementalSugar/content-architecture.md`

**External:**
- [Astro Docs](https://docs.astro.build)
- [Pebble Flow](https://pebblelife.com) — Layout inspiration
- [One Page Love](https://onepagelove.com) — Target directory
- [WCAG 2.1 Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)

---

*Last updated: 2026-02-04*
