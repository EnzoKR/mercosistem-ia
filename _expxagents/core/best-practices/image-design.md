---
platform: universal
format: image-design
constraints:
  max_chars: null
  image_ratio: null
  max_hashtags: null
---

# Best Practices: Image Design

## Core Principles

Visual content communicates faster than text and sets the first impression. Every image asset should be intentional in its composition, on-brand in its aesthetics, and technically optimized for its delivery platform.

- **Purpose first.** Ask: what should the viewer feel, understand, or do as a result of seeing this image?
- **Brand cohesion.** Consistent color palette, typography, and visual style create recognition across touchpoints.
- **Technical precision.** Deliver at the correct dimensions, resolution, and file format for each platform.

## Technical Specifications by Platform

| Platform | Format | Dimensions | Max File Size |
|----------|--------|------------|---------------|
| Instagram Feed | Square | 1080x1080px | 8MB |
| Instagram Feed | Portrait | 1080x1350px | 8MB |
| Instagram Stories / Reels | Vertical | 1080x1920px | 30MB |
| LinkedIn Feed | Horizontal | 1200x627px | 5MB |
| Twitter/X | Horizontal | 1200x675px | 5MB |
| YouTube Thumbnail | Horizontal | 1280x720px | 2MB |
| YouTube Shorts | Vertical | 1080x1920px | — |
| Blog Featured | Horizontal | 1200x628px | < 200KB (web) |
| Email Banner | Horizontal | 600x200px | < 100KB |
| WhatsApp | Any | Max 1600px wide | 5MB |

## Design Structure

```
[BRAND LAYER]
- Color palette: 2–3 primary colors; 1–2 accent colors
- Typography: 1 display font (headlines), 1 body font (captions)
- Logo position: consistent corner placement at consistent size

[HIERARCHY LAYER]
- Focal point: one dominant element that the eye lands on first
- Secondary elements: support without competing
- Negative space: intentional emptiness that prevents visual noise

[TEXT OVERLAY (if applicable)]
- Max 20% of image area covered by text (for ad approval compliance)
- Minimum font size: 24px for mobile readability
- Text contrast: 4.5:1 minimum ratio against background (WCAG AA)

[CTA LAYER (for ads/promotional assets)]
- Button or arrow graphic indicating next action
- Urgency element (countdown, "Limited", "Free")
```

## Guidelines

- Use a 3-column, 3-row grid as the foundation for composition (rule of thirds).
- High-contrast images perform better in feed environments — busy backgrounds cause content to disappear.
- Real people and faces drive significantly more engagement than illustrations or product-only shots.
- Accessible color contrast: use WebAIM Contrast Checker to verify text legibility.
- Deliver web images as WebP (lossy compression, smaller files than JPEG at equivalent quality).
- Maintain a master asset library with source files (Figma, Adobe) separate from exported deliverables.
- Always include descriptive alt text when images are published digitally.
- Test image performance: A/B test thumbnail variations using a 50/50 split for 48 hours before choosing a winner.

## File Format Guide

| Use Case | Format | Reason |
|----------|--------|--------|
| Photos with no transparency | JPEG / WebP | Smallest file size |
| Logos, icons, graphics | PNG-24 | Lossless + transparency |
| Animated graphics | GIF / WebP (animated) | Cross-platform animated |
| Web images | WebP | Best quality-to-size ratio |
| Print | TIFF / PDF | Lossless, print-ready |
| Social media | JPEG or PNG | Universal compatibility |
