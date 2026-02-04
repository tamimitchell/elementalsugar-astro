# CLAUDE.md — ElementalSugar Creative Studio Portfolio Site

---
created: 2026-02-04
updated: 2026-02-04
---

> One-page Astro portfolio site for Elemental Sugar Creative Studio
> Showcasing calm tech philosophy, mystical aesthetic, and 13 years of proven work

---

## 🎯 Project Overview

**What:** Professional portfolio site for Elemental Sugar Creative Studio (run by Tami Mitchell)
**Goal:** Get listed on One Page Love directory as "Astro/static site specialist"
**Stack:** Astro 5.17.1 + TypeScript + CSS Custom Properties + Cloudflare Pages
**Status:** Phase 1 complete (design system), ready for component implementation

**Key Features:**
- Mystical tarot card aesthetic (gold foil SVGs)
- Energy-aware design philosophy demonstrated
- Proven client work (Rebelle Rally, SafetyChain, Campendium)
- Lighthouse 95+ performance, WCAG 2.1 AA accessibility
- Static export for Cloudflare Pages edge delivery

---

## 📋 Essential Context Documents

**Read THESE before coding:**

1. **Design Direction** → `docs/softforge-links/design-direction.md`
   - Complete visual system (colors, typography, spacing)
   - Mystical gold foil SVG aesthetic
   - Pebble Flow-inspired layouts
   - Japandi + enchanted forest vibe

2. **Content Architecture** → `docs/softforge-links/content-architecture.md`
   - All copy finalized (Hero, Build, Solve, Recent Work, About, Contact)
   - Voice parameters (Becky Chambers energy, Soft Systems approach)
   - AISEO-optimized structure

3. **Design Tokens** → `src/styles/global.css`
   - Complete CSS custom properties (400+ lines)
   - All colors, spacing, typography, animation tokens
   - Utility classes (gradient-text, eyebrow, container)
   - Accessibility features (skip links, focus states)

4. **Comprehensive Docs** → `docs/README.md`
   - Complete design system reference (390+ lines)
   - Stack decisions, deployment guide
   - Why Astro? section

5. **SoftForge Universal Patterns** → `docs/softforge-links/`
   - design-values.md — Soft tech design philosophy
   - archetypes.md — Systems Weaver identity
   - code-craftsperson.md — Pair programming workflow
   - code-reviewer.md — Code review patterns

---

## 🛠️ Tech Stack

### Core

- **Astro 5.17.1** — Static site generator
- **TypeScript** — Type safety (strict mode)
- **CSS Custom Properties** — Design tokens (no Tailwind, no Sass)
- **Node.js 20.x** — Runtime environment

### Why Astro?

**Perfect for content-focused, performance-first sites:**
- Zero JavaScript by default (only HTML + CSS)
- 10-50KB bundle vs 200-500KB for React/Next.js
- Lighthouse 95+ scores out of the box
- Static HTML generated at build time
- Add interactivity only where needed (islands architecture)

**Use Astro when:**
- Content-focused sites (portfolios, blogs, marketing)
- Performance is top priority
- Minimal client-side interactivity

**Don't use Astro for:**
- Complex web applications (dashboards, SaaS)
- Heavy client-side state management
- Real-time features

### Hosting & Deployment

- **Cloudflare Pages** (global edge network, automatic HTTPS)
- **Static export** (pre-rendered HTML at build time)
- **GitHub** → Cloudflare auto-deploy pipeline

### Fonts

- **Cardo** (serif, display/headlines) — Self-hosted WOFF2 (weights: 400, 700)
- **Comfortaa** (sans, playful headings/nav) — Self-hosted WOFF2 (weight: 700 only)
- **Atkinson Hyperlegible** (body text, accessibility) — Self-hosted WOFF2 (weights: 400, 700)

---

## 🎨 Design System

Complete design token system available as CSS custom properties in `src/styles/global.css`.

### Colors (Enchanted Forest + Japandi)

**Base Colors:**
```css
--color-parchment: #F6F4EF;  /* Warm off-white background */
--color-ink: #2E2E2B;        /* Charcoal text */
--color-fog: #CFCFC8;        /* Dividers, borders */
--color-stone: #E8E3DC;      /* Subtle backgrounds */
```

**Forest Accents:**
```css
--color-moss: #6F7F6A;       /* Moss green */
--color-pine: #2F4A3A;       /* Deep pine */
--color-lichen: #B8A875;     /* Lichen gold */
```

**Sparkle (Rosé Pine, WCAG AA adjusted):**
```css
--color-iris: #9d7fd4;       /* Darker lavender (WCAG AA) */
--color-rose: #d7827e;       /* Deeper rose (WCAG AA) */
```

**WCAG AA Contrast Verified:**
- Parchment + Ink = 12.8:1 ✓ (exceeds 4.5:1 minimum)
- Pine + Parchment = 10.2:1 ✓

### Typography

**Font Families:**
```css
--font-serif: 'Cardo', 'Georgia', serif;
--font-sans: 'Comfortaa', 'Inter', system-ui, sans-serif;
--font-body: 'Atkinson Hyperlegible', 'Inter', system-ui, sans-serif;
```

**Type Scale (8px base):**
```css
--font-size-xs: 0.875rem;    /* 14px - meta, captions */
--font-size-sm: 1rem;        /* 16px - body text */
--font-size-md: 1.125rem;    /* 18px - large body */
--font-size-lg: 1.5rem;      /* 24px - section labels */
--font-size-xl: 2rem;        /* 32px - subheadlines */
--font-size-2xl: 3rem;       /* 48px - main headline */
--font-size-3xl: 3.5rem;     /* 56px - hero (desktop) */
--font-size-4xl: clamp(4.5rem, 12vw, 10rem); /* Hero responsive */
```

### Spacing Scale (8px base)

```css
--space-2xs: 0.25rem;  /* 4px */
--space-xs: 0.5rem;    /* 8px */
--space-sm: 1rem;      /* 16px */
--space-md: 1.5rem;    /* 24px */
--space-lg: 2.5rem;    /* 40px */
--space-xl: 4rem;      /* 64px */
--space-2xl: 6rem;     /* 96px */
--space-3xl: 8rem;     /* 128px */
--space-4xl: 10rem;    /* 160px */
```

**Semantic Spacing:**
```css
--space-section: var(--space-3xl);  /* Between major sections */
--space-block: var(--space-xl);     /* Between content blocks */
--space-element: var(--space-md);   /* Between elements */
```

### Animation (Calm, Not Snappy)

```css
/* Duration */
--duration-instant: 150ms;
--duration-fast: 250ms;
--duration-base: 350ms;
--duration-slow: 500ms;

/* Easing */
--ease-in: cubic-bezier(0.32, 0, 0.67, 0);
--ease-out: cubic-bezier(0.33, 1, 0.68, 1);
--ease-in-out: cubic-bezier(0.65, 0, 0.35, 1);
```

**Respects `prefers-reduced-motion`:** All animations disabled for users who prefer reduced motion.

---

## 🔄 Standard Workflow (Code Craftsperson)

**CRITICAL:** Always follow this sequence for ALL code changes.

### Step 1: Start Work (Linear Issue → Branch)

```bash
cd ~/claude-workspace/elementalsugar-astro

# Start work with automatic timer + branch (solo dev, no prefix)
tam start <issue-number> "Short description"

# Example:
tam start 109 "Hero section"
# → Starts Harvest timer: "TAM-109: Hero section"
# → Creates branch: tam-109-hero-section (no mail/ prefix)
# → Shows Linear issue link
```

**Branch naming:** `tam-<issue-number>-<short-description>` (no prefix needed, solo dev project)

### Step 2: Do the Work (But Don't Commit Yet!)

- Implement the component/feature
- Run local dev server: `npm run dev`
- Check design matches design-direction.md
- Verify accessibility (VoiceOver, keyboard nav)
- **DON'T commit or close Linear issue yet!**

### Step 3: Check with User BEFORE Committing

Present changes for review:
```
"I've implemented [component]. Here's what I did:
- Created Hero.astro component in src/components/
- Added gradient text effect using .gradient-text utility
- Styled with design tokens from global.css

Changes are staged but not committed. Want me to:
1. Proceed with commit + PR?
2. Adjust anything first?"
```

**Why:** User may want different approach, prevents wasted work.

### Step 4: Commit (After Approval)

```bash
git add [files]
git commit -m "$(cat <<'EOF'
feat: implement hero section (TAM-109)

Added hero section with gradient logo and energy-aware design.

Changes:
- Created Hero.astro component with TypeScript
- Implemented gradient text effect using utility class
- Used design tokens for all spacing and colors
- Responsive layout (mobile/desktop)

Example:
- Tagline: "Calm, modern software crafted with a little sparkle"
- Uses Cardo serif for headlines, Comfortaa for tagline

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>
EOF
)"
```

**Commit types:** `feat:`, `fix:`, `refactor:`, `docs:`, `test:`, `chore:`

### Step 5: Push and Create PR

```bash
# Push branch
git push -u origin tam-109-hero-section

# Create PR
gh pr create --title "feat: Hero section (TAM-109)" --body "$(cat <<'EOF'
## Summary
Implemented hero section with gradient logo and energy-aware design.

## Changes
- Hero.astro component with TypeScript props
- Gradient text effect using .gradient-text utility
- Cardo serif for headlines, Comfortaa for tagline
- Responsive layout with mobile breakpoints

## Testing
- ✅ Tested on Chrome, Safari, Firefox
- ✅ VoiceOver navigation working
- ✅ Keyboard focus visible
- ✅ Gradient renders correctly
- ✅ Respects prefers-reduced-motion

## Accessibility
- WCAG 2.1 AA compliant
- Semantic HTML (section, h1, p)
- Proper heading hierarchy

## Linear Issues
- Closes TAM-109

EOF
)"
```

### Step 6: Update Indexes (ALWAYS)

**CRITICAL:** Extract learnings before closing issue.

```bash
# Project-specific patterns
~/claude-workspace/elementalsugar-astro/docs/indexes/decisions.md
~/claude-workspace/elementalsugar-astro/docs/indexes/patterns.md

# Universal patterns (AFTER merge, if truly universal)
~/claude-workspace/SoftForge/reference/indexes/by-category/accessibility.md
~/claude-workspace/SoftForge/reference/indexes/by-category/ui-ux.md
```

**Document:**
- Component patterns (how you structured it)
- Design decisions (why you chose this approach)
- Accessibility techniques (ARIA labels, semantic HTML)
- Astro-specific patterns (.astro component structure)

### Step 7: Stop Timer & Close Linear Issue (After Merge)

```bash
# Stop timer
tam stop

# After PR merges, update Linear (using Linear MCP)
mcp__linear__update_issue({
  id: "TAM-109",
  state: "Done"
})

# Add comment
mcp__linear__create_comment({
  issueId: "TAM-109",
  body: "✅ Completed in PR #X\n\nTime: [X hours]\n\nPatterns documented in:\n- docs/indexes/patterns.md"
})
```

---

## 🎨 Component Patterns

### TypeScript + Astro

```astro
---
// src/components/Hero.astro

interface Props {
  title: string;
  subtitle?: string;
  showCTA?: boolean;
}

const {
  title,
  subtitle,
  showCTA = true
} = Astro.props;
---

<section class="hero">
  <div class="container">
    <p class="eyebrow">Elemental Sugar Creative Studio</p>

    <h1>
      <span class="title-main">{title}</span>
      {subtitle && <span class="title-sub">{subtitle}</span>}
    </h1>

    {showCTA && <a href="#contact" class="cta">Get Started →</a>}
  </div>
</section>

<style>
  .hero {
    min-height: 100vh;
    display: flex;
    align-items: center;
    padding: var(--space-section);
    background: var(--color-bg-primary);
  }

  .container {
    max-width: var(--container-max);
    margin-inline: auto;
  }

  h1 {
    font-family: var(--font-serif);
    font-size: var(--font-size-4xl);
    line-height: var(--line-height-tight);
  }
</style>
```

### Gradient Text Utility

```astro
<!-- Pine → Moss → Iris → Rose gradient -->
<h2 class="gradient-text">We BUILD</h2>

<!-- Parchment → Iris → Rose (for dark backgrounds) -->
<h2 class="gradient-text-light">We SOLVE</h2>
```

### Mystical SVG Component

```astro
---
// src/components/MysticalArt.astro

interface Props {
  variant: 'crystal' | 'moon' | 'eye';
  className?: string;
}

const { variant, className = '' } = Astro.props;
---

<!-- SVG with gold gradient and shimmer animation -->
<!-- See design-direction.md for full SVG patterns -->
```

---

## ♿ Accessibility Requirements

**WCAG 2.1 AA Compliance Required:**

### Color Contrast
- Parchment + Ink = 12.8:1 ✓ (exceeds 4.5:1)
- Pine + Parchment = 10.2:1 ✓
- All text meets minimum contrast ratios

### Semantic HTML
```astro
<!-- Good -->
<header role="banner">
  <nav role="navigation">
    <a href="#build">Build</a>
  </nav>
</header>

<main role="main" id="main-content">
  <section id="build" aria-labelledby="build-heading">
    <h2 id="build-heading">We BUILD</h2>
  </section>
</main>
```

### Keyboard Navigation
- All interactive elements focusable
- Visible focus indicators (no `outline: none`)
- Tab order logical
- Skip links for main content

### Motion Preferences
```css
/* Respects reduced motion */
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## ⚡ Performance Requirements

**Target: Lighthouse 95+ (mobile + desktop)**

### Core Web Vitals
- **LCP** (Largest Contentful Paint) < 2.5s
- **FID** (First Input Delay) < 100ms
- **CLS** (Cumulative Layout Shift) < 0.1

### Astro Performance Wins
- Static HTML generation (no hydration overhead)
- Zero JavaScript by default
- Optimized CSS (scoped styles)
- Font optimization (preconnect, font-display: swap)

### Build Command
```bash
npm run build
# Generates static HTML in dist/
```

---

## 🧪 Testing Checklist

**Before marking issue as Done:**

### Visual Testing
- [ ] Matches design-direction.md visual system
- [ ] Colors from design tokens (not hardcoded)
- [ ] Typography uses correct font families
- [ ] Spacing uses design token scale
- [ ] Responsive on mobile/tablet/desktop
- [ ] Gradients display properly

### Accessibility Testing
- [ ] VoiceOver navigation works (macOS)
- [ ] Keyboard navigation works (Tab, Enter, Space)
- [ ] Focus indicators visible
- [ ] Color contrast meets WCAG AA (4.5:1 text, 3:1 large text)
- [ ] Semantic HTML (`<header>`, `<nav>`, `<main>`, `<section>`)
- [ ] Alt text on images
- [ ] ARIA labels where needed

### Performance Testing
- [ ] Lighthouse Performance 95+ (mobile + desktop)
- [ ] Lighthouse Accessibility 100/100
- [ ] Core Web Vitals passing
- [ ] Build succeeds: `npm run build`

### Browser Testing
- [ ] Chrome (latest)
- [ ] Safari (latest)
- [ ] Firefox (latest)
- [ ] Mobile Safari (iOS)
- [ ] Mobile Chrome (Android)

---

## 📝 Code Style

### TypeScript
- Functional components only
- Props interfaces in frontmatter
- Explicit types (no `any`)
- Type all parameters and returns

### Astro Components
```astro
---
// Props interface
interface Props {
  title: string;
  optional?: boolean;
}

// Destructure props
const { title, optional = false } = Astro.props;
---

<!-- Template (use props) -->
<section>
  <h1>{title}</h1>
</section>

<style>
  /* Scoped styles */
  section {
    padding: var(--space-lg);
  }
</style>
```

### CSS
- Use design tokens (CSS custom properties)
- Mobile-first responsive design
- No magic numbers (use spacing scale)
- Respect motion preferences

```css
/* Good - uses design tokens */
background: var(--color-parchment);
color: var(--color-ink);
padding: var(--space-lg);

/* Bad - hardcoded values */
background: #F6F4EF;
color: #2E2E2B;
padding: 40px;
```

---

## 🔗 Quick Links

**Project:**
- **GitHub:** https://github.com/tamimitchell/elementalsugar-astro
- **Linear:** TAM-108+ (ElementalSugar project)
- **Docs:** `/docs/README.md` (complete design system reference)

**SoftForge:**
- **Design Direction:** `docs/softforge-links/design-direction.md`
- **Content:** `docs/softforge-links/content-architecture.md`
- **Code Craftsperson:** `docs/softforge-links/code-craftsperson.md`

**External:**
- [Astro Docs](https://docs.astro.build)
- [Pebble Flow](https://pebblelife.com) — Layout inspiration
- [One Page Love](https://onepagelove.com) — Target directory

---

## 🎯 Success Criteria

**This project is done when:**

1. **All sections implemented** (Header, Hero, Build, Solve, Work, About, Contact)
2. **Performance** - Lighthouse 95+ on mobile + desktop
3. **Accessibility** - WCAG 2.1 AA compliant, VoiceOver tested
4. **Visual fidelity** - Matches design-direction.md exactly
5. **Content accuracy** - Matches content-architecture.md exactly
6. **Deployed** - Live on elementalsugar.com via Cloudflare Pages
7. **Listed** - Applied to One Page Love directory
8. **Documented** - Patterns extracted to indexes

---

## 💡 Energy-Aware Development

This project demonstrates Soft Tech principles. Honor your energy while building:

### 🌙 Low Energy
- Documentation updates
- Content tweaks (copy edits)
- Small bug fixes
- Accessibility testing

### 🌟 Medium Energy
- Component implementation
- Styling with design tokens
- Responsive design
- Standard feature work

### ⚡ High Energy
- Complex animations (shimmer effect)
- Architecture decisions
- Creative problem-solving
- System design

**Remember:** Maintenance mode is valid work. Small commits are progress. Come back to hard problems when rested.

---

## 🚀 Quick Start Commands

```bash
# Install dependencies
npm install

# Run dev server (http://localhost:4321)
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview

# Type check
npx astro check
```

---

## 🌟 Core Mantras

**When coding:**
- "Make it work, make it right, make it fast" (in that order)
- "Future-you will read this in 6 months"
- "Boring code is maintainable code"
- "Check accessibility NOW - fixes are cheap while context is fresh"

**When stuck:**
- "Check design-direction.md first"
- "Check content-architecture.md for exact copy"
- "Check global.css for design tokens"
- "Ask user before major decisions"

**When tired:**
- "Small commits are still progress"
- "Maintenance mode is valid work"
- "Come back to this when rested"

---

*"Calm, modern software crafted with a little sparkle. That's what we're building."*
