# Decision Log (ElementalSugar.com)

---
created: 2026-02-02
updated: 2026-02-04
purpose: Quick reference for "Why did we do X?" questions (project-specific)
---

## How to Use This Log

**Format:** Descending date (newest first)

**When to add:** After making a significant technical or design decision

**Keep it short:** One paragraph "why", link to detailed docs if needed

**Universal decisions:** If it applies to ALL projects, add to SoftForge instead:
`~/claude-workspace/SoftForge/reference/indexes/decisions.md`

---

## 2026-02-04: Separate CSS Files Per Component (Not Scoped Styles)

**Decision:** Use separate CSS files in `src/styles/components/` with BEM naming, imported via Astro frontmatter, instead of Astro's built-in scoped `<style>` blocks.

**Why:**
- **Consistency** - `global.css` already has hero styles in it; having some styles in `styles/` and some scoped creates an inconsistent pattern
- **Readability** - Header.astro went from 343 lines (74% CSS) to 94 lines (just markup + script). Easier to scan and edit.
- **Familiar pattern** - Mirrors the Next.js build's co-located SCSS files per component. Same mental model, plain CSS instead of SCSS.
- **BEM naming prevents collisions** - `.header__nav-link`, `.btn--gradient` are unique enough without Astro's scoping hashes

**Trade-off:** Styles are not auto-scoped by Astro. Relies on naming discipline (BEM) to prevent collisions. Acceptable because BEM naming makes collisions essentially impossible and the team is already comfortable with the pattern.

**Structure:**
```
src/styles/
  global.css                  (tokens, resets, utilities)
  components/
    header.css                (header layout, logo, nav, scroll blur)
    button.css                (reusable .btn / .btn--gradient)
```

**Related:** TAM-111, PR #3

---

## 2026-02-04: Darkened Moss Color for Universal Accessibility

**Decision:** Updated Moss color from `#6F7F6A` to `#5A6A55` in design tokens.

**Why:**
- **Original Moss contrast:** 3.74:1 on Parchment - passed WCAG AA for large text (20px bold) but failed for normal text (needs 4.5:1)
- **New Moss contrast:** 5.07:1 on Parchment, 4.51:1 on Stone - passes WCAG AA for all text sizes
- **Maintains aesthetic:** Still reads as "moss green" while being universally accessible
- **Works across backgrounds:** Passes on both Parchment (main) and Stone (subtle sections)
- **Hero section tagline:** Uses Moss at 20px weight 800 (bold), now accessible regardless of text size interpretation

**Trade-off:** Slightly darker than original, but improved accessibility outweighs minimal aesthetic shift.

**Related:** TAM-101 Hero section polish, style guide accessibility documentation

---

## 2026-02-02: Next.js Static Export for Cloudflare Pages

**Decision:** Use `output: 'export'` in next.config.ts for static HTML generation.

**Why:**
- **Edge delivery** - Cloudflare Pages serves from global CDN (faster than origin server)
- **Zero server costs** - No Node.js runtime needed
- **Simpler deployment** - Push to GitHub, auto-deploy to Cloudflare
- **One-page site** - No dynamic routes or server-side rendering needed
- **Lighthouse performance** - Static HTML loads fastest

**Trade-off:** Can't use server-side features (API routes, ISR, SSR). Acceptable for one-page portfolio.

**See:** CLAUDE.md "Static Export Config" section

---

## 2026-02-02: Local Atkinson Hyperlegible Fonts (Not Google)

**Decision:** Host Atkinson Hyperlegible Next font files locally, not via Google Fonts.

**Why:**
- **Accessibility-first** - Atkinson Hyperlegible designed for low-vision readers
- **Not on Google Fonts** - Google only has original version, not "Next" with extended weights
- **Performance** - Local fonts = one fewer external request
- **Privacy** - No Google tracking for font requests
- **Variable font available** - Single WOFF2 file covers all weights

**Implementation:** Font files in `/public/fonts/`, CSS @font-face in globals.css

**Font source:** `/Users/athena/claude-workspace/SoftForge/active/projects/ElementalSugar/Atkinson Hyperlegible Next/`

---

## Template for New Entries

```markdown
## YYYY-MM-DD: Decision title

**Decision:** What did we decide?

**Why:** One paragraph explaining the reasoning

**Trade-offs:** What we accepted in exchange (optional)

**See:** Link to related docs/code (optional)
```
