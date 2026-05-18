---
title: "Deployment"
description: "Deploy your portfolio to Vercel, Netlify, or any static host."
order: 3
---

## Build for Production

```bash
pnpm build
```

This generates a static site in the `dist/` directory.

## Deploy to Vercel

The easiest way to deploy is with Vercel:

1. Push your code to GitHub
2. Import the repository at [vercel.com/new](https://vercel.com/new)
3. Vercel auto-detects Astro and configures the build

Or use the CLI:

```bash
npx vercel --prod
```

## Deploy to Netlify

1. Connect your GitHub repo at [app.netlify.com](https://app.netlify.com)
2. Set build command: `pnpm build`
3. Set publish directory: `dist`

## Deploy to GitHub Pages

Add this to `astro.config.mjs`:

```js
export default defineConfig({
  site: 'https://username.github.io',
  base: '/repo-name',
});
```

Then use the official [Astro GitHub Pages action](https://docs.astro.build/en/guides/deploy/github/).

## Environment Variables

Create a `.env` file for local development:

```bash
PUBLIC_SITE_URL=http://localhost:4321
```

Variables prefixed with `PUBLIC_` are exposed to the client.
