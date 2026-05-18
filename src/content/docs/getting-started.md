---
title: "Getting Started"
description: "Everything you need to know to get up and running quickly."
order: 1
---

## Prerequisites

Before you begin, make sure you have the following installed:

- **Node.js** 18 or higher
- **pnpm** (recommended) or npm/yarn
- A code editor (VS Code recommended)

## Installation

Clone the repository and install dependencies:

```bash
git clone https://github.com/monir/project.git
cd project
pnpm install
```

## Running Locally

Start the development server:

```bash
pnpm dev
```

Open [http://localhost:4321](http://localhost:4321) in your browser.

## Project Structure

```
src/
├── components/    # Reusable UI components
├── content/       # Markdown content (blog, docs, projects)
├── layouts/       # Page layouts
├── pages/         # File-based routing
└── styles/        # Global CSS
```

## Next Steps

- Read the [Configuration](/docs/configuration) guide
- Explore the [API Reference](/docs/api-reference)
- Check out the [Deployment](/docs/deployment) guide
