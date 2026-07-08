---
title: "DevFlow"
description: "A full-stack project management tool with real-time collaboration, kanban boards, and GitHub integration."
tags: ["React", "Node.js", "PostgreSQL", "WebSockets"]
github: "https://github.com"
demo: "https://example.com"
featured: true
order: 1
---

## Overview

DevFlow is a modern project management application built for developer teams. It combines the simplicity of a kanban board with deep GitHub integration, real-time collaboration, and a developer-first API.

## Features

- **Real-time kanban boards** — drag-and-drop cards with live updates via WebSockets
- **GitHub integration** — link PRs, issues, and commits directly to tasks
- **Team collaboration** — presence indicators, comments, and @mentions
- **REST + GraphQL API** — full programmatic access to all resources
- **Role-based access control** — owner, admin, member, and viewer roles

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 18, Zustand, TailwindCSS |
| Backend | Node.js, Express, GraphQL |
| Database | PostgreSQL + Prisma ORM |
| Realtime | Socket.io |
| Auth | JWT + refresh tokens |

## Architecture

The backend follows a layered architecture:

```
src/
├── api/          # Route handlers
├── services/     # Business logic
├── repositories/ # Database access (Prisma)
├── events/       # WebSocket event handlers
└── middleware/   # Auth, validation, error handling
```

## Key Code: Real-time Board Sync

When a card is moved, the server broadcasts the update to all connected clients in the same workspace:

```typescript
// server/events/board.ts
socket.on('card:move', async ({ cardId, columnId, position }) => {
  const card = await cardService.move(cardId, columnId, position);

  // Broadcast to everyone in the workspace except sender
  socket.to(`workspace:${card.workspaceId}`).emit('card:moved', card);
});
```

On the client, Zustand handles the optimistic update:

```typescript
// client/store/boardStore.ts
const moveCard = (cardId: string, columnId: string, position: number) => {
  // Optimistic update
  set(state => ({ cards: reorderCards(state.cards, cardId, columnId, position) }));

  socket.emit('card:move', { cardId, columnId, position });
};
```

## Database Schema

```sql
CREATE TABLE cards (
  id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  title       TEXT NOT NULL,
  description TEXT,
  column_id   UUID REFERENCES columns(id) ON DELETE CASCADE,
  position    INTEGER NOT NULL,
  assignee_id UUID REFERENCES users(id),
  created_at  TIMESTAMPTZ DEFAULT NOW()
);
```

## Getting Started

```bash
git clone https://github.com/monir/devflow
cd devflow
pnpm install

# Set up environment
cp .env.example .env
# Edit .env with your database URL and JWT secret

# Run migrations
pnpm db:migrate

# Start dev servers
pnpm dev
```

The app will be available at `http://localhost:3000`.
