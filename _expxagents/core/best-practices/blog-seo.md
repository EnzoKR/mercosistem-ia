---
platform: blog
format: seo-content
constraints:
  max_chars: null
  image_ratio: "16:9"
  max_hashtags: null
---

# Best Practices: Blog — SEO-Optimized Content

## Format Rules

- Title tag: 50–60 characters; primary keyword in the first 3 words when possible
- Meta description: 150–160 characters; include primary keyword and a clear benefit
- URL slug: lowercase, hyphens only, primary keyword only (e.g., `/best-crm-software`)
- H1: exact match or close variant of the target keyword; use only once
- Keyword density: 1–2% naturally placed; avoid keyword stuffing
- Image alt text: descriptive and keyword-contextual (not just the keyword alone)
- Schema markup: Article or HowTo schema for rich snippets
- Page speed: target Core Web Vitals — LCP < 2.5s, CLS < 0.1, FID < 100ms

## Structure

```
[TITLE TAG — primary keyword first]

[META DESCRIPTION — keyword + benefit + CTA under 160 chars]

[H1 — matches or closely mirrors title tag]

[INTRODUCTION]
- Mention primary keyword in first 100 words
- Acknowledge the search intent (informational, commercial, transactional)

[TABLE OF CONTENTS — for articles over 1500 words; improves dwell time]

[H2 SECTIONS — secondary and LSI keywords as H2 headers]
- Each H2 targets a related search query
- 200–400 words per section

[H2 FAQ SECTION]
- Target "People Also Ask" queries from Google SERP
- Question as H3, concise answer (40–60 words) immediately following

[CONCLUSION with CTA]
```

## Guidelines

- **Match search intent precisely.** Rank for the right audience by matching what someone actually wants when they type that query (informational, navigational, transactional, commercial investigation).
- Use tools like Ahrefs, Semrush, or Google Search Console to identify the exact keyword phrase to target.
- Cover the topic comprehensively — include sub-topics that competing articles address, then add unique depth they don't.
- Build topical authority: create a cluster of 5–15 related articles all linking to one cornerstone page on the topic.
- Earn backlinks through original data, studies, quotes from experts, or unique tools embedded in the page.
- E-E-A-T (Experience, Expertise, Authoritativeness, Trustworthiness): include author bios, cite sources, show real experience.
- Structured data (JSON-LD): implement Article, BreadcrumbList, and FAQPage schema where relevant.
- Internal link anchor text should be descriptive and keyword-relevant, not generic ("click here").

## Examples

**Meta description:**
```
Discover the 7 best project management tools in 2024 — compared by price, features, and team size. Find the right fit in under 5 minutes.
```

**FAQPage schema example (JSON-LD):**
```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [{
    "@type": "Question",
    "name": "What is the best CRM for small businesses?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "HubSpot CRM is the top choice for small businesses due to its free tier, ease of use, and robust integrations."
    }
  }]
}
```

**Keyword placement checklist:**
- [ ] Title tag (first 3 words)
- [ ] Meta description (natural inclusion)
- [ ] H1 header
- [ ] First paragraph (within 100 words)
- [ ] At least one H2 header
- [ ] Image alt text
- [ ] URL slug
- [ ] Conclusion paragraph
