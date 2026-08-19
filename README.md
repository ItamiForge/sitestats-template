# SiteStats Template

A self-hosted, privacy-first web analytics tool you can deploy for free on Cloudflare Workers and Pages.

> Catalog: [ItamiForge](https://itamiforge.github.io/itamiforge/docs/projects/#sitestats)

**[Documentation →](docs-site/)** · **[API Reference →](docs/API.md)**

---

## What you get

- **Lightweight tracker** — a single `<script>` tag, no npm install on your site.
- **Analytics dashboard** — pageviews, sessions, bounce rate, top pages, devices, countries, referrers, and more.
- **Custom events and goals** — track signups, purchases, or any user action.
- **Public + admin split** — share a public dashboard; keep raw data and site management owner-only.
- **Privacy-first** — no raw IP storage, no third-party calls, GDPR-friendly defaults.
- **Free to run** — fits entirely within Cloudflare's free tier for most personal and small-business use.

## Quick start

### 1. Use this template

Click **Use this template** on GitHub to create your own copy of this repo.

### 2. Install dependencies

```bash
bun install
```

### 3. Create a D1 database

```bash
bunx wrangler d1 create your-db-name
```

Paste the `database_id` into `worker/wrangler.toml`.

### 4. Apply migrations

```bash
bun run db:migrate:remote
```

### 5. Set secrets

```bash
bun run worker:secret put ADMIN_PASSWORD_HASH
bun run worker:secret put ADMIN_SESSION_SECRET   # openssl rand -hex 32
```

Fill `YOUR_*` tokens in `worker/wrangler.toml` (synced from `worker/wrangler.template.toml`).
Copy `worker/.dev.vars.example` → `worker/.dev.vars` for local development.
Optionally copy `deploy.instance.example.toml` → `deploy.instance.toml` for your own notes.

### 6. Deploy

```bash
bun run worker:deploy
```

Then deploy the dashboard to Cloudflare Pages with `VITE_API_ENDPOINT=https://<your-worker-domain>`.

**Full guide →** [docs/SETUP.md](docs/SETUP.md) or the [docs site](docs-site/).

---

## Repo layout

```
worker/        Cloudflare Worker — ingestion API, auth, analytics queries
dashboard/     React + Vite analytics dashboard
database/      D1 migrations and setup scripts
tracker/       Browser tracker script (also served by the Worker)
docs/          Markdown reference docs
docs-site/     Fuma Docs site (Next.js)
```

## Requirements

- [Bun](https://bun.sh) ≥ 1.x
- A Cloudflare account (free tier)
- Node.js ≥ 20 (for the docs site)

## License

[MIT](LICENSE)
