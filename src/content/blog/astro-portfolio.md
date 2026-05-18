---
title: "Building a Lightning-Fast Portfolio with Astro"
description: "How I built this portfolio using Astro, Tailwind CSS, and glassmorphism design — achieving a perfect Lighthouse score."
date: 2026-05-10
tags: ["Astro", "Performance", "CSS"]
---

## Why Astro?

Astro is a modern static site builder that ships **zero JavaScript by default**. For a portfolio site, this means blazing-fast load times and perfect Core Web Vitals scores.

## The Glassmorphism Effect

The frosted glass effect on the navigation is achieved with just a few CSS properties:

```css
.glass-nav {
  background: rgba(3, 7, 18, 0.75);
  backdrop-filter: blur(20px) saturate(200%);
  border-bottom: 1px solid rgba(99, 102, 241, 0.2);
}
```

The key is `backdrop-filter: blur()` combined with a semi-transparent background. The `saturate()` function enhances the colors behind the element, giving it that premium look.

## Dark Mode Without Flash

To avoid the dreaded flash of unstyled content (FOUC) when loading in dark mode, I store the preference in `localStorage` and apply the class synchronously before the page renders:

```js
const isDark = localStorage.getItem('theme') === 'dark';
if (isDark) document.documentElement.classList.add('dark');
```

## Performance Results

- **Lighthouse Performance**: 100
- **First Contentful Paint**: 0.4s
- **Time to Interactive**: 0.4s

Astro's island architecture means only the interactive components ship JavaScript — everything else is pure HTML and CSS.
