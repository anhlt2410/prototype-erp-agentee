# Prototypes

Static HTML prototypes for customer review, deployed on Vercel.

## Contents

- `index.html` — Landing page with links to each prototype
- `agentic.html` — Agentic AI Agent Workspace prototype
- `erp.html` — Acme ERP Employees prototype

## Local preview

Just open `index.html` in a browser, or run a quick local server:

```bash
# Python 3
python3 -m http.server 8000

# Or Node
npx serve .
```

Then visit `http://localhost:8000`.

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
