---
platform: software-house
format: fullstack-page-generation
constraints:
  max_chars: null
  image_ratio: null
  max_hashtags: null
---

# Full-Stack Page Generation — Best Practices

## Philosophy

Unlike single-file HTML landing pages, full-stack generation creates **production-ready project structures** that integrate with existing codebases or stand alone as deployable applications. The goal is never a throwaway prototype — it is a codebase a team can maintain, extend, and deploy with confidence.

Every generated project must be:

- **Typed end-to-end** — TypeScript strict mode, no `any` escapes.
- **Token-driven** — Colors, spacing, typography, and radii defined once, referenced everywhere.
- **Component-decomposed** — Atoms, molecules, organisms. Never a monolithic single component.
- **Build-ready** — `npm install && npm run build` must succeed on first run.
- **Accessible by default** — Semantic HTML, ARIA attributes, keyboard navigation, focus management.

---

## Supported Stacks

### 1. Next.js (Recommended for SSR/SSG)

Best for marketing sites, content platforms, and applications requiring server-side rendering or static generation.

```
project/
├── src/
│   ├── app/                  # App Router (Next.js 14+)
│   │   ├── layout.tsx        # Root layout with metadata
│   │   ├── page.tsx          # Home page
│   │   └── globals.css       # Global resets + font imports
│   ├── components/
│   │   ├── ui/               # Atoms: Button, Badge, Input, Heading, Text
│   │   ├── sections/         # Organisms: Hero, Features, Pricing, Testimonials
│   │   └── layout/           # Layout: Container, Header, Footer, NavBar
│   ├── lib/
│   │   └── utils.ts          # cn() helper, formatters, constants
│   └── styles/
│       └── tokens.css        # Design tokens as CSS custom properties
├── public/                   # Static assets (images, fonts, favicon)
├── package.json
├── tailwind.config.ts
├── tsconfig.json
└── next.config.ts
```

### 2. Vite + React (Recommended for SPAs)

Best for interactive applications, dashboards, and tools that do not need server-side rendering.

```
project/
├── src/
│   ├── main.tsx              # Entry point — ReactDOM.createRoot
│   ├── App.tsx               # Root component with router
│   ├── components/
│   │   ├── ui/               # Atoms: Button, Badge, Input, Heading, Text
│   │   ├── sections/         # Organisms: Hero, Features, Pricing
│   │   └── layout/           # Layout: Container, Header, Footer
│   ├── hooks/                # Custom hooks (useMediaQuery, useScrollPosition)
│   ├── lib/
│   │   └── utils.ts          # cn() helper, formatters
│   └── styles/
│       ├── tokens.css        # Design tokens
│       └── global.css        # Resets, base styles
├── public/                   # Static assets
├── index.html                # HTML entry point
├── package.json
├── vite.config.ts
├── tailwind.config.ts
└── tsconfig.json
```

### 3. Astro (Recommended for content-heavy static sites)

Best for blogs, documentation sites, and content-driven pages where minimal JavaScript is desired.

```
project/
├── src/
│   ├── layouts/
│   │   └── BaseLayout.astro  # Root layout with <html>, <head>, <body>
│   ├── pages/
│   │   └── index.astro       # Home page
│   ├── components/           # .astro or .tsx components
│   │   ├── ui/
│   │   ├── sections/
│   │   └── layout/
│   └── styles/
│       └── tokens.css
├── public/
├── package.json
├── astro.config.mjs
├── tailwind.config.ts
└── tsconfig.json
```

---

## Generation Workflow

### Step 1: Scaffold Project

Initialize the project with all necessary tooling before writing any component code.

```bash
# Next.js
npx create-next-app@latest project --typescript --tailwind --eslint --app --src-dir --import-alias "@/*"

# Vite + React
npm create vite@latest project -- --template react-ts
cd project && npm install tailwindcss @tailwindcss/vite

# Astro
npm create astro@latest project -- --template minimal --typescript strict
cd project && npx astro add tailwind
```

After scaffolding:
1. Remove boilerplate content (default pages, sample styles).
2. Create the `styles/tokens.css` file with the design token system.
3. Create the component directory structure (`ui/`, `sections/`, `layout/`).
4. Add the `lib/utils.ts` helper file.

### Step 2: Design Token System

All visual properties flow from a single source of truth. Define tokens as CSS custom properties and map them into Tailwind's configuration.

**`src/styles/tokens.css`**:

```css
:root {
  /* === COLORS === */
  --color-base-900: #0f172a;
  --color-base-800: #1e293b;
  --color-base-700: #334155;
  --color-base-200: #e2e8f0;
  --color-base-100: #f1f5f9;
  --color-base-50: #f8fafc;
  --color-white: #ffffff;

  --color-accent: oklch(0.65 0.25 250);
  --color-accent-hover: oklch(0.58 0.25 250);
  --color-accent-subtle: oklch(0.65 0.25 250 / 0.1);

  --color-surface: var(--color-white);
  --color-surface-alt: var(--color-base-50);
  --color-surface-dark: var(--color-base-900);
  --color-on-surface: var(--color-base-800);
  --color-on-surface-muted: var(--color-base-700);
  --color-on-dark: var(--color-base-50);

  /* === SPACING (4px base) === */
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

  --section-py: clamp(4rem, 10vw, 8rem);
  --container-max: 1200px;
  --container-narrow: 720px;

  /* === TYPOGRAPHY === */
  --font-display: 'Plus Jakarta Sans', 'Inter', system-ui, sans-serif;
  --font-body: 'Inter', system-ui, sans-serif;
  --font-mono: 'JetBrains Mono', 'Fira Code', monospace;

  --text-display: clamp(2.5rem, 5vw + 1rem, 4.5rem);
  --text-h1: clamp(2rem, 4vw + 0.5rem, 3.5rem);
  --text-h2: clamp(1.5rem, 3vw + 0.25rem, 2.25rem);
  --text-h3: clamp(1.125rem, 2vw + 0.25rem, 1.5rem);
  --text-body: clamp(1rem, 1vw + 0.5rem, 1.125rem);
  --text-small: 0.875rem;

  --leading-tight: 1.15;
  --leading-normal: 1.6;

  /* === RADIUS === */
  --radius-sm: 0.375rem;
  --radius-md: 0.75rem;
  --radius-lg: 1rem;
  --radius-xl: 1.5rem;
  --radius-full: 9999px;

  /* === SHADOWS === */
  --shadow-sm: 0 1px 2px rgb(0 0 0 / 0.05);
  --shadow-md: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
  --shadow-lg: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
  --shadow-xl: 0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1);

  /* === TRANSITIONS === */
  --transition-fast: 150ms ease;
  --transition-base: 250ms ease;
  --transition-slow: 400ms ease;
}
```

### Step 3: Tailwind Configuration

Map CSS tokens into Tailwind so utility classes reference the design system.

**`tailwind.config.ts`**:

```typescript
import type { Config } from "tailwindcss";

const config: Config = {
  content: ["./src/**/*.{ts,tsx,astro,mdx}"],
  theme: {
    extend: {
      colors: {
        accent: {
          DEFAULT: "var(--color-accent)",
          hover: "var(--color-accent-hover)",
          subtle: "var(--color-accent-subtle)",
        },
        surface: {
          DEFAULT: "var(--color-surface)",
          alt: "var(--color-surface-alt)",
          dark: "var(--color-surface-dark)",
        },
        on: {
          surface: "var(--color-on-surface)",
          "surface-muted": "var(--color-on-surface-muted)",
          dark: "var(--color-on-dark)",
        },
      },
      fontFamily: {
        display: "var(--font-display)",
        body: "var(--font-body)",
        mono: "var(--font-mono)",
      },
      fontSize: {
        display: ["var(--text-display)", { lineHeight: "var(--leading-tight)" }],
        h1: ["var(--text-h1)", { lineHeight: "var(--leading-tight)" }],
        h2: ["var(--text-h2)", { lineHeight: "var(--leading-tight)" }],
        h3: ["var(--text-h3)", { lineHeight: "var(--leading-tight)" }],
        body: ["var(--text-body)", { lineHeight: "var(--leading-normal)" }],
        small: ["var(--text-small)", { lineHeight: "var(--leading-normal)" }],
      },
      borderRadius: {
        sm: "var(--radius-sm)",
        md: "var(--radius-md)",
        lg: "var(--radius-lg)",
        xl: "var(--radius-xl)",
      },
      boxShadow: {
        sm: "var(--shadow-sm)",
        md: "var(--shadow-md)",
        lg: "var(--shadow-lg)",
        xl: "var(--shadow-xl)",
      },
      maxWidth: {
        container: "var(--container-max)",
        narrow: "var(--container-narrow)",
      },
    },
  },
  plugins: [],
};

export default config;
```

### Step 4: Component Library

Build components in a strict layered order: atoms first, then molecules, then organisms/sections.

#### Utility — `cn()` helper

**`src/lib/utils.ts`**:

```typescript
import { type ClassValue, clsx } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]): string {
  return twMerge(clsx(inputs));
}
```

Install dependencies: `npm install clsx tailwind-merge`.

#### Atoms — Button

**`src/components/ui/Button.tsx`**:

```typescript
import { forwardRef, type ButtonHTMLAttributes } from "react";
import { cn } from "@/lib/utils";

interface ButtonProps extends ButtonHTMLAttributes<HTMLButtonElement> {
  variant?: "primary" | "secondary" | "ghost";
  size?: "sm" | "md" | "lg";
}

const variantStyles: Record<NonNullable<ButtonProps["variant"]>, string> = {
  primary:
    "bg-accent text-white hover:bg-accent-hover focus-visible:ring-accent/50",
  secondary:
    "bg-surface-alt text-on-surface border border-on-surface/10 hover:bg-surface-alt/80",
  ghost:
    "bg-transparent text-on-surface hover:bg-surface-alt",
};

const sizeStyles: Record<NonNullable<ButtonProps["size"]>, string> = {
  sm: "px-3 py-1.5 text-small rounded-sm",
  md: "px-5 py-2.5 text-body rounded-md",
  lg: "px-8 py-3.5 text-body rounded-lg font-semibold",
};

export const Button = forwardRef<HTMLButtonElement, ButtonProps>(
  ({ variant = "primary", size = "md", className, children, ...props }, ref) => (
    <button
      ref={ref}
      className={cn(
        "inline-flex items-center justify-center font-medium",
        "transition-colors duration-[var(--transition-fast)]",
        "focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-offset-2",
        "disabled:pointer-events-none disabled:opacity-50",
        variantStyles[variant],
        sizeStyles[size],
        className
      )}
      {...props}
    >
      {children}
    </button>
  )
);

Button.displayName = "Button";
```

#### Atoms — Heading

**`src/components/ui/Heading.tsx`**:

```typescript
import { type HTMLAttributes } from "react";
import { cn } from "@/lib/utils";

type HeadingLevel = "h1" | "h2" | "h3" | "h4";

interface HeadingProps extends HTMLAttributes<HTMLHeadingElement> {
  as?: HeadingLevel;
  size?: "display" | "h1" | "h2" | "h3";
}

const sizeClasses: Record<NonNullable<HeadingProps["size"]>, string> = {
  display: "text-display font-display font-extrabold tracking-tight",
  h1: "text-h1 font-display font-bold tracking-tight",
  h2: "text-h2 font-display font-bold",
  h3: "text-h3 font-display font-semibold",
};

export function Heading({
  as: Tag = "h2",
  size = "h2",
  className,
  children,
  ...props
}: HeadingProps) {
  return (
    <Tag className={cn(sizeClasses[size], "text-on-surface", className)} {...props}>
      {children}
    </Tag>
  );
}
```

#### Atoms — Badge

**`src/components/ui/Badge.tsx`**:

```typescript
import { type HTMLAttributes } from "react";
import { cn } from "@/lib/utils";

interface BadgeProps extends HTMLAttributes<HTMLSpanElement> {
  variant?: "default" | "accent" | "outline";
}

export function Badge({ variant = "default", className, children, ...props }: BadgeProps) {
  return (
    <span
      className={cn(
        "inline-flex items-center px-3 py-1 text-small font-medium rounded-full",
        variant === "default" && "bg-surface-alt text-on-surface-muted",
        variant === "accent" && "bg-accent-subtle text-accent",
        variant === "outline" && "border border-on-surface/20 text-on-surface-muted",
        className
      )}
      {...props}
    >
      {children}
    </span>
  );
}
```

#### Layout — Container

**`src/components/layout/Container.tsx`**:

```typescript
import { type HTMLAttributes } from "react";
import { cn } from "@/lib/utils";

interface ContainerProps extends HTMLAttributes<HTMLDivElement> {
  narrow?: boolean;
  as?: "div" | "section" | "main" | "article";
}

export function Container({
  narrow = false,
  as: Tag = "div",
  className,
  children,
  ...props
}: ContainerProps) {
  return (
    <Tag
      className={cn(
        "mx-auto w-full px-[var(--space-6)]",
        narrow ? "max-w-narrow" : "max-w-container",
        className
      )}
      {...props}
    >
      {children}
    </Tag>
  );
}
```

#### Molecules — Feature Card

**`src/components/ui/FeatureCard.tsx`**:

```typescript
import { type ReactNode } from "react";
import { cn } from "@/lib/utils";
import { Heading } from "./Heading";

interface FeatureCardProps {
  icon: ReactNode;
  title: string;
  description: string;
  className?: string;
}

export function FeatureCard({ icon, title, description, className }: FeatureCardProps) {
  return (
    <div
      className={cn(
        "flex flex-col gap-[var(--space-4)] p-[var(--space-8)]",
        "bg-surface rounded-lg shadow-sm",
        "border border-on-surface/5",
        "transition-shadow duration-[var(--transition-base)]",
        "hover:shadow-md",
        className
      )}
    >
      <div className="flex h-12 w-12 items-center justify-center rounded-md bg-accent-subtle text-accent">
        {icon}
      </div>
      <Heading as="h3" size="h3">
        {title}
      </Heading>
      <p className="text-body text-on-surface-muted leading-relaxed">
        {description}
      </p>
    </div>
  );
}
```

#### Organisms — Hero Section

**`src/components/sections/HeroSection.tsx`**:

```typescript
import { Container } from "@/components/layout/Container";
import { Badge } from "@/components/ui/Badge";
import { Button } from "@/components/ui/Button";
import { Heading } from "@/components/ui/Heading";

interface HeroSectionProps {
  badge?: string;
  title: string;
  subtitle: string;
  primaryCta: { label: string; href: string };
  secondaryCta?: { label: string; href: string };
}

export function HeroSection({
  badge,
  title,
  subtitle,
  primaryCta,
  secondaryCta,
}: HeroSectionProps) {
  return (
    <section className="py-[var(--section-py)] bg-surface">
      <Container narrow className="text-center">
        <div className="flex flex-col items-center gap-[var(--space-6)]">
          {badge && (
            <Badge variant="accent">{badge}</Badge>
          )}

          <Heading as="h1" size="display">
            {title}
          </Heading>

          <p className="max-w-[600px] text-body text-on-surface-muted leading-relaxed">
            {subtitle}
          </p>

          <div className="flex flex-wrap items-center justify-center gap-[var(--space-4)] mt-[var(--space-4)]">
            <Button size="lg" asChild>
              <a href={primaryCta.href}>{primaryCta.label}</a>
            </Button>

            {secondaryCta && (
              <Button variant="secondary" size="lg" asChild>
                <a href={secondaryCta.href}>{secondaryCta.label}</a>
              </Button>
            )}
          </div>
        </div>
      </Container>
    </section>
  );
}
```

#### Organisms — Features Grid

**`src/components/sections/FeaturesSection.tsx`**:

```typescript
import { type ReactNode } from "react";
import { Container } from "@/components/layout/Container";
import { Heading } from "@/components/ui/Heading";
import { FeatureCard } from "@/components/ui/FeatureCard";

interface Feature {
  icon: ReactNode;
  title: string;
  description: string;
}

interface FeaturesSectionProps {
  badge?: string;
  title: string;
  subtitle?: string;
  features: Feature[];
  columns?: 2 | 3 | 4;
}

const gridCols: Record<number, string> = {
  2: "grid-cols-1 md:grid-cols-2",
  3: "grid-cols-1 md:grid-cols-2 lg:grid-cols-3",
  4: "grid-cols-1 md:grid-cols-2 lg:grid-cols-4",
};

export function FeaturesSection({
  title,
  subtitle,
  features,
  columns = 3,
}: FeaturesSectionProps) {
  return (
    <section className="py-[var(--section-py)] bg-surface-alt">
      <Container>
        <div className="text-center mb-[var(--space-16)]">
          <Heading as="h2" size="h2">
            {title}
          </Heading>
          {subtitle && (
            <p className="mt-[var(--space-4)] text-body text-on-surface-muted max-w-narrow mx-auto">
              {subtitle}
            </p>
          )}
        </div>

        <div className={`grid ${gridCols[columns]} gap-[var(--space-8)]`}>
          {features.map((feature) => (
            <FeatureCard key={feature.title} {...feature} />
          ))}
        </div>
      </Container>
    </section>
  );
}
```

### Step 5: Page Assembly

Compose sections into a complete page.

**`src/app/page.tsx`** (Next.js) or **`src/App.tsx`** (Vite):

```typescript
import { HeroSection } from "@/components/sections/HeroSection";
import { FeaturesSection } from "@/components/sections/FeaturesSection";
// Import more sections as needed

export default function HomePage() {
  return (
    <main>
      <HeroSection
        badge="Now in Beta"
        title="Ship faster with AI-powered squads"
        subtitle="Orchestrate teams of AI agents to design, build, and deploy production-ready applications in minutes."
        primaryCta={{ label: "Get Started", href: "/signup" }}
        secondaryCta={{ label: "See Demo", href: "/demo" }}
      />

      <FeaturesSection
        title="Everything you need"
        subtitle="A complete platform for AI-driven development workflows."
        columns={3}
        features={[
          {
            icon: <span aria-hidden="true">&#9881;</span>,
            title: "Automated Scaffolding",
            description:
              "Generate complete project structures with TypeScript, Tailwind, and your preferred framework.",
          },
          {
            icon: <span aria-hidden="true">&#9733;</span>,
            title: "Component Library",
            description:
              "Every project includes typed, accessible UI components built from your design tokens.",
          },
          {
            icon: <span aria-hidden="true">&#9889;</span>,
            title: "One-Command Deploy",
            description:
              "Build and deploy to Vercel, Netlify, or GitHub Pages with a single command.",
          },
        ]}
      />
    </main>
  );
}
```

### Step 6: SEO Metadata

**Next.js App Router** — export metadata from `layout.tsx` or `page.tsx`:

```typescript
import type { Metadata } from "next";

export const metadata: Metadata = {
  title: "Project Name — Tagline",
  description: "A concise description for search engines (max 160 chars).",
  openGraph: {
    title: "Project Name — Tagline",
    description: "A concise description for social sharing.",
    url: "https://example.com",
    siteName: "Project Name",
    type: "website",
    images: [{ url: "/og-image.png", width: 1200, height: 630 }],
  },
  twitter: {
    card: "summary_large_image",
    title: "Project Name — Tagline",
    description: "A concise description for social sharing.",
    images: ["/og-image.png"],
  },
};
```

**Vite + React** — use `react-helmet-async`:

```typescript
import { Helmet } from "react-helmet-async";

export function SEO({ title, description }: { title: string; description: string }) {
  return (
    <Helmet>
      <title>{title}</title>
      <meta name="description" content={description} />
      <meta property="og:title" content={title} />
      <meta property="og:description" content={description} />
    </Helmet>
  );
}
```

### Step 7: Build and Deploy

```bash
# Next.js
npm run build         # produces .next/
npx next export       # static export to out/ (if applicable)

# Vite
npm run build         # produces dist/

# Astro
npm run build         # produces dist/
```

Deployment targets:
- **Vercel**: `npx vercel --prod` (zero-config for Next.js)
- **Netlify**: push to repo with `netlify.toml` or use `npx netlify deploy --prod`
- **GitHub Pages**: use `gh-pages` package or GitHub Actions workflow

---

## Package.json Template

```json
{
  "name": "project-name",
  "version": "0.1.0",
  "private": true,
  "type": "module",
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint",
    "type-check": "tsc --noEmit"
  },
  "dependencies": {
    "next": "^14.2.0",
    "react": "^18.3.0",
    "react-dom": "^18.3.0",
    "clsx": "^2.1.0",
    "tailwind-merge": "^2.3.0"
  },
  "devDependencies": {
    "@types/node": "^20.0.0",
    "@types/react": "^18.3.0",
    "@types/react-dom": "^18.3.0",
    "autoprefixer": "^10.4.0",
    "postcss": "^8.4.0",
    "tailwindcss": "^3.4.0",
    "typescript": "^5.5.0"
  }
}
```

For **Vite + React**, replace the `scripts` and `next` dependency:

```json
{
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "preview": "vite preview",
    "lint": "eslint src --ext .ts,.tsx",
    "type-check": "tsc --noEmit"
  },
  "dependencies": {
    "react": "^18.3.0",
    "react-dom": "^18.3.0",
    "react-router-dom": "^6.23.0",
    "clsx": "^2.1.0",
    "tailwind-merge": "^2.3.0"
  },
  "devDependencies": {
    "@vitejs/plugin-react": "^4.3.0",
    "vite": "^5.4.0",
    "tailwindcss": "^3.4.0",
    "typescript": "^5.5.0"
  }
}
```

---

## TypeScript Configuration

**`tsconfig.json`**:

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "lib": ["DOM", "DOM.Iterable", "ES2022"],
    "module": "ESNext",
    "moduleResolution": "bundler",
    "jsx": "react-jsx",
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true,
    "forceConsistentCasingInFileNames": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  "include": ["src"],
  "exclude": ["node_modules", "dist"]
}
```

---

## Scroll Animations

Use CSS `@keyframes` and `IntersectionObserver` for performant scroll-triggered animations. Avoid heavy animation libraries for simple reveal effects.

**`src/hooks/useInView.ts`**:

```typescript
import { useEffect, useRef, useState } from "react";

interface UseInViewOptions {
  threshold?: number;
  rootMargin?: string;
  triggerOnce?: boolean;
}

export function useInView({
  threshold = 0.1,
  rootMargin = "0px",
  triggerOnce = true,
}: UseInViewOptions = {}) {
  const ref = useRef<HTMLDivElement>(null);
  const [inView, setInView] = useState(false);

  useEffect(() => {
    const element = ref.current;
    if (!element) return;

    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          setInView(true);
          if (triggerOnce) observer.unobserve(element);
        } else if (!triggerOnce) {
          setInView(false);
        }
      },
      { threshold, rootMargin }
    );

    observer.observe(element);
    return () => observer.disconnect();
  }, [threshold, rootMargin, triggerOnce]);

  return { ref, inView };
}
```

**Usage in a section component**:

```typescript
import { useInView } from "@/hooks/useInView";
import { cn } from "@/lib/utils";

export function AnimatedSection({ children }: { children: React.ReactNode }) {
  const { ref, inView } = useInView({ threshold: 0.15 });

  return (
    <div
      ref={ref}
      className={cn(
        "transition-all duration-700 ease-out",
        inView
          ? "opacity-100 translate-y-0"
          : "opacity-0 translate-y-8"
      )}
    >
      {children}
    </div>
  );
}
```

---

## Responsive Design Rules

- **Mobile-first**: Write base styles for mobile, use `md:` and `lg:` breakpoints for larger screens.
- **Fluid typography**: All heading sizes use `clamp()` — no breakpoint jumps.
- **Fluid spacing**: Section padding uses `clamp()` for smooth scaling.
- **Grid to stack**: Multi-column grids collapse to single column on mobile (`grid-cols-1 md:grid-cols-2 lg:grid-cols-3`).
- **Touch targets**: Minimum 44x44px for all interactive elements on mobile.
- **No horizontal scroll**: Container always has `px-[var(--space-6)]` padding and `max-w-container`.

---

## Accessibility Checklist

- [ ] All images have `alt` text (or `alt=""` + `aria-hidden="true"` for decorative).
- [ ] Heading hierarchy is sequential (h1 > h2 > h3, no skipping levels).
- [ ] All interactive elements are keyboard-focusable with visible focus indicators.
- [ ] Color contrast ratio meets WCAG AA (4.5:1 for text, 3:1 for large text).
- [ ] Form inputs have associated `<label>` elements.
- [ ] Navigation landmarks use `<nav>`, `<main>`, `<header>`, `<footer>`.
- [ ] Decorative icons use `aria-hidden="true"`.
- [ ] Skip-to-content link is present for keyboard users.

---

## Anti-Patterns

| Anti-Pattern | Why It Fails | Correct Approach |
|---|---|---|
| Monolithic single component | Unmaintainable, untestable, impossible to reuse | Decompose into atoms, molecules, organisms |
| No TypeScript | Bugs surface at runtime, not build time | `strict: true` in tsconfig, all props typed |
| Hardcoded colors and spacing | Inconsistent design, painful to rebrand | Design tokens in `tokens.css`, referenced via Tailwind |
| CSS-in-JS with runtime overhead | Slower first paint, bundle bloat | Tailwind utilities or CSS Modules |
| No `package.json` / build config | Cannot install, build, or deploy | Always generate complete project scaffolding |
| Skipping accessibility | Excludes users, legal risk | Semantic HTML, ARIA, focus management from the start |
| Inline styles for layout | Hard to maintain, no responsive support | Tailwind utilities or CSS classes |
| No SEO metadata | Invisible to search engines and social platforms | Export metadata (Next.js) or use `<Helmet>` (Vite) |
| Single massive CSS file | Specificity conflicts, dead code accumulation | Component-scoped styles via Tailwind or CSS Modules |
| Skipping error states | Broken UX when API calls fail or content is missing | Loading, error, and empty states for every data-driven component |
