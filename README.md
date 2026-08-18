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

### Pin/Update Rule

- Promote versions in fixed order: `harvest-flow-core` -> `harvest-flow` -> `harvest-flow-mscsy0104-notes`.
- Pin to tested app/core versions in `pyproject.toml` before running production-like workflows.
- Keep the previous known-good pin so rollback can be done quickly.

### Personal Smoke Runbook (Gate 3)

1. `uv sync --all-extras`
2. `bash scripts/run_engine.sh` and verify startup logs are healthy.
3. Move one sample note from review request to publish-ready stage.
4. `bash scripts/run_dashboard.sh` and verify dashboard + RAG menu loads.
5. Record pass/fail and version pins in personal release notes.

### Release/Rollback Ownership

- Core maintainer owns core tags and API notes.
- App maintainer owns app compatibility range and CI.
- Personal ops maintainer owns final pin update and smoke evidence in this repository.

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

