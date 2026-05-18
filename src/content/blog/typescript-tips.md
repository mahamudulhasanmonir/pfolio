---
title: "TypeScript Tips That Will Change How You Code"
description: "Five advanced TypeScript patterns I use every day to write safer, more expressive code."
date: 2026-04-22
tags: ["TypeScript", "JavaScript", "Tips"]
---

## 1. Discriminated Unions

Instead of using optional properties everywhere, use discriminated unions to model state explicitly:

```typescript
type Result<T> =
  | { status: 'success'; data: T }
  | { status: 'error'; error: string }
  | { status: 'loading' };
```

TypeScript will narrow the type correctly in each branch of a switch statement.

## 2. Template Literal Types

Build powerful string types at compile time:

```typescript
type EventName = `on${Capitalize<string>}`;
type CSSProperty = `${string}-${string}`;
```

## 3. Satisfies Operator

The `satisfies` operator validates a value against a type without widening it:

```typescript
const palette = {
  red: [255, 0, 0],
  green: '#00ff00',
} satisfies Record<string, string | number[]>;

// palette.red is still number[], not string | number[]
```

## 4. Infer in Conditional Types

Extract types from complex generics:

```typescript
type UnwrapPromise<T> = T extends Promise<infer U> ? U : T;
type UnwrapArray<T> = T extends Array<infer U> ? U : T;
```

## 5. const Assertions

Use `as const` to get the most specific type possible:

```typescript
const routes = ['/', '/blog', '/projects'] as const;
type Route = typeof routes[number]; // '/' | '/blog' | '/projects'
```

These patterns have saved me countless runtime bugs. TypeScript's type system is incredibly powerful once you learn to leverage it fully.
