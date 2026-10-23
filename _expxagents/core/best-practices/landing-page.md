# Landing Page — Best Practices

## Princípios de Design

### 1. Design System First
Toda landing page DEVE começar com um design system definido via CSS custom properties. Zero valores hardcoded.

```css
:root {
  /* === CORE TOKENS === */
  /* Colors — use off-black/off-white, never pure #000/#fff */
  --color-base-900: #0f172a;
  --color-base-800: #1e293b;
  --color-base-700: #334155;
  --color-base-100: #f1f5f9;
  --color-base-50: #f8fafc;
  --color-white: #ffffff;

  /* Accent — single brand color + hover state */
  --color-accent: oklch(0.65 0.25 15);    /* vibrant, perceptually uniform */
  --color-accent-hover: oklch(0.58 0.25 15);
  --color-accent-subtle: oklch(0.65 0.25 15 / 0.1);

  /* Semantic */
  --color-surface: var(--color-white);
  --color-surface-alt: var(--color-base-50);
  --color-surface-dark: var(--color-base-900);
  --color-on-surface: var(--color-base-800);
  --color-on-surface-muted: var(--color-base-700);
  --color-on-dark: var(--color-base-50);
  --color-success: oklch(0.72 0.19 150);

  /* === SPACING (4px base unit) === */
  --space-1: 0.25rem;   /* 4px */
  --space-2: 0.5rem;    /* 8px */
  --space-3: 0.75rem;   /* 12px */
  --space-4: 1rem;      /* 16px */
  --space-6: 1.5rem;    /* 24px */
  --space-8: 2rem;      /* 32px */
  --space-12: 3rem;     /* 48px */
  --space-16: 4rem;     /* 64px */
  --space-20: 5rem;     /* 80px */
  --space-24: 6rem;     /* 96px */
  --space-32: 8rem;     /* 128px */

  /* Section spacing — generous */
  --section-py: clamp(var(--space-16), 10vw, var(--space-32));
  --section-px: var(--space-6);
  --container-max: 1200px;
  --container-narrow: 720px;

  /* === TYPOGRAPHY === */
  --font-display: 'Plus Jakarta Sans', 'Inter', system-ui, sans-serif;
  --font-body: 'Inter', system-ui, sans-serif;
  --font-mono: 'JetBrains Mono', 'Fira Code', monospace;

  /* Fluid type scale — min @ 320px, max @ 1200px */
  --text-display: clamp(2.5rem, 5vw + 1rem, 4.5rem);
  --text-h1: clamp(2rem, 4vw + 0.5rem, 3.5rem);
  --text-h2: clamp(1.5rem, 3vw + 0.25rem, 2.25rem);
  --text-h3: clamp(1.125rem, 2vw + 0.25rem, 1.5rem);
  --text-body: clamp(1rem, 1vw + 0.5rem, 1.125rem);
  --text-small: 0.875rem;
  --text-caption: 0.75rem;

  --leading-tight: 1.15;
  --leading-normal: 1.6;
  --leading-relaxed: 1.8;

  --tracking-tight: -0.02em;
  --tracking-normal: 0;
  --tracking-wide: 0.05em;
  --tracking-widest: 0.1em;

  /* === RADIUS === */
  --radius-sm: 0.375rem;   /* 6px — inputs, small elements */
  --radius-md: 0.75rem;    /* 12px — cards, containers */
  --radius-lg: 1rem;       /* 16px — featured cards */
  --radius-xl: 1.5rem;     /* 24px — hero elements */
  --radius-full: 9999px;   /* pills, avatars */

  /* === SHADOWS (multi-layered for realism) === */
  --shadow-sm:
    0 1px 2px oklch(0 0 0 / 0.04),
    0 1px 3px oklch(0 0 0 / 0.06);
  --shadow-md:
    0 2px 4px oklch(0 0 0 / 0.04),
    0 4px 8px oklch(0 0 0 / 0.06),
    0 8px 16px oklch(0 0 0 / 0.04);
  --shadow-lg:
    0 4px 8px oklch(0 0 0 / 0.03),
    0 8px 16px oklch(0 0 0 / 0.06),
    0 16px 32px oklch(0 0 0 / 0.06),
    0 32px 64px oklch(0 0 0 / 0.04);
  --shadow-xl:
    0 8px 16px oklch(0 0 0 / 0.04),
    0 16px 32px oklch(0 0 0 / 0.08),
    0 32px 64px oklch(0 0 0 / 0.08),
    0 64px 128px oklch(0 0 0 / 0.06);
  --shadow-accent:
    0 4px 12px oklch(0.65 0.25 15 / 0.25),
    0 8px 24px oklch(0.65 0.25 15 / 0.15);

  /* === TRANSITIONS === */
  --ease-out: cubic-bezier(0.16, 1, 0.3, 1);
  --ease-in-out: cubic-bezier(0.65, 0, 0.35, 1);
  --duration-fast: 150ms;
  --duration-normal: 250ms;
  --duration-slow: 400ms;
}
```

### 2. Layout Patterns

**Container:**
```css
.container {
  max-width: var(--container-max);
  margin: 0 auto;
  padding: 0 var(--section-px);
}
.container--narrow { max-width: var(--container-narrow); }
```

**Section rhythm — alternating density:**
```
[HERO — full-bleed, dense, dark]
[PROBLEM — spacious, light, breathing room]
[SOLUTION — medium density, alternating columns]
[PROOF — full-bleed, dark, contrasting]
[CTA — full-bleed, gradient, dense]
```

**Grid patterns:**
- Stats/numbers: `grid-template-columns: repeat(auto-fit, minmax(200px, 1fr))`
- Cards: `grid-template-columns: repeat(auto-fill, minmax(300px, 1fr))`
- Two-column content: `grid-template-columns: 1fr 1fr` with `gap: var(--space-16)`
- Asymmetric: `grid-template-columns: 1.2fr 0.8fr`

### 3. Typography Rules

- **Display (hero):** --font-display, weight 800, --leading-tight, --tracking-tight
- **Headings:** --font-display, weight 700, --leading-tight
- **Body:** --font-body, weight 400-500, --leading-normal
- **Labels/badges:** --font-body, weight 600, uppercase, --tracking-widest, --text-caption
- **NEVER** use font-size less than 16px for body text on mobile
- **ALWAYS** use clamp() for fluid sizing between breakpoints

### 4. Color Usage

- Background alternation: --color-surface → --color-surface-alt → --color-surface-dark
- Text: --color-on-surface for primary, --color-on-surface-muted for secondary
- Accent: ONLY on CTAs, key numbers, highlights, and active states (<15% of page)
- Gradients: Use subtle gradients (same hue, different lightness) for backgrounds
- Never use opacity for text colors — use explicit muted color tokens

### 5. Component Patterns

**Button/CTA:**
```css
.btn-primary {
  background: var(--color-accent);
  color: var(--color-white);
  padding: var(--space-4) var(--space-8);
  border-radius: var(--radius-md);
  font-weight: 700;
  font-size: var(--text-body);
  box-shadow: var(--shadow-accent);
  transition: all var(--duration-normal) var(--ease-out);
}
.btn-primary:hover {
  background: var(--color-accent-hover);
  transform: translateY(-2px);
  box-shadow: var(--shadow-lg);
}
```

**Card:**
```css
.card {
  background: var(--color-surface);
  border-radius: var(--radius-lg);
  padding: var(--space-8);
  box-shadow: var(--shadow-md);
  border: 1px solid oklch(0 0 0 / 0.05);
  transition: all var(--duration-normal) var(--ease-out);
}
.card:hover {
  transform: translateY(-4px);
  box-shadow: var(--shadow-lg);
}
```

**Badge/Pill:**
```css
.badge {
  display: inline-flex;
  align-items: center;
  gap: var(--space-2);
  padding: var(--space-1) var(--space-3);
  border-radius: var(--radius-full);
  font-size: var(--text-caption);
  font-weight: 600;
  letter-spacing: var(--tracking-wide);
  text-transform: uppercase;
  background: var(--color-accent-subtle);
  color: var(--color-accent);
}
```

### 6. Animation Guidelines

**Scroll reveals (IntersectionObserver):**
```css
.reveal {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity var(--duration-slow) var(--ease-out),
              transform var(--duration-slow) var(--ease-out);
}
.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}
```

- Stagger children: `transition-delay: calc(var(--index) * 80ms)`
- Only animate `opacity` and `transform` — never width, height, margin, or padding
- Use `will-change: transform, opacity` on animated elements
- Respect `prefers-reduced-motion` media query

### 7. Responsive Strategy

- Mobile-first: base styles are mobile, media queries add desktop
- Breakpoints: 640px (sm), 768px (md), 1024px (lg), 1280px (xl)
- Use `clamp()` for fluid values between breakpoints
- Stack columns on mobile, grid on desktop
- Touch targets: minimum 44x44px on mobile
- Hide non-essential content on mobile (less is more)

### 8. Performance Requirements

- Single HTML file with inline CSS and JS
- Fonts: max 2 families, preconnect + font-display: swap
- Images: WebP, lazy loading, explicit dimensions (aspect-ratio)
- JS: vanilla only, defer/async, IntersectionObserver for scroll effects
- Target: Lighthouse 95+ on all categories
- Above-the-fold content must render without JS

### 9. Accessibility Minimum

- Semantic HTML: header, nav, main, section, article, footer
- Heading hierarchy: single H1, sequential H2-H6
- Color contrast: 4.5:1 for text, 3:1 for UI elements
- Focus-visible on all interactive elements
- ARIA attributes on custom widgets (accordion, modal)
- Skip-to-content link
- Form labels and error messages
- lang attribute on html element

### 10. Quality Checklist

Before finalizing any landing page:

- [ ] All values use CSS custom properties (zero hardcoded)
- [ ] Typography uses clamp() for fluid sizing
- [ ] Shadows are multi-layered (min 2 layers)
- [ ] Whitespace between sections is generous (80-128px)
- [ ] Max 3 colors used (base + surface + accent)
- [ ] CTAs have accent shadow (--shadow-accent)
- [ ] Cards/elements have subtle borders (1px, <5% opacity)
- [ ] Scroll animations use IntersectionObserver
- [ ] Respects prefers-reduced-motion
- [ ] Mobile-first CSS with min-width media queries
- [ ] All images have alt text
- [ ] Form inputs have associated labels
- [ ] Focus states are visible and styled
- [ ] Lighthouse score >90 in all categories
- [ ] "Squint test" passes — hierarchy is clear at a glance
