---
title: "QueryKit"
description: "A type-safe query builder for PostgreSQL with automatic TypeScript type inference from your schema."
tags: ["TypeScript", "PostgreSQL", "Library"]
github: "https://github.com"
featured: true
order: 3
---

## Overview

QueryKit is a lightweight TypeScript library that brings full type safety to raw PostgreSQL queries. It infers your column types directly from your schema definition — no code generation step required.

## The Problem

Most query builders either sacrifice type safety or require a heavy code generation pipeline. QueryKit takes a different approach: you define your schema as TypeScript types, and the builder infers everything from there.

```typescript
// Without QueryKit — no type safety
const result = await db.query('SELECT * FROM users WHERE id = $1', [id]);
// result.rows is any[]

// With QueryKit — fully typed
const result = await db.from('users').where({ id }).select('name', 'email').one();
// result is { name: string; email: string } | null
```

## Schema Definition

```typescript
import { defineSchema, t } from 'querykit';

const schema = defineSchema({
  users: {
    id: t.uuid().primaryKey(),
    name: t.text().notNull(),
    email: t.text().notNull().unique(),
    role: t.enum(['admin', 'member']).default('member'),
    created_at: t.timestamp().default('now()'),
  },
  posts: {
    id: t.uuid().primaryKey(),
    title: t.text().notNull(),
    body: t.text(),
    author_id: t.uuid().references('users.id'),
    published: t.boolean().default(false),
  },
});

const db = createClient({ schema, connectionString: process.env.DATABASE_URL });
```

## Query Examples

**Select with filtering:**

```typescript
const admins = await db.from('users')
  .where({ role: 'admin' })
  .select('id', 'name', 'email')
  .orderBy('name', 'asc')
  .many();
// Type: { id: string; name: string; email: string }[]
```

**Insert with returning:**

```typescript
const user = await db.into('users')
  .insert({ name: 'Monir', email: 'hello@monir.dev', role: 'admin' })
  .returning('id', 'created_at')
  .one();
// Type: { id: string; created_at: Date }
```

**Joins:**

```typescript
const posts = await db.from('posts')
  .join('users', 'posts.author_id', 'users.id')
  .where({ 'posts.published': true })
  .select('posts.title', 'users.name')
  .many();
```

## Installation

```bash
pnpm add querykit
```

## How It Works

QueryKit uses TypeScript's conditional types and template literal types to infer the return type of every query at compile time:

```typescript
type SelectResult<T extends Table, K extends keyof T['columns']> = {
  [P in K]: InferColumnType<T['columns'][P]>;
};
```

No runtime overhead — all type magic happens at compile time. The generated SQL is plain parameterized queries passed directly to `pg`.
