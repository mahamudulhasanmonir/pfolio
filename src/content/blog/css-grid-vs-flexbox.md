---
title: "CSS Grid vs Flexbox: When to Use Which"
description: "A practical guide to choosing between CSS Grid and Flexbox for your layouts."
date: 2026-03-15
tags: ["CSS", "Layout", "Frontend"]
---

## The Simple Rule

- **Flexbox** → one-dimensional layouts (row OR column)
- **Grid** → two-dimensional layouts (rows AND columns)

## When to Use Flexbox

Flexbox shines for:

- Navigation bars
- Card rows that wrap
- Centering content
- Distributing space between items

```css
.nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
```

## When to Use Grid

Grid is perfect for:

- Page layouts
- Card grids with consistent sizing
- Overlapping elements
- Complex two-dimensional arrangements

```css
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1.5rem;
}
```

## The `auto-fill` vs `auto-fit` Trick

`auto-fill` creates as many columns as possible, even empty ones. `auto-fit` collapses empty columns and stretches existing ones. For responsive card grids, `auto-fill` with `minmax` is usually what you want.

## They Work Together

The best layouts often combine both. Use Grid for the overall page structure, and Flexbox for the components within each grid area.
