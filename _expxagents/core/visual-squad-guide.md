# Visual Squad Guide

Instructions for designing squads that produce visual output (social media, landing pages, emails, presentations, ads, banners, slides).
Only read this file when the squad being designed has visual outputs.

## Design System Integration

1. **ALWAYS include** in squad.yaml:
   ```yaml
   design_system: "squads/design-system/_memory/design-tokens.md"
   brand_guidelines: "squads/design-system/_memory/brand-guidelines.md"
   assets_path: "_expxagents/_assets/"
   ```
2. **Agent instructions** must include: "Before producing any visual output, read `squads/design-system/_memory/design-tokens.md` for colors, fonts, and spacing. Read `squads/design-system/_memory/brand-guidelines.md` for brand rules. Use assets from `_expxagents/_assets/` for logos and images."
3. The first step of visual squads should always reference the design system tokens.

## Pencil Visual Templates

### When to Enable

| Squad Type | visual_templates? |
|-----------|------------------|
| Instagram Post/Carousel/Stories | YES |
| Landing Page | YES |
| Slide Deck | YES |
| Email Marketing | YES |
| Ads (Meta/Google) | YES |
| Branding/Web Design | YES |
| Blog | NO |
| Instagram Reels | NO |
| Non-visual squads | NO |

### squad.yaml Configuration

```yaml
visual_templates:
  enabled: true
  format: "4:5"   # 4:5 for IG, 16:9 for slides, etc.
  count: 3
```

### Standard Dimensions

| Type | Width x Height | Format |
|------|---------------|--------|
| Instagram Post | 1080x1350 | 4:5 |
| Instagram Post (square) | 1080x1080 | 1:1 |
| Instagram Story | 1080x1920 | 9:16 |
| Slide Deck | 1920x1080 | 16:9 |
| Email Header | 600x200 | 3:1 |
| Blog Cover | 1200x630 | ~2:1 |
| Landing Page | 1440x900+ | ~16:10 |

### Directory Structure

Create `templates/` directory inside the squad:

```
squads/<setor>/<grupo>/<sessao>/<code>/
├── squad.yaml
├── templates/
├── agents/
└── _memory/
```

### Designer Agent Instructions

Include in the designer agent's .md:

```markdown
## Pencil Templates
- **Templates directory:** `templates/`
- **Sync command:** Run `expxagents sync-templates` after editing .pen files
- **Template rotation:** Rotate through available templates for variety
- **Always read the template .md files** before generating HTML output
```

## Validation Checklist (visual squads only)

- [ ] `design_system`, `brand_guidelines`, and `assets_path` included in squad.yaml
- [ ] `visual_templates` block added for image-producing squads
- [ ] `templates/` directory created
- [ ] Designer agent instructions reference the design system
