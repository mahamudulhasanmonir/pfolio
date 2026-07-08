---
title: "PulseUI"
description: "A minimal React component library with glassmorphism design tokens and full accessibility support."
tags: ["React", "TypeScript", "CSS", "Accessibility"]
github: "https://github.com"
demo: "https://example.com"
featured: false
order: 4
---

## Overview

PulseUI is a headless-first React component library built around glassmorphism design tokens. Every component is fully accessible (WCAG 2.1 AA), keyboard navigable, and ships with zero runtime CSS-in-JS overhead.

## Design Principles

1. **Accessible by default** — ARIA roles, keyboard navigation, and focus management built in
2. **Token-driven** — all visual properties are CSS custom properties, easy to theme
3. **Headless option** — use the logic hooks without any styles if you prefer
4. **Tiny bundle** — tree-shakeable, each component is independently importable

## Components

| Component | Description |
|---|---|
| `Button` | Primary, ghost, and icon variants |
| `Card` | Glass surface with hover lift |
| `Dialog` | Accessible modal with focus trap |
| `Tooltip` | Floating label with smart positioning |
| `Badge` | Status and count indicators |
| `Input` | Text, password, and search fields |

## Usage

```tsx
import { Button, Card, Badge } from 'pulseui';

export function ProjectCard({ project }) {
  return (
    <Card className="p-6 hover:shadow-glow">
      <div className="flex items-center justify-between mb-4">
        <h3 className="font-bold text-lg">{project.title}</h3>
        <Badge variant="success">Live</Badge>
      </div>
      <p className="text-muted mb-4">{project.description}</p>
      <Button variant="primary" size="sm">
        View Project
      </Button>
    </Card>
  );
}
```

## Theming

Override the CSS custom properties to match your brand:

```css
:root {
  --pulse-accent: #6366f1;
  --pulse-accent-glow: rgba(99, 102, 241, 0.25);
  --pulse-surface: rgba(255, 255, 255, 0.6);
  --pulse-surface-border: rgba(255, 255, 255, 0.5);
  --pulse-radius: 12px;
}
```

## Accessibility

The `Dialog` component implements the ARIA dialog pattern with a full focus trap:

```tsx
import { Dialog, useDialog } from 'pulseui';

function App() {
  const dialog = useDialog();

  return (
    <>
      <Button onClick={dialog.open}>Open</Button>
      <Dialog
        {...dialog.props}
        title="Confirm action"
        description="This cannot be undone."
      >
        <Button onClick={dialog.close}>Cancel</Button>
        <Button variant="danger" onClick={handleConfirm}>Delete</Button>
      </Dialog>
    </>
  );
}
```

Focus is trapped inside the dialog, `Escape` closes it, and focus returns to the trigger on close — all automatically.

## Installation

```bash
pnpm add pulseui
```

Requires React 18+ and a CSS custom properties-capable browser (all modern browsers).
