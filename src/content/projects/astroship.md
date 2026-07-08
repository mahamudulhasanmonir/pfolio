---
title: "AstroShip"
description: "An open-source Astro starter template with authentication, blog, and dark mode out of the box."
tags: ["Astro", "TypeScript", "Tailwind"]
github: "https://github.com"
demo: "https://example.com"
featured: true
order: 2
---

## Overview

AstroShip is a production-ready starter template for Astro projects. It ships with everything you need to launch a modern website — authentication, a blog engine, dark mode, and SEO — all pre-configured and ready to customize.

## What's Included

- ✅ Glassmorphism UI with dark/light mode (no flash)
- ✅ Content Collections for blog and docs
- ✅ SEO meta tags and Open Graph images
- ✅ Sitemap and RSS feed generation
- ✅ 100/100 Lighthouse score out of the box

## Project Structure

```
src/
├── content/
│   ├── blog/        # Markdown blog posts
│   └── docs/        # Documentation pages
├── layouts/
│   └── Layout.astro # Base layout with nav + footer
├── pages/
│   ├── index.astro
│   ├── blog/
│   └── docs/
└── styles/
    └── global.css   # Design tokens + utilities
```

## Dark Mode Without Flash

The key to flicker-free dark mode is a blocking inline script in `<head>`:

```html
<script is:inline>
  const t = localStorage.getItem('theme');
  const dark = t === 'dark' || (!t && window.matchMedia('(prefers-color-scheme: dark)').matches);
  if (dark) document.documentElement.classList.add('dark');
  document.write('<style id="_ti">' + (dark ? '#icon-moon{display:none}' : '#icon-sun{display:none}') + '</style>');
</script>
```

This runs synchronously before the browser paints anything, so the correct theme is applied from the very first frame.

## Content Collections

Define your schema once in `content.config.ts`:

```typescript
import { defineCollection, z } from 'astro:content';
import { glob } from 'astro/loaders';

const blog = defineCollection({
  loader: glob({ pattern: '**/*.md', base: './src/content/blog' }),
  schema: z.object({
    title: z.string(),
    date: z.coerce.date(),
    tags: z.array(z.string()).default([]),
  }),
});

export const collections = { blog };
```

## Performance

AstroShip ships **zero JavaScript** by default. Every page is pure static HTML + CSS. Interactive components opt-in via Astro Islands.

```bash
# Lighthouse scores (production build)
Performance:    100
Accessibility:  100
Best Practices: 100
SEO:            100
```

## Quick Start

```bash
npx create-astro@latest my-site --template monir/astroship
cd my-site
pnpm install
pnpm dev
```
