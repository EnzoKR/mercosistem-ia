# Landing Page React — Best Practices

## Project Structure

### Next.js (recommended for SEO-critical pages)
```
├── app/
│   ├── layout.tsx          # Root layout, fonts, metadata
│   ├── page.tsx            # Landing page entry
│   └── globals.css         # Design tokens + base styles
├── components/
│   ├── atoms/              # Button, Badge, Heading, Text, Input, Image
│   ├── molecules/          # FeatureCard, TestimonialCard, PricingCard, StatCounter, CTAGroup
│   ├── organisms/          # HeroSection, FeaturesGrid, PricingSection, FAQAccordion, Footer
│   └── ui/                 # Container, Section (layout primitives)
├── hooks/                  # useIntersectionObserver, useMediaQuery, useCountUp
├── lib/                    # cn() utility, constants
└── public/                 # Static assets (images, fonts)
```

### Vite + React (lightweight, no SSR needed)
```
├── src/
│   ├── main.tsx
│   ├── App.tsx
│   ├── index.css           # Design tokens + base styles
│   ├── components/
│   │   ├── atoms/
│   │   ├── molecules/
│   │   ├── organisms/
│   │   └── ui/
│   ├── hooks/
│   └── lib/
└── public/
```

### File Naming Conventions
- Components: `PascalCase.tsx` — `Button.tsx`, `HeroSection.tsx`
- Hooks: `camelCase.ts` — `useIntersectionObserver.ts`
- Utilities: `camelCase.ts` — `cn.ts`
- Styles (CSS Modules): `ComponentName.module.css`
- One component per file, export as default
- Co-locate tests: `Button.test.tsx` next to `Button.tsx`

---

## Design System Setup

Use the SAME design tokens from the HTML version, injected via CSS custom properties. This ensures visual parity between HTML and React landing pages.

### Design Tokens (globals.css / index.css)
```css
:root {
  /* === CORE TOKENS (identical to HTML version) === */

  /* Colors — off-black/off-white, never pure #000/#fff */
  --color-base-900: #0f172a;
  --color-base-800: #1e293b;
  --color-base-700: #334155;
  --color-base-100: #f1f5f9;
  --color-base-50: #f8fafc;
  --color-white: #ffffff;

  /* Accent — single brand color + hover state */
  --color-accent: oklch(0.65 0.25 15);
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
  --space-1: 0.25rem;
  --space-2: 0.5rem;
  --space-3: 0.75rem;
  --space-4: 1rem;
  --space-6: 1.5rem;
  --space-8: 2rem;
  --space-12: 3rem;
  --space-16: 4rem;
  --space-20: 5rem;
  --space-24: 6rem;
  --space-32: 8rem;

  /* Section spacing */
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
  --radius-sm: 0.375rem;
  --radius-md: 0.75rem;
  --radius-lg: 1rem;
  --radius-xl: 1.5rem;
  --radius-full: 9999px;

  /* === SHADOWS (multi-layered) === */
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

### Tailwind CSS Configuration (optional)

If using Tailwind, extend the config to reference the same CSS tokens:

```ts
// tailwind.config.ts
import type { Config } from 'tailwindcss';

const config: Config = {
  content: ['./src/**/*.{ts,tsx}', './app/**/*.{ts,tsx}'],
  theme: {
    extend: {
      colors: {
        base: {
          50: 'var(--color-base-50)',
          100: 'var(--color-base-100)',
          700: 'var(--color-base-700)',
          800: 'var(--color-base-800)',
          900: 'var(--color-base-900)',
        },
        accent: {
          DEFAULT: 'var(--color-accent)',
          hover: 'var(--color-accent-hover)',
          subtle: 'var(--color-accent-subtle)',
        },
        surface: {
          DEFAULT: 'var(--color-surface)',
          alt: 'var(--color-surface-alt)',
          dark: 'var(--color-surface-dark)',
        },
      },
      fontFamily: {
        display: ['var(--font-display)'],
        body: ['var(--font-body)'],
        mono: ['var(--font-mono)'],
      },
      borderRadius: {
        sm: 'var(--radius-sm)',
        md: 'var(--radius-md)',
        lg: 'var(--radius-lg)',
        xl: 'var(--radius-xl)',
        full: 'var(--radius-full)',
      },
      boxShadow: {
        sm: 'var(--shadow-sm)',
        md: 'var(--shadow-md)',
        lg: 'var(--shadow-lg)',
        xl: 'var(--shadow-xl)',
        accent: 'var(--shadow-accent)',
      },
    },
  },
  plugins: [],
};

export default config;
```

### CSS Modules Approach (alternative to Tailwind)

```css
/* Button.module.css */
.primary {
  background: var(--color-accent);
  color: var(--color-white);
  padding: var(--space-4) var(--space-8);
  border-radius: var(--radius-md);
  font-weight: 700;
  font-size: var(--text-body);
  box-shadow: var(--shadow-accent);
  transition: all var(--duration-normal) var(--ease-out);
  border: none;
  cursor: pointer;
}
.primary:hover {
  background: var(--color-accent-hover);
  transform: translateY(-2px);
  box-shadow: var(--shadow-lg);
}
```

### Utility: Class Name Merging
```ts
// lib/cn.ts
export function cn(...classes: (string | false | null | undefined)[]): string {
  return classes.filter(Boolean).join(' ');
}
```

---

## Component Patterns

### Atoms

#### Button
```tsx
// components/atoms/Button.tsx
import { type ButtonHTMLAttributes, forwardRef } from 'react';
import styles from './Button.module.css';
import { cn } from '@/lib/cn';

type ButtonVariant = 'primary' | 'secondary' | 'ghost';
type ButtonSize = 'sm' | 'md' | 'lg';

interface ButtonProps extends ButtonHTMLAttributes<HTMLButtonElement> {
  variant?: ButtonVariant;
  size?: ButtonSize;
}

const Button = forwardRef<HTMLButtonElement, ButtonProps>(
  ({ variant = 'primary', size = 'md', className, children, ...props }, ref) => {
    return (
      <button
        ref={ref}
        className={cn(styles.base, styles[variant], styles[size], className)}
        {...props}
      >
        {children}
      </button>
    );
  }
);

Button.displayName = 'Button';
export default Button;
```

```css
/* components/atoms/Button.module.css */
.base {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-2);
  font-family: var(--font-body);
  font-weight: 700;
  border: none;
  cursor: pointer;
  transition: all var(--duration-normal) var(--ease-out);
  text-decoration: none;
  line-height: 1;
}

.primary {
  background: var(--color-accent);
  color: var(--color-white);
  border-radius: var(--radius-md);
  box-shadow: var(--shadow-accent);
}
.primary:hover {
  background: var(--color-accent-hover);
  transform: translateY(-2px);
  box-shadow: var(--shadow-lg);
}

.secondary {
  background: transparent;
  color: var(--color-on-surface);
  border: 2px solid var(--color-base-100);
  border-radius: var(--radius-md);
}
.secondary:hover {
  border-color: var(--color-accent);
  color: var(--color-accent);
  transform: translateY(-2px);
}

.ghost {
  background: transparent;
  color: var(--color-accent);
  border-radius: var(--radius-md);
}
.ghost:hover {
  background: var(--color-accent-subtle);
}

.sm { padding: var(--space-2) var(--space-4); font-size: var(--text-small); }
.md { padding: var(--space-4) var(--space-8); font-size: var(--text-body); }
.lg { padding: var(--space-4) var(--space-12); font-size: var(--text-body); }
```

#### Badge
```tsx
// components/atoms/Badge.tsx
import styles from './Badge.module.css';
import { cn } from '@/lib/cn';

interface BadgeProps {
  children: React.ReactNode;
  className?: string;
}

export default function Badge({ children, className }: BadgeProps) {
  return (
    <span className={cn(styles.badge, className)}>
      {children}
    </span>
  );
}
```

```css
/* components/atoms/Badge.module.css */
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

#### Heading
```tsx
// components/atoms/Heading.tsx
import styles from './Heading.module.css';
import { cn } from '@/lib/cn';

type HeadingLevel = 1 | 2 | 3 | 4 | 5 | 6;

interface HeadingProps {
  level: HeadingLevel;
  as?: HeadingLevel;
  children: React.ReactNode;
  className?: string;
}

export default function Heading({ level, as, children, className }: HeadingProps) {
  const Tag = `h${as ?? level}` as keyof JSX.IntrinsicElements;
  return <Tag className={cn(styles[`h${level}`], className)}>{children}</Tag>;
}
```

```css
/* components/atoms/Heading.module.css */
.h1 {
  font-family: var(--font-display);
  font-size: var(--text-h1);
  font-weight: 800;
  line-height: var(--leading-tight);
  letter-spacing: var(--tracking-tight);
  color: var(--color-on-surface);
}
.h2 {
  font-family: var(--font-display);
  font-size: var(--text-h2);
  font-weight: 700;
  line-height: var(--leading-tight);
  letter-spacing: var(--tracking-tight);
  color: var(--color-on-surface);
}
.h3 {
  font-family: var(--font-display);
  font-size: var(--text-h3);
  font-weight: 700;
  line-height: var(--leading-tight);
  color: var(--color-on-surface);
}
.h4, .h5, .h6 {
  font-family: var(--font-display);
  font-size: var(--text-body);
  font-weight: 600;
  line-height: var(--leading-tight);
  color: var(--color-on-surface);
}
```

#### Text
```tsx
// components/atoms/Text.tsx
import styles from './Text.module.css';
import { cn } from '@/lib/cn';

type TextVariant = 'body' | 'caption' | 'label';

interface TextProps {
  variant?: TextVariant;
  muted?: boolean;
  children: React.ReactNode;
  className?: string;
}

export default function Text({ variant = 'body', muted = false, children, className }: TextProps) {
  return (
    <p className={cn(styles[variant], muted && styles.muted, className)}>
      {children}
    </p>
  );
}
```

```css
/* components/atoms/Text.module.css */
.body {
  font-family: var(--font-body);
  font-size: var(--text-body);
  line-height: var(--leading-normal);
  color: var(--color-on-surface);
}
.caption {
  font-family: var(--font-body);
  font-size: var(--text-caption);
  line-height: var(--leading-normal);
  color: var(--color-on-surface-muted);
}
.label {
  font-family: var(--font-body);
  font-size: var(--text-caption);
  font-weight: 600;
  letter-spacing: var(--tracking-widest);
  text-transform: uppercase;
  color: var(--color-on-surface-muted);
}
.muted { color: var(--color-on-surface-muted); }
```

#### Input
```tsx
// components/atoms/Input.tsx
import { type InputHTMLAttributes, forwardRef } from 'react';
import styles from './Input.module.css';
import { cn } from '@/lib/cn';

interface InputProps extends InputHTMLAttributes<HTMLInputElement> {
  label?: string;
  error?: string;
}

const Input = forwardRef<HTMLInputElement, InputProps>(
  ({ label, error, className, id, ...props }, ref) => {
    const inputId = id ?? label?.toLowerCase().replace(/\s+/g, '-');
    return (
      <div className={styles.wrapper}>
        {label && <label htmlFor={inputId} className={styles.label}>{label}</label>}
        <input
          ref={ref}
          id={inputId}
          className={cn(styles.input, error && styles.error, className)}
          aria-invalid={error ? 'true' : undefined}
          aria-describedby={error ? `${inputId}-error` : undefined}
          {...props}
        />
        {error && <span id={`${inputId}-error`} className={styles.errorText} role="alert">{error}</span>}
      </div>
    );
  }
);

Input.displayName = 'Input';
export default Input;
```

```css
/* components/atoms/Input.module.css */
.wrapper { display: flex; flex-direction: column; gap: var(--space-2); }
.label {
  font-size: var(--text-small);
  font-weight: 600;
  color: var(--color-on-surface);
}
.input {
  padding: var(--space-3) var(--space-4);
  border: 2px solid var(--color-base-100);
  border-radius: var(--radius-sm);
  font-size: var(--text-body);
  font-family: var(--font-body);
  background: var(--color-surface);
  color: var(--color-on-surface);
  transition: border-color var(--duration-fast) var(--ease-out);
  outline: none;
}
.input:focus {
  border-color: var(--color-accent);
  box-shadow: 0 0 0 3px var(--color-accent-subtle);
}
.error { border-color: oklch(0.55 0.25 25); }
.errorText { font-size: var(--text-small); color: oklch(0.55 0.25 25); }
```

#### LazyImage
```tsx
// components/atoms/LazyImage.tsx
import { useState, useRef, useEffect } from 'react';
import styles from './LazyImage.module.css';
import { cn } from '@/lib/cn';

interface LazyImageProps {
  src: string;
  alt: string;
  width: number;
  height: number;
  className?: string;
}

export default function LazyImage({ src, alt, width, height, className }: LazyImageProps) {
  const [loaded, setLoaded] = useState(false);
  const imgRef = useRef<HTMLImageElement>(null);

  useEffect(() => {
    const img = imgRef.current;
    if (!img) return;

    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          img.src = img.dataset.src!;
          observer.disconnect();
        }
      },
      { rootMargin: '200px' }
    );

    observer.observe(img);
    return () => observer.disconnect();
  }, []);

  return (
    <img
      ref={imgRef}
      data-src={src}
      alt={alt}
      width={width}
      height={height}
      onLoad={() => setLoaded(true)}
      className={cn(styles.image, loaded && styles.loaded, className)}
      style={{ aspectRatio: `${width} / ${height}` }}
    />
  );
}
```

```css
/* components/atoms/LazyImage.module.css */
.image {
  display: block;
  max-width: 100%;
  height: auto;
  opacity: 0;
  transition: opacity var(--duration-slow) var(--ease-out);
  object-fit: cover;
}
.loaded { opacity: 1; }
```

> **Next.js note:** When using Next.js, prefer the built-in `next/image` component over `LazyImage`. It handles lazy loading, responsive sizing, and format optimization automatically.

---

### Molecules

#### FeatureCard
```tsx
// components/molecules/FeatureCard.tsx
import Heading from '@/components/atoms/Heading';
import Text from '@/components/atoms/Text';
import styles from './FeatureCard.module.css';
import { cn } from '@/lib/cn';

interface FeatureCardProps {
  icon: React.ReactNode;
  title: string;
  description: string;
  className?: string;
}

export default function FeatureCard({ icon, title, description, className }: FeatureCardProps) {
  return (
    <article className={cn(styles.card, className)}>
      <div className={styles.icon}>{icon}</div>
      <Heading level={3}>{title}</Heading>
      <Text muted>{description}</Text>
    </article>
  );
}
```

```css
/* components/molecules/FeatureCard.module.css */
.card {
  background: var(--color-surface);
  border-radius: var(--radius-lg);
  padding: var(--space-8);
  box-shadow: var(--shadow-md);
  border: 1px solid oklch(0 0 0 / 0.05);
  transition: all var(--duration-normal) var(--ease-out);
  display: flex;
  flex-direction: column;
  gap: var(--space-4);
}
.card:hover {
  transform: translateY(-4px);
  box-shadow: var(--shadow-lg);
}
.icon {
  width: 48px;
  height: 48px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: var(--radius-md);
  background: var(--color-accent-subtle);
  color: var(--color-accent);
  font-size: 1.5rem;
}
```

#### TestimonialCard
```tsx
// components/molecules/TestimonialCard.tsx
import Text from '@/components/atoms/Text';
import styles from './TestimonialCard.module.css';

interface TestimonialCardProps {
  quote: string;
  author: string;
  role: string;
  avatarUrl?: string;
}

export default function TestimonialCard({ quote, author, role, avatarUrl }: TestimonialCardProps) {
  return (
    <blockquote className={styles.card}>
      <Text className={styles.quote}>&ldquo;{quote}&rdquo;</Text>
      <footer className={styles.footer}>
        {avatarUrl && (
          <img src={avatarUrl} alt={author} className={styles.avatar} width={40} height={40} />
        )}
        <div>
          <strong className={styles.author}>{author}</strong>
          <Text variant="caption">{role}</Text>
        </div>
      </footer>
    </blockquote>
  );
}
```

```css
/* components/molecules/TestimonialCard.module.css */
.card {
  background: var(--color-surface);
  border-radius: var(--radius-lg);
  padding: var(--space-8);
  box-shadow: var(--shadow-md);
  border: 1px solid oklch(0 0 0 / 0.05);
  display: flex;
  flex-direction: column;
  gap: var(--space-6);
  margin: 0;
}
.quote {
  font-size: var(--text-body);
  line-height: var(--leading-relaxed);
  font-style: italic;
}
.footer { display: flex; align-items: center; gap: var(--space-3); }
.avatar {
  width: 40px;
  height: 40px;
  border-radius: var(--radius-full);
  object-fit: cover;
}
.author {
  font-size: var(--text-small);
  font-weight: 700;
  color: var(--color-on-surface);
  display: block;
}
```

#### PricingCard
```tsx
// components/molecules/PricingCard.tsx
import Heading from '@/components/atoms/Heading';
import Text from '@/components/atoms/Text';
import Badge from '@/components/atoms/Badge';
import Button from '@/components/atoms/Button';
import styles from './PricingCard.module.css';
import { cn } from '@/lib/cn';

interface PricingCardProps {
  name: string;
  price: string;
  period?: string;
  description: string;
  features: string[];
  cta: string;
  highlighted?: boolean;
  badge?: string;
  onCtaClick?: () => void;
}

export default function PricingCard({
  name, price, period = '/mo', description, features, cta,
  highlighted = false, badge, onCtaClick,
}: PricingCardProps) {
  return (
    <article className={cn(styles.card, highlighted && styles.highlighted)}>
      {badge && <Badge className={styles.badge}>{badge}</Badge>}
      <Heading level={3}>{name}</Heading>
      <div className={styles.price}>
        <span className={styles.amount}>{price}</span>
        {period && <span className={styles.period}>{period}</span>}
      </div>
      <Text muted>{description}</Text>
      <ul className={styles.features}>
        {features.map((feature) => (
          <li key={feature} className={styles.feature}>
            <span className={styles.check} aria-hidden="true">&#10003;</span>
            {feature}
          </li>
        ))}
      </ul>
      <Button
        variant={highlighted ? 'primary' : 'secondary'}
        onClick={onCtaClick}
        className={styles.cta}
      >
        {cta}
      </Button>
    </article>
  );
}
```

```css
/* components/molecules/PricingCard.module.css */
.card {
  background: var(--color-surface);
  border-radius: var(--radius-lg);
  padding: var(--space-8);
  box-shadow: var(--shadow-md);
  border: 1px solid oklch(0 0 0 / 0.05);
  display: flex;
  flex-direction: column;
  gap: var(--space-4);
  position: relative;
  transition: all var(--duration-normal) var(--ease-out);
}
.highlighted {
  border-color: var(--color-accent);
  box-shadow: var(--shadow-lg);
  transform: scale(1.03);
}
.badge { position: absolute; top: calc(-1 * var(--space-3)); right: var(--space-6); }
.price { display: flex; align-items: baseline; gap: var(--space-1); }
.amount {
  font-family: var(--font-display);
  font-size: var(--text-h1);
  font-weight: 800;
  color: var(--color-on-surface);
}
.period { font-size: var(--text-small); color: var(--color-on-surface-muted); }
.features {
  list-style: none;
  padding: 0;
  margin: var(--space-4) 0;
  display: flex;
  flex-direction: column;
  gap: var(--space-3);
  flex: 1;
}
.feature {
  display: flex;
  align-items: center;
  gap: var(--space-2);
  font-size: var(--text-body);
  color: var(--color-on-surface);
}
.check { color: var(--color-success); font-weight: 700; }
.cta { width: 100%; margin-top: auto; }
```

#### StatCounter (with animated number)
```tsx
// components/molecules/StatCounter.tsx
import { useCountUp } from '@/hooks/useCountUp';
import Text from '@/components/atoms/Text';
import styles from './StatCounter.module.css';

interface StatCounterProps {
  value: number;
  suffix?: string;
  prefix?: string;
  label: string;
}

export default function StatCounter({ value, suffix = '', prefix = '', label }: StatCounterProps) {
  const { ref, count } = useCountUp(value);

  return (
    <div ref={ref} className={styles.stat}>
      <span className={styles.value}>
        {prefix}{count.toLocaleString()}{suffix}
      </span>
      <Text variant="caption" muted>{label}</Text>
    </div>
  );
}
```

```css
/* components/molecules/StatCounter.module.css */
.stat {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--space-2);
  text-align: center;
}
.value {
  font-family: var(--font-display);
  font-size: var(--text-h1);
  font-weight: 800;
  color: var(--color-accent);
  line-height: 1;
}
```

#### CTAGroup
```tsx
// components/molecules/CTAGroup.tsx
import Button from '@/components/atoms/Button';
import styles from './CTAGroup.module.css';
import { cn } from '@/lib/cn';

interface CTAGroupProps {
  primaryLabel: string;
  primaryHref?: string;
  secondaryLabel?: string;
  secondaryHref?: string;
  onPrimaryClick?: () => void;
  onSecondaryClick?: () => void;
  className?: string;
}

export default function CTAGroup({
  primaryLabel, primaryHref, secondaryLabel, secondaryHref,
  onPrimaryClick, onSecondaryClick, className,
}: CTAGroupProps) {
  return (
    <div className={cn(styles.group, className)}>
      {primaryHref ? (
        <a href={primaryHref}><Button variant="primary" size="lg">{primaryLabel}</Button></a>
      ) : (
        <Button variant="primary" size="lg" onClick={onPrimaryClick}>{primaryLabel}</Button>
      )}
      {secondaryLabel && (
        secondaryHref ? (
          <a href={secondaryHref}><Button variant="secondary" size="lg">{secondaryLabel}</Button></a>
        ) : (
          <Button variant="secondary" size="lg" onClick={onSecondaryClick}>{secondaryLabel}</Button>
        )
      )}
    </div>
  );
}
```

```css
/* components/molecules/CTAGroup.module.css */
.group {
  display: flex;
  align-items: center;
  gap: var(--space-4);
  flex-wrap: wrap;
}
```

---

### Organisms

#### Layout Primitives

```tsx
// components/ui/Container.tsx
import styles from './Container.module.css';
import { cn } from '@/lib/cn';

interface ContainerProps {
  narrow?: boolean;
  children: React.ReactNode;
  className?: string;
}

export default function Container({ narrow = false, children, className }: ContainerProps) {
  return (
    <div className={cn(styles.container, narrow && styles.narrow, className)}>
      {children}
    </div>
  );
}
```

```css
/* components/ui/Container.module.css */
.container {
  max-width: var(--container-max);
  margin: 0 auto;
  padding: 0 var(--section-px);
}
.narrow { max-width: var(--container-narrow); }
```

```tsx
// components/ui/Section.tsx
import styles from './Section.module.css';
import { cn } from '@/lib/cn';

type SectionBackground = 'default' | 'alt' | 'dark';

interface SectionProps {
  bg?: SectionBackground;
  id?: string;
  children: React.ReactNode;
  className?: string;
}

export default function Section({ bg = 'default', id, children, className }: SectionProps) {
  return (
    <section id={id} className={cn(styles.section, styles[bg], className)}>
      {children}
    </section>
  );
}
```

```css
/* components/ui/Section.module.css */
.section {
  padding: var(--section-py) 0;
}
.default { background: var(--color-surface); color: var(--color-on-surface); }
.alt { background: var(--color-surface-alt); color: var(--color-on-surface); }
.dark { background: var(--color-surface-dark); color: var(--color-on-dark); }
```

#### Navbar
```tsx
// components/organisms/Navbar.tsx
import { useState } from 'react';
import Button from '@/components/atoms/Button';
import Container from '@/components/ui/Container';
import styles from './Navbar.module.css';
import { cn } from '@/lib/cn';

interface NavLink {
  label: string;
  href: string;
}

interface NavbarProps {
  logo: React.ReactNode;
  links: NavLink[];
  ctaLabel?: string;
  ctaHref?: string;
}

export default function Navbar({ logo, links, ctaLabel, ctaHref }: NavbarProps) {
  const [open, setOpen] = useState(false);

  return (
    <header className={styles.header}>
      <Container>
        <nav className={styles.nav} aria-label="Main navigation">
          <div className={styles.logo}>{logo}</div>

          <button
            className={styles.toggle}
            onClick={() => setOpen(!open)}
            aria-expanded={open}
            aria-label="Toggle menu"
          >
            <span className={cn(styles.bar, open && styles.open)} />
          </button>

          <div className={cn(styles.menu, open && styles.menuOpen)}>
            <ul className={styles.links}>
              {links.map(({ label, href }) => (
                <li key={href}>
                  <a href={href} className={styles.link}>{label}</a>
                </li>
              ))}
            </ul>
            {ctaLabel && ctaHref && (
              <a href={ctaHref}>
                <Button variant="primary" size="sm">{ctaLabel}</Button>
              </a>
            )}
          </div>
        </nav>
      </Container>
    </header>
  );
}
```

```css
/* components/organisms/Navbar.module.css */
.header {
  position: sticky;
  top: 0;
  z-index: 100;
  background: oklch(1 0 0 / 0.85);
  backdrop-filter: blur(12px);
  border-bottom: 1px solid oklch(0 0 0 / 0.05);
}
.nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 64px;
}
.logo { font-weight: 800; font-size: var(--text-h3); }
.menu { display: flex; align-items: center; gap: var(--space-8); }
.links {
  display: flex;
  list-style: none;
  gap: var(--space-6);
  margin: 0;
  padding: 0;
}
.link {
  font-size: var(--text-small);
  font-weight: 500;
  color: var(--color-on-surface-muted);
  text-decoration: none;
  transition: color var(--duration-fast) var(--ease-out);
}
.link:hover { color: var(--color-accent); }
.toggle {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
  padding: var(--space-2);
}
.bar {
  display: block;
  width: 24px;
  height: 2px;
  background: var(--color-on-surface);
  position: relative;
  transition: background var(--duration-fast);
}
.bar::before, .bar::after {
  content: '';
  display: block;
  width: 24px;
  height: 2px;
  background: var(--color-on-surface);
  position: absolute;
  transition: transform var(--duration-normal) var(--ease-out);
}
.bar::before { top: -7px; }
.bar::after { top: 7px; }
.open { background: transparent; }
.open::before { transform: rotate(45deg) translate(5px, 5px); }
.open::after { transform: rotate(-45deg) translate(5px, -5px); }

@media (max-width: 768px) {
  .toggle { display: block; }
  .menu {
    display: none;
    position: absolute;
    top: 64px;
    left: 0;
    right: 0;
    flex-direction: column;
    background: var(--color-surface);
    padding: var(--space-6);
    border-bottom: 1px solid oklch(0 0 0 / 0.05);
    box-shadow: var(--shadow-lg);
  }
  .menuOpen { display: flex; }
  .links { flex-direction: column; align-items: center; }
}
```

#### HeroSection
```tsx
// components/organisms/HeroSection.tsx
import Section from '@/components/ui/Section';
import Container from '@/components/ui/Container';
import Badge from '@/components/atoms/Badge';
import Heading from '@/components/atoms/Heading';
import Text from '@/components/atoms/Text';
import CTAGroup from '@/components/molecules/CTAGroup';
import styles from './HeroSection.module.css';

interface HeroSectionProps {
  badge?: string;
  title: string;
  subtitle: string;
  primaryCta: string;
  primaryHref: string;
  secondaryCta?: string;
  secondaryHref?: string;
  image?: React.ReactNode;
}

export default function HeroSection({
  badge, title, subtitle, primaryCta, primaryHref,
  secondaryCta, secondaryHref, image,
}: HeroSectionProps) {
  return (
    <Section bg="dark" className={styles.hero}>
      <Container>
        <div className={styles.grid}>
          <div className={styles.content}>
            {badge && <Badge>{badge}</Badge>}
            <h1 className={styles.title}>{title}</h1>
            <Text className={styles.subtitle}>{subtitle}</Text>
            <CTAGroup
              primaryLabel={primaryCta}
              primaryHref={primaryHref}
              secondaryLabel={secondaryCta}
              secondaryHref={secondaryHref}
            />
          </div>
          {image && <div className={styles.visual}>{image}</div>}
        </div>
      </Container>
    </Section>
  );
}
```

```css
/* components/organisms/HeroSection.module.css */
.hero { padding-top: var(--space-24); padding-bottom: var(--space-24); }
.grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: var(--space-12);
  align-items: center;
}
.content {
  display: flex;
  flex-direction: column;
  gap: var(--space-6);
}
.title {
  font-family: var(--font-display);
  font-size: var(--text-display);
  font-weight: 800;
  line-height: var(--leading-tight);
  letter-spacing: var(--tracking-tight);
  color: var(--color-on-dark);
  margin: 0;
}
.subtitle {
  font-size: var(--text-body);
  line-height: var(--leading-relaxed);
  color: var(--color-on-dark);
  opacity: 0.8;
  max-width: 540px;
}
.visual {
  display: flex;
  justify-content: center;
}

@media (min-width: 1024px) {
  .grid { grid-template-columns: 1.2fr 0.8fr; }
}
```

#### FeaturesGrid
```tsx
// components/organisms/FeaturesGrid.tsx
import Section from '@/components/ui/Section';
import Container from '@/components/ui/Container';
import Heading from '@/components/atoms/Heading';
import Text from '@/components/atoms/Text';
import FeatureCard from '@/components/molecules/FeatureCard';
import { useScrollReveal } from '@/hooks/useIntersectionObserver';
import styles from './FeaturesGrid.module.css';

interface Feature {
  icon: React.ReactNode;
  title: string;
  description: string;
}

interface FeaturesGridProps {
  badge?: string;
  title: string;
  subtitle?: string;
  features: Feature[];
}

export default function FeaturesGrid({ badge, title, subtitle, features }: FeaturesGridProps) {
  const { ref, isVisible } = useScrollReveal();

  return (
    <Section bg="alt" id="features">
      <Container>
        <div className={styles.header}>
          {badge && <span className={styles.badge}>{badge}</span>}
          <Heading level={2}>{title}</Heading>
          {subtitle && <Text muted>{subtitle}</Text>}
        </div>
        <div ref={ref} className={styles.grid}>
          {features.map((feature, i) => (
            <div
              key={feature.title}
              className={styles.item}
              style={{
                opacity: isVisible ? 1 : 0,
                transform: isVisible ? 'translateY(0)' : 'translateY(24px)',
                transition: `all var(--duration-slow) var(--ease-out)`,
                transitionDelay: `${i * 80}ms`,
              }}
            >
              <FeatureCard {...feature} />
            </div>
          ))}
        </div>
      </Container>
    </Section>
  );
}
```

```css
/* components/organisms/FeaturesGrid.module.css */
.header {
  text-align: center;
  max-width: var(--container-narrow);
  margin: 0 auto var(--space-12);
  display: flex;
  flex-direction: column;
  gap: var(--space-4);
}
.badge {
  display: inline-flex;
  align-self: center;
  padding: var(--space-1) var(--space-3);
  border-radius: var(--radius-full);
  font-size: var(--text-caption);
  font-weight: 600;
  letter-spacing: var(--tracking-wide);
  text-transform: uppercase;
  background: var(--color-accent-subtle);
  color: var(--color-accent);
}
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: var(--space-8);
}
.item { will-change: transform, opacity; }
```

#### FAQAccordion
```tsx
// components/organisms/FAQAccordion.tsx
import { useState, useId } from 'react';
import Section from '@/components/ui/Section';
import Container from '@/components/ui/Container';
import Heading from '@/components/atoms/Heading';
import styles from './FAQAccordion.module.css';

interface FAQItem {
  question: string;
  answer: string;
}

interface FAQAccordionProps {
  title: string;
  items: FAQItem[];
}

function FAQEntry({ question, answer }: FAQItem) {
  const [open, setOpen] = useState(false);
  const id = useId();

  return (
    <div className={styles.item}>
      <button
        className={styles.trigger}
        onClick={() => setOpen(!open)}
        aria-expanded={open}
        aria-controls={`${id}-panel`}
        id={`${id}-trigger`}
      >
        <span className={styles.question}>{question}</span>
        <span className={styles.icon} aria-hidden="true">{open ? '\u2212' : '+'}</span>
      </button>
      <div
        id={`${id}-panel`}
        role="region"
        aria-labelledby={`${id}-trigger`}
        className={styles.panel}
        style={{
          maxHeight: open ? '500px' : '0',
          opacity: open ? 1 : 0,
          paddingBottom: open ? 'var(--space-6)' : '0',
        }}
      >
        <p className={styles.answer}>{answer}</p>
      </div>
    </div>
  );
}

export default function FAQAccordion({ title, items }: FAQAccordionProps) {
  return (
    <Section bg="alt" id="faq">
      <Container narrow>
        <Heading level={2} className={styles.title}>{title}</Heading>
        <div className={styles.list}>
          {items.map((item) => (
            <FAQEntry key={item.question} {...item} />
          ))}
        </div>
      </Container>
    </Section>
  );
}
```

```css
/* components/organisms/FAQAccordion.module.css */
.title { text-align: center; margin-bottom: var(--space-12); }
.list {
  display: flex;
  flex-direction: column;
  gap: var(--space-2);
}
.item {
  border-bottom: 1px solid oklch(0 0 0 / 0.08);
}
.trigger {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: var(--space-6) 0;
  background: none;
  border: none;
  cursor: pointer;
  text-align: left;
}
.question {
  font-family: var(--font-display);
  font-size: var(--text-h3);
  font-weight: 600;
  color: var(--color-on-surface);
}
.icon {
  font-size: 1.5rem;
  color: var(--color-accent);
  flex-shrink: 0;
  margin-left: var(--space-4);
}
.panel {
  overflow: hidden;
  transition: max-height var(--duration-normal) var(--ease-out),
              opacity var(--duration-normal) var(--ease-out),
              padding-bottom var(--duration-normal) var(--ease-out);
}
.answer {
  font-size: var(--text-body);
  line-height: var(--leading-relaxed);
  color: var(--color-on-surface-muted);
  margin: 0;
}
```

#### CTASection
```tsx
// components/organisms/CTASection.tsx
import Section from '@/components/ui/Section';
import Container from '@/components/ui/Container';
import Heading from '@/components/atoms/Heading';
import Text from '@/components/atoms/Text';
import CTAGroup from '@/components/molecules/CTAGroup';
import styles from './CTASection.module.css';

interface CTASectionProps {
  title: string;
  subtitle: string;
  primaryLabel: string;
  primaryHref: string;
  secondaryLabel?: string;
  secondaryHref?: string;
}

export default function CTASection({
  title, subtitle, primaryLabel, primaryHref,
  secondaryLabel, secondaryHref,
}: CTASectionProps) {
  return (
    <Section bg="dark" className={styles.cta}>
      <Container narrow>
        <div className={styles.content}>
          <Heading level={2} className={styles.title}>{title}</Heading>
          <Text className={styles.subtitle}>{subtitle}</Text>
          <CTAGroup
            primaryLabel={primaryLabel}
            primaryHref={primaryHref}
            secondaryLabel={secondaryLabel}
            secondaryHref={secondaryHref}
            className={styles.actions}
          />
        </div>
      </Container>
    </Section>
  );
}
```

```css
/* components/organisms/CTASection.module.css */
.cta {
  background: linear-gradient(135deg, var(--color-base-900), var(--color-base-800));
}
.content {
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--space-6);
}
.title { color: var(--color-on-dark); }
.subtitle { color: var(--color-on-dark); opacity: 0.8; }
.actions { justify-content: center; }
```

#### Footer
```tsx
// components/organisms/Footer.tsx
import Container from '@/components/ui/Container';
import Text from '@/components/atoms/Text';
import styles from './Footer.module.css';

interface FooterLink {
  label: string;
  href: string;
}

interface FooterColumn {
  title: string;
  links: FooterLink[];
}

interface FooterProps {
  logo: React.ReactNode;
  columns: FooterColumn[];
  copyright: string;
}

export default function Footer({ logo, columns, copyright }: FooterProps) {
  return (
    <footer className={styles.footer}>
      <Container>
        <div className={styles.grid}>
          <div className={styles.brand}>{logo}</div>
          {columns.map((col) => (
            <nav key={col.title} className={styles.column} aria-label={col.title}>
              <h4 className={styles.columnTitle}>{col.title}</h4>
              <ul className={styles.links}>
                {col.links.map(({ label, href }) => (
                  <li key={href}>
                    <a href={href} className={styles.link}>{label}</a>
                  </li>
                ))}
              </ul>
            </nav>
          ))}
        </div>
        <div className={styles.bottom}>
          <Text variant="caption" muted>{copyright}</Text>
        </div>
      </Container>
    </footer>
  );
}
```

```css
/* components/organisms/Footer.module.css */
.footer {
  background: var(--color-base-900);
  padding: var(--space-16) 0 var(--space-8);
  color: var(--color-on-dark);
}
.grid {
  display: grid;
  grid-template-columns: 1.5fr repeat(auto-fit, minmax(150px, 1fr));
  gap: var(--space-12);
  margin-bottom: var(--space-12);
}
.brand { font-weight: 800; font-size: var(--text-h3); }
.columnTitle {
  font-size: var(--text-small);
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: var(--tracking-widest);
  margin: 0 0 var(--space-4);
  color: var(--color-on-dark);
}
.links { list-style: none; padding: 0; margin: 0; display: flex; flex-direction: column; gap: var(--space-3); }
.link {
  font-size: var(--text-small);
  color: var(--color-on-dark);
  opacity: 0.6;
  text-decoration: none;
  transition: opacity var(--duration-fast);
}
.link:hover { opacity: 1; }
.bottom {
  border-top: 1px solid oklch(1 0 0 / 0.1);
  padding-top: var(--space-8);
  text-align: center;
}

@media (max-width: 768px) {
  .grid { grid-template-columns: 1fr 1fr; }
  .brand { grid-column: 1 / -1; }
}
```

---

## Custom Hooks

### useIntersectionObserver (scroll reveals)
```ts
// hooks/useIntersectionObserver.ts
import { useRef, useState, useEffect, type RefObject } from 'react';

interface UseScrollRevealOptions {
  threshold?: number;
  rootMargin?: string;
  triggerOnce?: boolean;
}

export function useScrollReveal<T extends HTMLElement = HTMLDivElement>(
  options: UseScrollRevealOptions = {}
): { ref: RefObject<T | null>; isVisible: boolean } {
  const { threshold = 0.15, rootMargin = '0px', triggerOnce = true } = options;
  const ref = useRef<T>(null);
  const [isVisible, setIsVisible] = useState(false);

  useEffect(() => {
    const el = ref.current;
    if (!el) return;

    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          setIsVisible(true);
          if (triggerOnce) observer.disconnect();
        } else if (!triggerOnce) {
          setIsVisible(false);
        }
      },
      { threshold, rootMargin }
    );

    observer.observe(el);
    return () => observer.disconnect();
  }, [threshold, rootMargin, triggerOnce]);

  return { ref, isVisible };
}
```

### useCountUp (animated numbers)
```ts
// hooks/useCountUp.ts
import { useRef, useState, useEffect, type RefObject } from 'react';
import { useScrollReveal } from './useIntersectionObserver';

interface UseCountUpResult {
  ref: RefObject<HTMLDivElement | null>;
  count: number;
}

export function useCountUp(target: number, duration = 2000): UseCountUpResult {
  const { ref, isVisible } = useScrollReveal<HTMLDivElement>();
  const [count, setCount] = useState(0);
  const hasAnimated = useRef(false);

  useEffect(() => {
    if (!isVisible || hasAnimated.current) return;
    hasAnimated.current = true;

    const startTime = performance.now();

    function animate(now: number) {
      const elapsed = now - startTime;
      const progress = Math.min(elapsed / duration, 1);
      // Ease-out quad
      const eased = 1 - (1 - progress) * (1 - progress);
      setCount(Math.round(eased * target));

      if (progress < 1) {
        requestAnimationFrame(animate);
      }
    }

    requestAnimationFrame(animate);
  }, [isVisible, target, duration]);

  return { ref, count };
}
```

### useMediaQuery (responsive hooks)
```ts
// hooks/useMediaQuery.ts
import { useState, useEffect } from 'react';

export function useMediaQuery(query: string): boolean {
  const [matches, setMatches] = useState(false);

  useEffect(() => {
    const mql = window.matchMedia(query);
    setMatches(mql.matches);

    function onChange(e: MediaQueryListEvent) {
      setMatches(e.matches);
    }

    mql.addEventListener('change', onChange);
    return () => mql.removeEventListener('change', onChange);
  }, [query]);

  return matches;
}

// Convenience hooks using the same breakpoints as CSS
export const useIsMobile = () => useMediaQuery('(max-width: 767px)');
export const useIsTablet = () => useMediaQuery('(min-width: 768px) and (max-width: 1023px)');
export const useIsDesktop = () => useMediaQuery('(min-width: 1024px)');
```

---

## Animation Patterns

### CSS-Only Animations (default, no dependencies)

```css
/* globals.css — add to design tokens file */

/* Scroll reveal base */
.reveal {
  opacity: 0;
  transform: translateY(24px);
  transition:
    opacity var(--duration-slow) var(--ease-out),
    transform var(--duration-slow) var(--ease-out);
}
.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}

/* Stagger children */
.stagger > * {
  transition-delay: calc(var(--index, 0) * 80ms);
}

/* Reduced motion */
@media (prefers-reduced-motion: reduce) {
  .reveal,
  .reveal.visible {
    transition: none;
    opacity: 1;
    transform: none;
  }
}
```

### React component for scroll reveal
```tsx
// components/ui/Reveal.tsx
import { useScrollReveal } from '@/hooks/useIntersectionObserver';
import { cn } from '@/lib/cn';
import styles from './Reveal.module.css';

interface RevealProps {
  children: React.ReactNode;
  className?: string;
  delay?: number;
}

export default function Reveal({ children, className, delay = 0 }: RevealProps) {
  const { ref, isVisible } = useScrollReveal();

  return (
    <div
      ref={ref}
      className={cn(styles.reveal, isVisible && styles.visible, className)}
      style={{ transitionDelay: `${delay}ms` }}
    >
      {children}
    </div>
  );
}
```

```css
/* components/ui/Reveal.module.css */
.reveal {
  opacity: 0;
  transform: translateY(24px);
  transition:
    opacity var(--duration-slow) var(--ease-out),
    transform var(--duration-slow) var(--ease-out);
  will-change: transform, opacity;
}
.visible {
  opacity: 1;
  transform: translateY(0);
}

@media (prefers-reduced-motion: reduce) {
  .reveal {
    opacity: 1;
    transform: none;
    transition: none;
  }
}
```

### Framer Motion (optional, for complex animations)

Only add `framer-motion` when CSS-only is insufficient (e.g., layout animations, gesture-based, exit animations).

```tsx
// Example: stagger list with Framer Motion
import { motion } from 'framer-motion';

const container = {
  hidden: {},
  show: { transition: { staggerChildren: 0.08 } },
};

const item = {
  hidden: { opacity: 0, y: 24 },
  show: { opacity: 1, y: 0, transition: { duration: 0.4, ease: [0.16, 1, 0.3, 1] } },
};

function AnimatedList({ children }: { children: React.ReactNode[] }) {
  return (
    <motion.div variants={container} initial="hidden" whileInView="show" viewport={{ once: true, margin: '-50px' }}>
      {children.map((child, i) => (
        <motion.div key={i} variants={item}>{child}</motion.div>
      ))}
    </motion.div>
  );
}
```

### Animation Rules
- Only animate `opacity` and `transform` — never width, height, margin, or padding
- Use `will-change: transform, opacity` on animated elements
- ALWAYS respect `prefers-reduced-motion`
- CSS-only is the default; reach for Framer Motion only when needed
- Stagger delay: 60-100ms per item, cap at ~400ms total
- Scroll reveal threshold: 10-20% visibility before triggering

---

## Performance

### Image Strategy

**Next.js:**
```tsx
import Image from 'next/image';

<Image
  src="/hero-visual.webp"
  alt="Product screenshot"
  width={800}
  height={600}
  priority                        // for above-the-fold
  sizes="(max-width: 768px) 100vw, 50vw"
/>
```

**Vite + React:**
Use the `LazyImage` atom defined above, or a simple native approach:
```tsx
<img
  src="/hero.webp"
  alt="Product screenshot"
  width={800}
  height={600}
  loading="lazy"
  decoding="async"
  style={{ aspectRatio: '800 / 600' }}
/>
```

### Code Splitting
```tsx
import { lazy, Suspense } from 'react';

// Split heavy below-the-fold sections
const PricingSection = lazy(() => import('@/components/organisms/PricingSection'));
const TestimonialsSection = lazy(() => import('@/components/organisms/TestimonialsSection'));

function LandingPage() {
  return (
    <>
      <HeroSection {...heroProps} />
      <FeaturesGrid {...featuresProps} />
      <Suspense fallback={<div style={{ minHeight: '400px' }} />}>
        <PricingSection {...pricingProps} />
      </Suspense>
      <Suspense fallback={<div style={{ minHeight: '300px' }} />}>
        <TestimonialsSection {...testimonialsProps} />
      </Suspense>
      <CTASection {...ctaProps} />
    </>
  );
}
```

### Font Loading

**Next.js (built-in):**
```tsx
// app/layout.tsx
import { Inter, Plus_Jakarta_Sans } from 'next/font/google';

const inter = Inter({ subsets: ['latin'], variable: '--font-body' });
const jakarta = Plus_Jakarta_Sans({ subsets: ['latin'], variable: '--font-display', weight: ['600', '700', '800'] });

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="pt-BR" className={`${inter.variable} ${jakarta.variable}`}>
      <body>{children}</body>
    </html>
  );
}
```

**Vite (manual):**
```html
<!-- index.html -->
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link
  href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&family=Plus+Jakarta+Sans:wght@600;700;800&display=swap"
  rel="stylesheet"
/>
```

### Static Export

**Next.js:**
```ts
// next.config.ts
const config = { output: 'export' };
export default config;
```

**Vite:** Runs `vite build` by default — output in `dist/`.

---

## Responsive Strategy

### Mobile-First Approach

All base styles target mobile. Use `min-width` media queries for larger screens:

```css
/* Base: mobile */
.grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: var(--space-6);
}

/* Tablet */
@media (min-width: 768px) {
  .grid { grid-template-columns: 1fr 1fr; gap: var(--space-8); }
}

/* Desktop */
@media (min-width: 1024px) {
  .grid { grid-template-columns: repeat(3, 1fr); gap: var(--space-12); }
}
```

### Container Component Pattern
```tsx
// Already defined above — use <Container> and <Container narrow> everywhere
// Never set max-width or horizontal padding on individual sections
```

### Responsive Component Example
```tsx
import { useIsMobile } from '@/hooks/useMediaQuery';

function TestimonialsSection({ testimonials }: { testimonials: Testimonial[] }) {
  const isMobile = useIsMobile();

  return (
    <Section bg="default">
      <Container>
        <div className={styles.grid}>
          {testimonials.slice(0, isMobile ? 2 : 6).map((t) => (
            <TestimonialCard key={t.author} {...t} />
          ))}
        </div>
      </Container>
    </Section>
  );
}
```

### Touch Targets
- Minimum 44x44px for all interactive elements on mobile
- Use padding rather than fixed dimensions to achieve this
- Apply `min-height: 44px; min-width: 44px` on clickable atoms

---

## SEO

### Meta Tags

**Next.js (app router):**
```tsx
// app/layout.tsx
import type { Metadata } from 'next';

export const metadata: Metadata = {
  title: 'Product Name — Tagline',
  description: 'Clear value proposition in 150-160 characters.',
  openGraph: {
    title: 'Product Name — Tagline',
    description: 'Clear value proposition.',
    url: 'https://example.com',
    siteName: 'Product Name',
    images: [{ url: '/og-image.png', width: 1200, height: 630, alt: 'Product preview' }],
    type: 'website',
    locale: 'pt_BR',
  },
  twitter: {
    card: 'summary_large_image',
    title: 'Product Name — Tagline',
    description: 'Clear value proposition.',
    images: ['/og-image.png'],
  },
  robots: { index: true, follow: true },
  alternates: { canonical: 'https://example.com' },
};
```

**Vite + react-helmet-async:**
```tsx
import { Helmet } from 'react-helmet-async';

function SEO({ title, description, url, image }: SEOProps) {
  return (
    <Helmet>
      <title>{title}</title>
      <meta name="description" content={description} />
      <link rel="canonical" href={url} />
      <meta property="og:title" content={title} />
      <meta property="og:description" content={description} />
      <meta property="og:url" content={url} />
      <meta property="og:image" content={image} />
      <meta property="og:type" content="website" />
      <meta name="twitter:card" content="summary_large_image" />
      <meta name="twitter:title" content={title} />
      <meta name="twitter:description" content={description} />
      <meta name="twitter:image" content={image} />
    </Helmet>
  );
}
```

### Structured Data (JSON-LD)
```tsx
// components/ui/JsonLd.tsx
interface JsonLdProps {
  data: Record<string, unknown>;
}

export default function JsonLd({ data }: JsonLdProps) {
  return (
    <script
      type="application/ld+json"
      dangerouslySetInnerHTML={{ __html: JSON.stringify(data) }}
    />
  );
}

// Usage in page:
<JsonLd data={{
  '@context': 'https://schema.org',
  '@type': 'SoftwareApplication',
  name: 'Product Name',
  description: 'Product description.',
  url: 'https://example.com',
  applicationCategory: 'BusinessApplication',
  offers: {
    '@type': 'Offer',
    price: '29',
    priceCurrency: 'USD',
  },
}} />
```

### Semantic HTML in JSX
- Use `<header>`, `<main>`, `<section>`, `<article>`, `<footer>` in organisms
- Single `<h1>` per page (in HeroSection)
- Sequential heading hierarchy: h1 -> h2 -> h3
- Use `<nav>` with `aria-label` for navigation blocks
- Use `<blockquote>` for testimonials

---

## Full Page Assembly Example

```tsx
// app/page.tsx (Next.js) or src/App.tsx (Vite)
import Navbar from '@/components/organisms/Navbar';
import HeroSection from '@/components/organisms/HeroSection';
import FeaturesGrid from '@/components/organisms/FeaturesGrid';
import FAQAccordion from '@/components/organisms/FAQAccordion';
import CTASection from '@/components/organisms/CTASection';
import Footer from '@/components/organisms/Footer';
import JsonLd from '@/components/ui/JsonLd';

const NAV_LINKS = [
  { label: 'Features', href: '#features' },
  { label: 'Pricing', href: '#pricing' },
  { label: 'FAQ', href: '#faq' },
];

export default function LandingPage() {
  return (
    <>
      <JsonLd data={{ '@context': 'https://schema.org', '@type': 'WebSite', name: 'Product' }} />

      <a href="#main-content" className="sr-only focus:not-sr-only">
        Skip to content
      </a>

      <Navbar
        logo={<span>Product</span>}
        links={NAV_LINKS}
        ctaLabel="Get Started"
        ctaHref="#pricing"
      />

      <main id="main-content">
        <HeroSection
          badge="Now in Beta"
          title="The headline that hooks visitors"
          subtitle="A clear explanation of the value you deliver, in one or two sentences."
          primaryCta="Start Free Trial"
          primaryHref="/signup"
          secondaryCta="Watch Demo"
          secondaryHref="#demo"
        />

        <FeaturesGrid
          badge="Features"
          title="Everything you need"
          subtitle="Short supporting text that reinforces the value proposition."
          features={[
            { icon: <span>&#9889;</span>, title: 'Fast', description: 'Lightning-fast performance.' },
            { icon: <span>&#128274;</span>, title: 'Secure', description: 'Enterprise-grade security.' },
            { icon: <span>&#9881;</span>, title: 'Flexible', description: 'Customize everything.' },
          ]}
        />

        <FAQAccordion
          title="Frequently Asked Questions"
          items={[
            { question: 'How does it work?', answer: 'Clear, concise answer.' },
            { question: 'What does it cost?', answer: 'Transparent pricing details.' },
          ]}
        />

        <CTASection
          title="Ready to get started?"
          subtitle="Join thousands of teams already using Product."
          primaryLabel="Start Free"
          primaryHref="/signup"
          secondaryLabel="Talk to Sales"
          secondaryHref="/contact"
        />
      </main>

      <Footer
        logo={<span>Product</span>}
        columns={[
          { title: 'Product', links: [{ label: 'Features', href: '#features' }, { label: 'Pricing', href: '#pricing' }] },
          { title: 'Company', links: [{ label: 'About', href: '/about' }, { label: 'Blog', href: '/blog' }] },
        ]}
        copyright={`\u00A9 ${new Date().getFullYear()} Product. All rights reserved.`}
      />
    </>
  );
}
```

### Section Rhythm

Follow the same alternating density pattern as the HTML version:

```
[HERO — dark background, dense, above-the-fold]
[PROBLEM — light (alt), spacious, breathing room]
[SOLUTION — default surface, medium density, alternating columns]
[FEATURES — alt surface, grid layout]
[TESTIMONIALS/PROOF — dark, full-bleed, contrasting]
[PRICING — default surface, card grid]
[FAQ — alt surface, accordion]
[CTA — dark, gradient, dense]
[FOOTER — darkest, links grid]
```

---

## Quality Checklist

Before finalizing any React landing page:

### Design System
- [ ] All values use CSS custom properties (zero hardcoded colors, spacing, or font sizes)
- [ ] Design tokens match the HTML landing-page best practices exactly
- [ ] Typography uses `clamp()` for fluid sizing
- [ ] Shadows are multi-layered (min 2 layers)
- [ ] Whitespace between sections is generous (80-128px via `--section-py`)
- [ ] Max 3 color families used (base + surface + accent)

### Components
- [ ] Components follow Atomic Design (atoms, molecules, organisms)
- [ ] All components are typed with TypeScript interfaces
- [ ] `forwardRef` used on interactive atoms (Button, Input)
- [ ] Components accept `className` prop for composition
- [ ] No hardcoded content in organisms — all data via props

### Accessibility
- [ ] Semantic HTML: `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`
- [ ] Single `<h1>`, sequential heading hierarchy
- [ ] Skip-to-content link present
- [ ] Color contrast: 4.5:1 text, 3:1 UI elements
- [ ] `focus-visible` on all interactive elements
- [ ] `aria-expanded`, `aria-controls` on accordions and toggles
- [ ] `aria-label` on navigation landmarks
- [ ] Form inputs have associated `<label>` elements
- [ ] `alt` text on all images
- [ ] `lang` attribute on `<html>`

### Animation
- [ ] Scroll animations use `IntersectionObserver` (not scroll events)
- [ ] Only `opacity` and `transform` are animated
- [ ] `prefers-reduced-motion` respected with `@media` query
- [ ] Stagger delay capped at ~400ms total
- [ ] `will-change` applied to animated elements

### Performance
- [ ] Above-the-fold content renders without JavaScript (SSR or static)
- [ ] Below-the-fold sections use `React.lazy` + `Suspense`
- [ ] Images: WebP format, lazy loading, explicit `width`/`height` or `aspect-ratio`
- [ ] Fonts: max 2 families, `font-display: swap`, preconnected
- [ ] Bundle size: no unnecessary dependencies (prefer CSS over JS animations)
- [ ] Lighthouse score > 90 in all categories

### SEO
- [ ] `<title>` and `<meta description>` present
- [ ] Open Graph tags (title, description, image, url, type)
- [ ] Twitter card meta tags
- [ ] Canonical URL set
- [ ] Structured data (JSON-LD) for product/organization
- [ ] Semantic HTML throughout

### Responsive
- [ ] Mobile-first CSS (`min-width` media queries)
- [ ] Touch targets minimum 44x44px
- [ ] Content stacks vertically on mobile
- [ ] Non-essential content hidden on mobile
- [ ] Tested at 320px, 768px, 1024px, 1280px widths

### Final Test
- [ ] "Squint test" passes — hierarchy is clear at a glance
- [ ] Page loads and is interactive under 3 seconds on 3G
- [ ] No layout shifts (CLS < 0.1)
- [ ] All links and CTAs work
- [ ] Looks correct with and without JavaScript
