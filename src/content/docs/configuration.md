---
title: "Configuration"
description: "Learn how to configure and customize your portfolio."
order: 2
---

## Site Configuration

Edit `astro.config.mjs` to configure your site:

```js
import { defineConfig } from 'astro/config';
import tailwind from '@astrojs/tailwind';

export default defineConfig({
  site: 'https://yoursite.com',
  integrations: [tailwind()],
});
```

## Tailwind Configuration

The `tailwind.config.mjs` file controls your design tokens:

```js
export default {
  darkMode: 'class',
  theme: {
    extend: {
      colors: {
        accent: '#6366f1',
      },
    },
  },
};
```

## CSS Custom Properties

Global design tokens are defined as CSS custom properties in `src/styles/global.css`:

| Variable | Light | Dark |
|---|---|---|
| `--bg` | `#f8fafc` | `#030712` |
| `--accent` | `#6366f1` | `#818cf8` |
| `--text` | `#0f172a` | `#f1f5f9` |

## Content Collections

Add your content to the `src/content/` directory:

- `blog/` — Markdown blog posts
- `docs/` — Documentation pages
- `projects/` — Project showcases

Each collection has a schema defined in `src/content/config.ts`.
