# ElementalSugar.com Development Workflows

---
created: 2026-02-04
updated: 2026-02-04
---

> **One-page Astro portfolio site for Elemental Sugar Creative Studio**
> AI discovery optimized, Lighthouse 95+, WCAG 2.1 AA compliant

## Project Context

**Goal:** Ship high-performance Astro one-page site by Feb 17, 2026
**Stack:** Astro 5.x, TypeScript, CSS Custom Properties, Cloudflare Pages
**Success Criteria:**
- Lighthouse 95+ (mobile + desktop)
- WCAG 2.1 AA compliance
- AI discovery optimized (clear problem/solution statements)
- One Page Love submission ready

**See also:** `~/claude-workspace/SoftForge/active/projects/ElementalSugar/` for design docs

---

## Standard Development Workflow

**Quick Summary:**
1. **Check patterns** (SoftForge indexes + project indexes)
2. **Start work** (Linear → branch → timer)
3. **Do the work** (with code-craftsperson agent)
4. **Present changes** (get approval before commit)
5. **Code review** (with code-reviewer agent)
6. **Quality checks** (type-check, build)
7. **Commit** (semantic message with Co-Authored-By)
8. **Push + PR** (describe changes, link Linear)
9. **Update project indexes** (document project patterns)
10. **Stop timer + close** (after merge)
11. **Update SoftForge indexes** (AFTER merge, universal patterns only)

---

### Step 0: Check Existing Patterns (Before Starting)

**Before writing code, check if we've solved this before:**

```bash
# Project-specific patterns
/Users/athena/claude-workspace/elementalsugar-astro/docs/indexes/decisions.md
/Users/athena/claude-workspace/elementalsugar-astro/docs/indexes/patterns.md

# Universal patterns by category (quick lookup)
~/claude-workspace/SoftForge/reference/indexes/by-category/accessibility.md
~/claude-workspace/SoftForge/reference/indexes/by-category/performance.md
~/claude-workspace/SoftForge/reference/indexes/by-category/ui-ux.md

# Universal patterns by language
~/claude-workspace/SoftForge/reference/indexes/by-language/css.md
~/claude-workspace/SoftForge/reference/indexes/by-language/typescript.md
```

**What to look for:**
- **Global styles first:** Design tokens in `src/styles/global.css`
- Similar components we've built (hero section patterns, layout utilities)
- Design token usage (CSS custom properties for spacing, colors, typography)
- Accessibility patterns (focus states, motion preferences, semantic HTML)
- Performance optimizations (font loading, static HTML generation)
- Astro-specific patterns (.astro components, layouts, islands architecture)

**If pattern exists:** Use it. Don't reinvent.
**If pattern doesn't exist:** Document it when done (in indexes).

### Step 1: Start Work (Linear → Branch → Timer)

```bash
# Navigate to project
cd ~/claude-workspace/elementalsugar-astro

# Start work with timer + branch
tam start 109 "Build hero section"

# Or manually:
harvest start "TAM-109: Build hero section" --project "ElementalSugar"
git checkout -b tam-109-build-hero-section
```

### Step 2: Do the Work (With Code Craftsperson Agent)

**Agent:** Work with `/Users/athena/.claude/agents/code-craftsperson.md`
- Pair programming approach
- Clarity over cleverness, working over perfect
- Semantic naming, minimal complexity
- Accessibility and performance baked in

**As you code, check these BEFORE committing:**

#### Astro/TypeScript Specific Checks

**Component Structure:**
```astro
---
// ✅ GOOD: TypeScript in frontmatter
interface Props {
  title: string;
  subtitle?: string;
}

const { title, subtitle } = Astro.props;
---

<!-- ✅ GOOD: Semantic HTML -->
<section class="hero">
  <h1>{title}</h1>
  {subtitle && <p>{subtitle}</p>}
</section>

<style>
  /* ✅ GOOD: Scoped styles */
  .hero {
    padding: var(--space-xl);
  }
</style>
```

**Performance - Static HTML:**
```astro
// ✅ Astro generates static HTML by default
// No client-side JavaScript unless explicitly added

// ❌ Only add client directives when needed
<Component client:load />   // Loads immediately
<Component client:visible /> // Loads when visible
<Component client:idle />    // Loads when browser idle
```

**Design Tokens:**
```css
/* ✅ GOOD: Use CSS custom properties */
background: var(--color-parchment);
color: var(--color-ink);
padding: var(--space-lg);

/* ❌ BAD: Hardcoded values */
background: #F6F4EF;
color: #2E2E2B;
padding: 40px;
```

#### Accessibility Checks (WCAG 2.1 AA)

**Color Contrast:**
- Text: 4.5:1 minimum
- Large text (18pt+): 3:1 minimum
- Design tokens already verified (Parchment + Ink = 12.8:1)

**Semantic HTML:**
```astro
<!-- ✅ GOOD: Semantic structure -->
<header role="banner">
  <nav role="navigation">
    <a href="#main">Skip to main content</a>
  </nav>
</header>

<main id="main" role="main">
  <section aria-labelledby="hero-heading">
    <h1 id="hero-heading">Elemental Sugar</h1>
  </section>
</main>

<!-- ❌ BAD: Divs everywhere -->
<div class="header">
  <div class="nav">...</div>
</div>
```

**Focus States:**
```css
/* ✅ All interactive elements have visible focus */
a:focus-visible {
  outline: 2px solid var(--color-focus);
  outline-offset: 4px;
}

/* ❌ NEVER do this */
*:focus {
  outline: none; /* Removes keyboard accessibility */
}
```

**Motion Preferences:**
```css
/* ✅ Always respect reduced motion preference */
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

### Step 3: Present Changes (Get Approval BEFORE Commit)

**Don't commit blindly.** Present work for user review:

```
"I've implemented [component]. Here's what I did:
- Created Hero.astro component in src/components/
- Added gradient text effect using utility class
- Styled with design tokens from global.css

Changes are staged but not committed. Want me to:
1. Proceed with commit + PR?
2. Adjust anything first?"
```

**Why:** Prevents wasted work if user wants different approach.

### Step 4: Code Review (With Code Reviewer Agent)

**Agent:** `/Users/athena/.claude/agents/code-reviewer.md`

**Reviews for:**
- Security (no XSS, injection vulnerabilities)
- Performance (static HTML, minimal JS, image optimization)
- Accessibility (WCAG 2.1 AA, semantic HTML, ARIA labels)
- YAGNI (You Aren't Gonna Need It - no premature abstraction)
- Maintainability (clear naming, documented patterns)

**After code review approval, proceed to quality checks.**

### Step 5: Quality Checks

```bash
# Type check
npx astro check

# Build (catches errors)
npm run build

# Preview production build
npm run preview
```

**All checks must pass before committing.**

### Step 6: Commit (Semantic + Co-Authored-By)

```bash
git add [files]
git commit -m "$(cat <<'EOF'
feat: implement hero section (TAM-109)

Added hero section with gradient logo and energy-aware design.

Changes:
- Created Hero.astro component with TypeScript
- Implemented gradient text effect (pine → moss → iris → rose)
- Used design tokens for all spacing/colors
- Responsive layout (mobile/desktop)

Example:
- Tagline: "Calm, modern software crafted with a little sparkle"
- Uses Cardo serif for headlines, Comfortaa for tagline

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>
EOF
)"
```

**Commit types:** `feat:`, `fix:`, `refactor:`, `docs:`, `test:`, `chore:`

### Step 7: Push + Create PR

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

### Step 8: Update Project Indexes (Immediately After PR)

**IMPORTANT:** Document patterns while context is fresh.

```bash
# Project-specific decisions
~/claude-workspace/elementalsugar-astro/docs/indexes/decisions.md

# Reusable patterns
~/claude-workspace/elementalsugar-astro/docs/indexes/patterns.md
```

**Document:**
- Why you chose this approach (decisions.md)
- Reusable component patterns (patterns.md)
- Design token usage examples
- Accessibility techniques
- Astro-specific patterns (.astro component structure)

**Example entry:**

```markdown
## Hero Section Gradient Text (TAM-109, 2026-02-04)

**Decision:** Use .gradient-text utility class instead of inline styles
**Why:** Reusable across all section headings, maintains consistency
**Pattern:**
  - Apply .gradient-text class to any heading
  - Gradient flows: pine → moss → iris → rose
  - Use .gradient-text-light for dark backgrounds

**Code:**
\`\`\`astro
<h1 class="gradient-text">We BUILD</h1>
\`\`\`
```

### Step 9: Stop Timer + Close Linear (After Merge)

```bash
# Stop timer
tam stop

# After PR merges, update Linear
# (Using Linear MCP - available in this repo now)
mcp__linear__update_issue({
  id: "TAM-109",
  state: "Done"
})

# Add comment with time + patterns documented
mcp__linear__create_comment({
  issueId: "TAM-109",
  body: "✅ Completed in PR #X\n\nTime: [X hours]\n\nPatterns documented in:\n- docs/indexes/patterns.md (gradient text utility)"
})
```

### Step 10: Update SoftForge Indexes (AFTER Merge, Universal Only)

**Only document patterns that apply to ALL projects.**

```bash
# Universal patterns by category
~/claude-workspace/SoftForge/reference/indexes/by-category/accessibility.md
~/claude-workspace/SoftForge/reference/indexes/by-category/ui-ux.md

# Universal patterns by language
~/claude-workspace/SoftForge/reference/indexes/by-language/css.md
```

**Ask yourself:**
- Is this pattern universal (applies to any project)?
- Or project-specific (only makes sense for ElementalSugar)?

**Universal examples:**
- CSS custom property patterns
- Accessibility focus state patterns
- Responsive layout utilities

**Project-specific examples:**
- ElementalSugar's mystical gold gradient
- Specific color palette choices
- One-page portfolio structure

---

## Quality Standards

### Performance (Lighthouse 95+)

**Required:**
- Static HTML generation (Astro does this by default)
- Font optimization (preconnect, font-display: swap)
- Image optimization (proper sizing, lazy loading)
- Minimal CSS (scoped styles, no unused code)
- Zero JavaScript by default

**Test:**
```bash
npm run build
npm run preview
# Use Lighthouse in Chrome DevTools
```

### Accessibility (WCAG 2.1 AA)

**Required:**
- Color contrast 4.5:1 (text), 3:1 (large text)
- Semantic HTML (header, nav, main, section)
- ARIA labels where needed
- Keyboard navigation (all interactive elements focusable)
- Focus indicators visible
- Motion preference respected

**Test:**
```bash
# VoiceOver (macOS)
Cmd+F5 to enable, VO+A to read all

# Keyboard navigation
Tab through all interactive elements
Enter/Space to activate

# Lighthouse accessibility audit
# Chrome DevTools → Lighthouse → Accessibility
```

### Code Quality

**TypeScript:**
- No `any` types (use `unknown` if needed)
- Explicit interfaces for props
- Type all function parameters and returns

**Astro Components:**
- Props interface in frontmatter
- Scoped styles when possible
- Minimal client-side JavaScript
- Semantic HTML always

**CSS:**
- Use design tokens (CSS custom properties)
- Mobile-first responsive design
- No magic numbers (use spacing scale)
- Respect motion preferences

---

## Common Patterns

### Creating an Astro Component

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
    <h1>{title}</h1>
    {subtitle && <p class="subtitle">{subtitle}</p>}
    {showCTA && <a href="#contact" class="cta">Get Started →</a>}
  </div>
</section>

<style>
  .hero {
    padding: var(--space-section);
    background: var(--color-bg-primary);
  }

  .container {
    max-width: var(--container-max);
    margin-inline: auto;
  }

  h1 {
    font-family: var(--font-serif);
    font-size: var(--font-size-3xl);
    line-height: var(--line-height-tight);
  }
</style>
```

### Using the Component

```astro
---
// src/pages/index.astro
import BaseLayout from '../layouts/BaseLayout.astro';
import Hero from '../components/Hero.astro';
---

<BaseLayout title="Elemental Sugar Creative Studio">
  <Hero
    title="Calm, modern software"
    subtitle="crafted with a little sparkle"
  />
</BaseLayout>
```

---

## Astro-Specific Tips

**Islands Architecture:**
- Astro sends zero JS by default
- Only add `client:*` directives when needed
- Prefer static HTML over client-side interactivity

**File-based Routing:**
- `src/pages/index.astro` → `/`
- `src/pages/about.astro` → `/about`
- (This project is one-page, so just index.astro)

**Layouts:**
- Base layout in `src/layouts/BaseLayout.astro`
- Includes `<slot />` for page content
- Shared HTML structure, meta tags, global styles

**Styles:**
- Global: `src/styles/global.css` (imported in BaseLayout)
- Scoped: `<style>` in .astro components
- Design tokens available everywhere via CSS custom properties

---

## Resources

**Astro Docs:**
- [Component Reference](https://docs.astro.build/en/reference/api-reference/)
- [TypeScript](https://docs.astro.build/en/guides/typescript/)
- [Styling](https://docs.astro.build/en/guides/styling/)

**Project Docs:**
- `/docs/README.md` - Complete design system reference
- `src/styles/global.css` - All design tokens
- `~/claude-workspace/SoftForge/active/projects/ElementalSugar/design-direction.md`

---

*Keep it simple. Astro makes it easy to build fast, accessible sites.*
