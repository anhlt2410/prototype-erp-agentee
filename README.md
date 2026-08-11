# Prototypes

Static HTML prototypes for customer review, deployed on Vercel.

## Contents

- `index.html` — Landing page with links to each prototype
- `agentic.html` — Agentic AI Agent Workspace prototype
- `erp.html` — Acme ERP Employees prototype

## Local preview

```bash
pnpm install
pnpm dev
```

Then visit `http://localhost:8000`. The dev server mirrors the production
`cleanUrls` setting, so `/erp.html` redirects to `/erp` just like on Vercel.

There is no build step — the prototypes are self-contained HTML and are
deployed exactly as they sit in the repo. You can still just open
`index.html` in a browser if you prefer.

## Deploying to Vercel

### Option 1 — Vercel dashboard (easiest)

1. Push this repo to GitHub.
2. Go to [vercel.com/new](https://vercel.com/new) and import the repo.
3. Leave all settings as default (no build step needed — it's static).
4. Click **Deploy**.

### Option 2 — Vercel CLI

```bash
npm i -g vercel
vercel
```

Follow the prompts. For production:

```bash
vercel --prod
```

## URLs after deploy

- `/` → landing page
- `/agentic.html` → Agentic prototype
- `/erp.html` → ERP prototype
