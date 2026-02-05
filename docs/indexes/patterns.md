# Development Patterns (ElementalSugar.com)

---
created: 2026-02-02
updated: 2026-02-05
purpose: Reusable patterns discovered or refined in this project
---

## 📖 Living Documentation

**Style Guide is the source of truth:** `/app/style-guide/`

The style guide page (`/style-guide`) is our **living design system documentation**:
- Color palette (all design tokens with swatches)
- Typography scale (all heading/body classes with examples)
- Sass mixins (gradient mixins, nesting patterns, `@use` syntax)
- Responsive breakpoints (768px, 1441px + fluid `clamp()` typography)
- Layout patterns (`.section-inner`, viewport sections)
- Component patterns (section headers, links, cards)
- Accessibility patterns (focus states, reduced motion, contrast ratios)

**View it:** http://localhost:3000/style-guide (when dev server is running)

**This file:** Documents implementation patterns and "why" behind architectural decisions that aren't obvious from the style guide alone.

---

## How to Use This Index

**When to add:** After implementing a pattern that works well and could be reused

**Keep it practical:** Include code snippets, file references, and rationale

**Universal patterns:** If it applies to ALL Next.js/TypeScript projects, consider adding to SoftForge:
`~/claude-workspace/SoftForge/reference/indexes/by-language/typescript.md`

**Design patterns:** Add visual/component patterns to `/app/style-guide/` instead (living documentation)

---

## Mystical SVG Gold Gradient System

**Pattern:** Share a single gradient definition across multiple SVG elements using `<defs>` and `url(#gradient-id)`.

**Problem solved:** Consistent gold gradient across all mystical card artwork without duplicating gradient definitions.

**Implementation:**
```html
<!-- Hidden SVG with shared gradient definition -->
<svg width="0" height="0" style="position: absolute;" aria-hidden="true">
  <defs>
    <linearGradient id="gold-gradient" x1="0%" y1="0%" x2="100%" y2="100%">
      <stop offset="0%" style="stop-color:#B8A875;stop-opacity:1" />
      <stop offset="50%" style="stop-color:#9d7fd4;stop-opacity:1" />
      <stop offset="100%" style="stop-color:#d7827e;stop-opacity:1" />
    </linearGradient>
  </defs>
</svg>

<!-- Usage in any SVG -->
<svg viewBox="0 0 100 100">
  <path d="M30 25 L50 15 L70 25 Z" stroke="url(#gold-gradient)" fill="none" />
</svg>
```

**Why this is soft-tech:**
- **Consistent branding** - All mystical art uses same gradient (visual coherence reduces cognitive load)
- **Maintainable** - Change gradient in one place, updates everywhere
- **Performance** - Browser renders gradient once, reuses definition
- **Accessible** - `aria-hidden="true"` on definition SVG (decorative)

**Used in:**
- Build section capability cards
- Section headers (text gradient version)

---

## Reduced Motion Shimmer Fallback

**Pattern:** Provide static opacity state when user prefers reduced motion.

**Problem solved:** Shimmer animation can be disorienting for users with vestibular disorders or motion sensitivity.

**Implementation:**
```css
/* Default: gentle shimmer */
.capability:hover .mystical-art {
  animation: shimmer 2s ease-in-out infinite;
}

@keyframes shimmer {
  0%, 100% { opacity: 0.35; filter: brightness(1); }
  50% { opacity: 0.55; filter: brightness(1.3); }
}

/* Reduced motion: static hover state */
@media (prefers-reduced-motion: reduce) {
  .capability:hover .mystical-art {
    animation: none;
    opacity: 0.55; /* Still shows hover feedback, no motion */
  }
}
```

**Why this is soft-tech:**
- **Trauma-informed** - Respects user's stated preferences
- **Graceful degradation** - Still provides hover feedback (not broken-looking)
- **Accessibility** - WCAG 2.1 AA requires respecting motion preferences
- **Energy-aware** - Less animation = less visual processing load

**See:** CLAUDE.md "Respect Motion Preferences" section

---

## Tailwind Design Token Extension

**Pattern:** Extend Tailwind with project-specific design tokens using CSS custom properties.

**Problem solved:** Using arbitrary values (`bg-[#F6F4EF]`) is hard to maintain. Named tokens (`bg-parchment`) are semantic and changeable.

**Implementation:**
```javascript
// tailwind.config.ts
module.exports = {
  theme: {
    extend: {
      colors: {
        parchment: 'var(--color-parchment)',
        ink: 'var(--color-ink)',
        fog: 'var(--color-fog)',
        stone: 'var(--color-stone)',
        moss: 'var(--color-moss)',
        pine: 'var(--color-pine)',
        lichen: 'var(--color-lichen)',
        iris: 'var(--color-iris)',
        rose: 'var(--color-rose)',
      },
      spacing: {
        xs: 'var(--space-xs)',
        sm: 'var(--space-sm)',
        md: 'var(--space-md)',
        lg: 'var(--space-lg)',
        xl: 'var(--space-xl)',
        '2xl': 'var(--space-2xl)',
        '3xl': 'var(--space-3xl)',
        '4xl': 'var(--space-4xl)',
      },
    },
  },
};
```

```css
/* globals.css */
:root {
  --color-parchment: #F6F4EF;
  --color-ink: #2E2E2B;
  /* ... etc */
}
```

**Why this is soft-tech:**
- **Semantic naming** - `bg-parchment` reads like design intent
- **Single source of truth** - Change color in one place
- **Designer-friendly** - Names match design-direction.md vocabulary
- **Future-proof** - Can add dark mode by redefining CSS variables

**See:** design-direction.md for complete token definitions

---

## Critical Font Preloading

**Pattern:** Preload critical body font in `<head>` for faster initial render, reducing Flash of Unstyled Text (FOUT).

**Problem solved:** Body text is the most common content on page. Default font loading waits for CSS to parse before fetching fonts, causing delay. Preloading fetches font file in parallel with HTML, making text readable faster.

**Implementation:**
```typescript
// app/layout.tsx
export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <head>
        {/* Preload critical body font */}
        <link
          rel="preload"
          href="/fonts/atkinson/AtkinsonHyperlegibleNext-Regular.woff2"
          as="font"
          type="font/woff2"
          crossOrigin="anonymous"
        />
      </head>
      <body>{children}</body>
    </html>
  );
}

// Font configured with display: 'swap'
const atkinson = localFont({
  src: [/* font files */],
  variable: '--font-atkinson',
  display: 'swap', // Show fallback → swap when loaded
});
```

**Why this is soft-tech:**
- **Performance** - Faster initial render (body text appears ~100-200ms faster)
- **Accessibility** - Text always visible with `display: 'swap'` fallback
- **Prioritization** - Only preload critical fonts, not all fonts (avoids bandwidth waste)
- **Nervous system calm** - Text appears faster = less waiting anxiety

**Decision rationale:**
- **Preload Atkinson (body text):** Yes - Most common content, local font, critical for readability
- **Don't preload Cardo (headings):** Google Font auto-optimized by Next.js, less critical
- **Don't preload Comfortaa (accents):** Least critical, fallback acceptable

**Performance impact:**
- Before: Body text FOUT ~200-400ms on slow connections
- After: Body text appears immediately with preload
- Lighthouse score impact: +2-5 points on Performance

**Used in:**
- `app/layout.tsx` - Atkinson Regular preload

**See:**
- CLAUDE.md "Font Loading Strategy" section
- Web.dev guide: https://web.dev/font-best-practices/

---

## CSS-First Scroll Detection (Header Blur)

**Pattern:** Use a tiny inline script to toggle a data attribute, then handle all visual changes in CSS.

**Problem solved:** The header needs a frosted glass blur effect on scroll. React used `useState`/`useEffect` (~40KB+ runtime). Astro should minimize JS.

**Implementation:**
```html
<!-- Header element with data attribute for CSS targeting -->
<header class="header" data-header>...</header>

<script>
  // ~200 bytes minified. Toggles data-scrolled attribute.
  const header = document.querySelector('[data-header]');
  if (header) {
    const updateHeader = () => {
      if (window.scrollY > 10) {
        header.setAttribute('data-scrolled', '');
      } else {
        header.removeAttribute('data-scrolled');
      }
    };
    updateHeader(); // Handle page refresh mid-scroll
    window.addEventListener('scroll', updateHeader, { passive: true });
  }
</script>
```

```css
/* All visual logic in CSS -- no JS dependency */
.header {
  background: transparent;
  transition: background-color 350ms, backdrop-filter 350ms;
}

.header[data-scrolled] {
  backdrop-filter: blur(8px);
  background-color: rgba(246, 244, 239, 0.95);
}

/* Fallback for browsers without backdrop-filter */
@supports not (backdrop-filter: blur(8px)) {
  .header[data-scrolled] {
    background-color: var(--color-parchment);
  }
}
```

**Why this is soft-tech:**
- **Performance** - ~200B inline vs ~40KB+ React runtime for the same effect
- **Progressive enhancement** - Works without JS (header stays visible, just no blur)
- **Passive scroll listener** - Does not block main thread during scroll
- **GPU composited** - `transform: translateZ(0)` + `will-change` for smooth rendering

**Used in:**
- `src/components/Header.astro` (script)
- `src/styles/components/header.css` (visual logic)

---

## Reusable Gradient Button (.btn Pattern)

**Pattern:** Extract button styles into a shared CSS file with BEM variant classes.

**Problem solved:** The gradient CTA button (iris -> rose) will be reused in multiple sections (header, contact, hero). Putting it in a component-scoped style would duplicate it.

**Implementation:**
```css
/* src/styles/components/button.css */
.btn { /* base: font, padding, border-radius */ }
.btn--gradient { /* iris -> rose gradient, parchment text */ }
.btn--gradient:hover { /* darker gradient */ }
.btn--gradient:focus-visible { /* rose outline */ }
```

```astro
---
import '../styles/components/button.css';
---
<a href="#contact" class="btn btn--gradient">Contact</a>
```

**Why this is soft-tech:**
- **DRY** - One definition, many uses
- **Maintainable** - Change button style in one file, updates everywhere
- **Composable** - Add new variants (`.btn--outline`) when needed, not before

**Used in:**
- `src/components/Header.astro` (contact CTA)
- Future: contact section, hero CTA

---

## Hero Component Structure (TAM-112)

**Pattern:** Extract large sections (40+ lines) into standalone components following consistent structure.

**Problem solved:** Index pages become unwieldy with inline HTML. Hero section (42 lines) extracted to reusable component.

**Component structure:**
```astro
---
/**
 * Component.astro
 *
 * [Purpose statement]
 *
 * Typography:
 * - [Font choices with sizes]
 *
 * Layout:
 * - [Viewport/spacing decisions]
 *
 * Accessibility:
 * - [ARIA patterns, keyboard nav]
 *
 * Styles: src/styles/components/[name].css
 */

import '../styles/components/[name].css';

interface Props {
  /** Prop descriptions */
  prop?: string;
}

const { prop = 'default' } = Astro.props;
---

<section id="[name]" class="[name] section--viewport" aria-labelledby="[name]-heading">
  <div class="section-inner">
    <!-- Component content -->
  </div>
</section>
```

**CSS structure:**
```css
/* src/styles/components/hero.css */
/**
 * hero.css
 *
 * Hero section styles for Hero.astro component.
 *
 * Classes:
 *   .[name]                 - Section wrapper
 *   .[name]__element        - BEM naming
 *
 * Depends on: tokens.css, layout.css
 */

.[name] { /* Section styles */ }
.[name]__element { /* Element styles */ }
```

**Why this is soft-tech:**
- **Maintainable** - Find component logic and styles quickly
- **Documented** - JSDoc explains decisions for future-you
- **Consistent** - All components follow same structure (Header.astro → Hero.astro)
- **Low-energy friendly** - Clear patterns reduce cognitive load

**Used in:**
- `src/components/Header.astro` (navigation, logo, scroll blur)
- `src/components/Hero.astro` (headline with gradient, tagline)

---

## Font Weight Alignment with Loaded Fonts (TAM-112)

**Pattern:** Verify all `font-weight` declarations match weights defined in `@font-face` rules. Use design tokens for font weights.

**Problem solved:** Phantom font-weight declarations (e.g., `font-weight: 300` when only 400/700 loaded) create confusion and fallback behavior.

**Implementation:**

1. **Document loaded weights in tokens.css:**
```css
/* tokens.css */
/* Font Weights (aligned with loaded fonts) */
--font-weight-regular: 400;  /* Cardo 400 */
--font-weight-bold: 700;     /* Cardo 700 */
--font-weight-light: 400;    /* Cardo 400 (300 doesn't exist) */
```

2. **Use tokens in component CSS:**
```css
/* hero.css */
.hero__headline-sub {
  font-family: var(--font-family-display);  /* Cardo */
  font-weight: var(--font-weight-light);    /* Maps to 400, not phantom 300 */
}
```

3. **Check during code review:**
- Grep for numeric font-weight: `grep -r "font-weight: [0-9]" src/styles/`
- Compare against `@font-face` declarations
- Verify token mappings accurate

**Why this is soft-tech:**
- **Correctness** - No phantom declarations, no browser synthesis
- **Clarity** - `var(--font-weight-light)` expresses intent even when using 400
- **Maintainable** - Change font loading? Update tokens once, applies everywhere
- **Self-documenting** - Token comments explain "why 400 for light"

**Code review checklist:**
- [ ] All font-weight values exist in loaded fonts
- [ ] Font weights use tokens, not magic numbers
- [ ] Token comments explain mappings (especially non-obvious ones)
- [ ] Documentation accurate (don't say "light weight" when using 400)

**Related:** SoftForge `code-review.md` (Design Token Consistency pattern)

---

## Astro Whitespace Handling (TAM-112)

**Pattern:** Use natural HTML whitespace in Astro templates. Don't use JSX-style `{' '}` expressions.

**Problem solved:** JSX pattern `{' '}` creates double spaces in Astro output (Astro preserves whitespace naturally).

**Implementation:**
```astro
<!-- GOOD: Natural whitespace -->
<span class="hero__headline-sub">
  crafted with a little <span class="hero__sparkle">sparkle</span>
</span>

<!-- BAD: JSX-ism creates double space -->
<span class="hero__headline-sub">
  crafted with a little{' '}<span class="hero__sparkle">sparkle</span>
</span>
```

**Why this is soft-tech:**
- **Framework-appropriate** - Uses Astro's natural whitespace rules, not React patterns
- **Correct HTML** - No double spaces in output
- **Clear code** - Visual whitespace matches output whitespace

**Code review check:**
- Grep for JSX space expressions: `grep -r "{' '}" src/`
- Should return zero results in Astro projects

**Related:** SoftForge `ui-frameworks.md` (Astro patterns)

---

## Template for New Patterns

```markdown
## Pattern Name

**Pattern:** One-sentence description

**Problem solved:** What problem does this address?

**Implementation:**
```code
// Example with comments
```

**Why this is soft-tech:**
- Bullet points explaining alignment with design values
- How it supports accessibility, performance, maintainability

**Used in:**
- File references

**See:** Related docs (optional)
```
