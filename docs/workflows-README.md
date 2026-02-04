# ElementalSugar.com Documentation

---
created: 2026-02-04
updated: 2026-02-04
---

## Purpose

This directory provides quick access to project-specific decisions and links to universal SoftForge patterns. The goal is to enable Claude Code to navigate between elementalsugar-astro and SoftForge seamlessly.

## Structure

```
docs/
├── workflows-README.md          ← You are here
├── workflows.md                 ← Development workflows (Linear → PR → Deploy)
├── indexes/                     ← Project-specific quick lookups
│   ├── decisions.md             ← "Why did we do X?" (ElementalSugar-specific)
│   └── patterns.md              ← Reusable patterns discovered here
└── softforge-links/             ← Symlinks to key SoftForge docs
    ├── design-direction.md      → Visual system (colors, typography, layout)
    ├── content-architecture.md  → All copy (finalized)
    ├── design-values.md         → Soft tech design philosophy
    ├── professional-positioning.md → Service offerings, target audiences
    ├── archetypes.md            → Systems Weaver identity
    ├── core-truths.md           → Foundational beliefs
    ├── decisions.md             → Universal decision log
    ├── patterns.md              → Universal reusable patterns
    ├── code-craftsperson.md     → Pair programming guide
    └── code-reviewer.md         → Code review patterns
```

## Quick Access

### Project-Specific (Check First)

- **workflows.md** - Development workflows (Linear → Branch → PR → Deploy, quality checks)
- **indexes/decisions.md** - ElementalSugar-specific decisions ("Why did we use Astro?")
- **indexes/patterns.md** - Patterns discovered/refined in this project
- **src/styles/global.css** - Complete design token system

### SoftForge Universal (Check When Needed)

**Via symlinks in `docs/softforge-links/`:**

*Design & Content:*
- **design-direction.md** - Complete visual system (colors, typography, spacing, mystical SVGs)
- **content-architecture.md** - All copy finalized (Hero, Build, Solve, Work, About, Contact)

*Values & Identity:*
- **design-values.md** - Soft tech design philosophy (Five Pillars)
- **professional-positioning.md** - Service offerings, target audiences, client-facing copy
- **archetypes.md** - Systems Weaver identity definition
- **core-truths.md** - Foundational beliefs and healing framework

*Indexes:*
- **decisions.md** - Universal decisions across all projects
- **patterns.md** - Universal reusable patterns

*Agent Guides:*
- **code-craftsperson.md** - Pair programming partner (writing code, debugging, implementing features)
- **code-reviewer.md** - Code review patterns (security, performance, accessibility, YAGNI)

**Direct paths (when symlinks aren't enough):**
- `~/claude-workspace/SoftForge/reference/indexes/` - All quick lookup indexes
- `~/claude-workspace/SoftForge/reference/values/` - Identity, design values, archetypes
- `~/claude-workspace/SoftForge/reference/tools/` - Reusable testing tools
- `~/claude-workspace/SoftForge/active/projects/ElementalSugar/` - Project tracking, design docs

## Workflow

### Before Starting Work

1. Check `docs/workflows.md` - See full development workflow
2. Check `src/styles/global.css` - **Design tokens** (colors, typography, spacing, all CSS custom properties)
3. Check `docs/softforge-links/design-direction.md` - Visual system details
4. Check `docs/indexes/decisions.md` - Did we already decide this?
5. Check `docs/indexes/patterns.md` - Is there a pattern for this?
6. Check SoftForge indexes if not found locally

### After Completing Work

1. Made a decision? Add to `docs/indexes/decisions.md`
2. Discovered a reusable pattern? Add to `docs/indexes/patterns.md`
3. Pattern is universal (applies to all projects)? Add to SoftForge instead
4. Update Linear issue with learnings

## Key Project Documents

**In this repo:**
- `/CLAUDE.md` - Complete project context, design tokens, workflow
- `/docs/README.md` - Complete design system reference (400+ lines)
- `/src/styles/global.css` - All design tokens (CSS custom properties)

**In SoftForge:**
- `/active/projects/ElementalSugar/design-direction.md` - Visual system
- `/active/projects/ElementalSugar/content-architecture.md` - All copy
- `/active/projects/ElementalSugar/character-sheet.md` - Project status

## Linear Integration

- Tasks tracked in Linear (TAM-* issues)
- Linear MCP available in this repo (`.mcp.json`, `.claude/settings.local.json`)
- Use Linear tools to update issues, add comments, check status

## Technology

**Stack:**
- **Astro 5.17.1** - Static site generator
- **TypeScript** - Type safety
- **CSS Custom Properties** - Design tokens (no Tailwind, no Sass)
- **Cloudflare Pages** - Global edge deployment (planned)

**Why Astro?**
- Zero JavaScript by default
- Perfect for content-focused sites
- Lighthouse 95+ out of the box
- 10x smaller bundle than Next.js for static content

---

*Lightweight docs structure for a one-page Astro site. Keep it simple.*
