# harvest-flow-mscsy0104-notes

Personal runtime repository for blogging and dashboard operation.

## What this repo contains

- Personal `.env` values and runtime config
- Personal note source and Quartz content/theme assets
- Thin runner scripts for engine/dashboard

## Dependency strategy

This repository depends on:

- `harvest-flow` (open-source app package), or
- `harvest-flow-core` + your own app wiring

## Git tracking policy

- Commit: note source and Quartz source/theme files.
- Do not commit: qdrant data, logs, sqlite DB files, model caches, and local secrets.
- Cache/runtime data should stay under `data/` and remain git-ignored.

## Quick Start

```bash
cp .env.example .env
uv sync --all-extras
bash scripts/run_engine.sh
```

In another terminal:

```bash
bash scripts/run_dashboard.sh
```

## Ollama Preflight

When Docker and local Ollama are both running, `localhost:11434` can resolve to a different service.
Use `127.0.0.1` in `.env` for stable local routing.

```bash
curl -s http://127.0.0.1:11434/api/tags
ollama pull gemma2:2b
ollama pull nomic-embed-text
```

