# Design System Squad Setup

Instructions for auto-creating the design system squad during onboarding.
Only read this file when the user confirms the company produces visual content.

## What to Create

Populate `squads/design-system/` with the following structure:

```
squads/design-system/
├── squad.yaml
├── _memory/
│   ├── design-tokens.md   — colors, fonts, spacing, component patterns
│   └── brand-guidelines.md — logo usage, color contexts, tone of voice
```

## squad.yaml Template

```yaml
squad:
  code: design-system
  setor: design
  grupo: identidade
  sessao: marca
  name: Design System
  description: Single source of truth for visual identity
  icon: palette
  version: "1.0.0"

  company: "_expxagents/_memory/company.md"
  preferences: "_expxagents/_memory/preferences.md"
  memory: "_memory/memories.md"
  assets_path: "_expxagents/_assets/"
```

## design-tokens.md — Populate From Extracted Data

Fill using the colors/fonts extracted during onboarding WebFetch:

```markdown
# Design Tokens

## Colors
- Primary: #<hex>
- Secondary: #<hex>
- Accent: #<hex>
- Background: #<hex>
- Text: #<hex>
- Muted: #<hex>

## Typography
- Heading font: <family>
- Body font: <family>
- Mono font: <family or "system-mono">

## Spacing Scale
- xs: 4px | sm: 8px | md: 16px | lg: 24px | xl: 48px

## Border Radius
- Default: 4px | Card: 8px | Pill: 999px

## Shadows
- sm: 0 1px 3px rgba(0,0,0,0.1)
- md: 0 4px 12px rgba(0,0,0,0.1)

## Visual Style
<modern/corporate/playful/minimalist — from website analysis>
```

## brand-guidelines.md — Populate From Research

```markdown
# Brand Guidelines

## Logo Usage
- Primary logo: `_expxagents/_assets/logo/`
- Minimum size: 32px height
- Clear space: 1× logo height on all sides
- Do NOT stretch, recolor, or add effects

## Color Usage
- Primary: CTAs, links, highlights
- Secondary: backgrounds, cards
- Accent: badges, tags, hover states
- Never use primary on dark backgrounds without contrast check

## Tone of Voice
<from website/company description>

## Do's and Don'ts
- DO: <from brand analysis>
- DON'T: <from brand analysis>
```

## Rules for Visual Squads

**All squads that produce visual work** (landing pages, social media, emails, presentations) MUST:
1. Read `squads/design-system/_memory/design-tokens.md` before generating visual output
2. Read `squads/design-system/_memory/brand-guidelines.md` for brand rules
3. Use assets from `_expxagents/_assets/` for logos and images
