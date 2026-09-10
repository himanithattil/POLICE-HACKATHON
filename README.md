# Sentinel Command Console

Sentinel is an AI-assisted surveillance and monitoring command console. It brings together live camera feeds, license-plate/person detection, vehicle & person route intelligence, watchlists, and shareable access into a single dashboard — with the AI layer running **fully local and free via Ollama** (no mandatory paid API keys).

## Features

- **Operations dashboard** — command-center overview of live activity
- **Live Detection** — real-time detection feed (CCTV/image analysis)
- **Camera Registry** — manage and register monitored camera feeds
- **Watchlist** — track flagged vehicles/persons of interest
- **Route Intelligence** — reconstruct vehicle and person movement routes on a map, with verified-GPS vs. approximate-location handling
- **Data Intake** — ingest detection/event data into the system
- **Shared Access** — generate tokenized links for independent, app-native sharing of specific views (no third-party platform dependency)
- **Hackathon Readiness** — internal checklist/status view

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 19, Vite, TypeScript, Tailwind CSS, Radix UI, Wouter (routing), TanStack Query |
| Backend | Node.js, Express, tRPC |
| Database | MySQL (via Drizzle ORM) |
| AI | Ollama (local, free) — optional OpenAI/Anthropic fallback |
| Maps | OpenStreetMap (default, free) — optional Google Maps |
| Storage | S3-compatible object storage |
| Testing | Vitest |

## Prerequisites

- [Node.js](https://nodejs.org/) 18+
- [pnpm](https://pnpm.io/)
- A MySQL database (local or hosted)
- [Ollama](https://ollama.com/) installed locally, for free local AI inference

## Getting Started

1. **Clone the repo**
   ```bash
   git clone <your-repo-url>
   cd sentinel-project
   ```

2. **Install dependencies**
   ```bash
   pnpm install
   ```

3. **Configure environment variables**

   Copy the example file and fill in your values:
   ```bash
   cp .env.example .env
   ```

   | Variable | Description |
   |---|---|
   | `DATABASE_URL` | MySQL connection string |
   | `JWT_SECRET` | Secret used to sign session cookies |
   | `OLLAMA_ENABLED` | `true` to use local AI (recommended, free) |
   | `OLLAMA_BASE_URL` | Ollama server URL (default `http://127.0.0.1:11434`) |
   | `OLLAMA_MODEL` | Text model to use (default `qwen2.5:3b`) |
   | `OLLAMA_VISION_MODEL` | Vision model for CCTV/image analysis (default `qwen2.5vl:3b`) |
   | `OPENAI_API_KEY` / `ANTHROPIC_API_KEY` | Optional — use a paid provider instead of Ollama |
   | `VITE_GOOGLE_MAPS_API_KEY` | Optional — falls back to OpenStreetMap if omitted |

4. **Pull the Ollama models** (if using local AI)
   ```bash
   ollama pull qwen2.5:3b
   ollama pull qwen2.5vl:3b
   ```

5. **Set up the database**
   ```bash
   pnpm db:push
   ```

6. **Run in development**
   ```bash
   pnpm dev
   ```

7. **Build for production**
   ```bash
   pnpm build
   pnpm start
   ```

## Testing & Type Checking

```bash
pnpm check   # TypeScript type checking
pnpm test    # Run Vitest suite
```

## Deployment

This app is a full-stack Node service (Express serving the built React app + tRPC API), not a static site — it needs a host that runs a persistent Node process plus a MySQL database, such as **Railway** or **Render**. If you enable Ollama, you'll also need a machine capable of running the model (a plain serverless/static host won't support it); otherwise, switch to the `OPENAI_API_KEY` or `ANTHROPIC_API_KEY` fallback for a cloud-only deployment.

## License

MIT
