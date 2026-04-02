# atlas-starter-vercel

A text-to-SQL data analyst agent powered by [Atlas](https://www.useatlas.dev).

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?env=AI_GATEWAY_API_KEY,BETTER_AUTH_SECRET&envDescription=AI_GATEWAY_API_KEY%3A%20Vercel%20AI%20Gateway%20key%20(vercel.com%2F~%2Fai%2Fapi-keys).%20BETTER_AUTH_SECRET%3A%20Random%20string%2C%2032%2B%20chars%20(openssl%20rand%20-base64%2032).&project-name=atlas-starter-vercel)

This project is configured for **PostgreSQL**. Ask natural-language questions, and the agent explores a semantic layer, writes validated SQL, and returns interpreted results.

## Quick Start

1. **Install dependencies:**
   ```bash
   bun install
   ```

2. **Configure environment:** Edit `.env` with your API key and database URL.

3. **Generate semantic layer:**
   ```bash
   bun run atlas -- init          # From your database
   bun run atlas -- init --demo   # Or load demo data
   ```

4. **Run locally:**
   ```bash
   bun run dev
   ```
   Open [http://localhost:3000](http://localhost:3000).

## Deploy to Vercel

1. Push to GitHub:
   ```bash
   git init && git add -A && git commit -m "Initial commit"
   gh repo create atlas-starter-vercel --public --source=. --push
   ```

2. Import in the [Vercel Dashboard](https://vercel.com/new) and set environment variables:
   - `ATLAS_PROVIDER` — `anthropic` (or `gateway` for Vercel AI Gateway)
   - `ANTHROPIC_API_KEY` — Your API key
   - `ATLAS_DATASOURCE_URL` — Your analytics database (`postgresql://...`)
   - `DATABASE_URL` — Atlas internal Postgres (auth, audit)

3. Deploy. Vercel auto-detects `@vercel/sandbox` for secure explore isolation.

## Project Structure

```
atlas-starter-vercel/
├── src/                # Application source (API + UI)
├── bin/                # CLI tools (atlas init, enrich, eval)
├── data/               # Demo datasets (SQL seed files)
├── semantic/           # Semantic layer (YAML — entities, metrics, glossary)
├── .env                # Environment configuration
└── docs/deploy.md      # Full deployment guide
```

## Commands

| Command | Description |
|---------|-------------|
| `bun run dev` | Start dev server |
| `bun run build` | Production build |
| `bun run start` | Start production server |
| `bun run atlas -- init` | Generate semantic layer from database |
| `bun run atlas -- init --demo` | Load simple demo dataset |
| `bun run atlas -- init --demo cybersec` | Load cybersec demo (62 tables) |
| `bun run atlas -- diff` | Compare DB schema vs semantic layer |
| `bun run atlas -- query "question"` | Headless query (table output) |
| `bun run test` | Run tests |

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `ATLAS_PROVIDER` | Yes | LLM provider (`anthropic`, `openai`, `bedrock`, `ollama`, `openai-compatible`, `gateway`) |
| Provider API key | Yes | e.g. `ANTHROPIC_API_KEY=sk-ant-...` |
| `ATLAS_DATASOURCE_URL` | Yes | Analytics database connection string |
| `DATABASE_URL` | No | Atlas internal Postgres (auth, audit). Auto-set on most platforms |
| `ATLAS_MODEL` | No | Override the default LLM model |
| `ATLAS_ROW_LIMIT` | No | Max rows per query (default: 1000) |

See `docs/deploy.md` for the full variable reference.

## Learn More

- [Atlas Documentation](https://www.useatlas.dev)
- [GitHub](https://github.com/AtlasDevHQ/atlas)
