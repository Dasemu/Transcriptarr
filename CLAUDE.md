# CLAUDE.md

## Overview
Transcriptarr: AI-powered subtitle transcription service. FastAPI backend (Whisper/faster-whisper/stable-ts transcription, worker pool, SQLite/PostgreSQL/MariaDB) with a Vue 3 + TypeScript web UI.

## Commands
- Backend install: `pip install -r requirements.txt`
- Backend run (dev): `python backend/cli.py server --reload`
- Backend run (prod): `python backend/cli.py server --host 0.0.0.0 --port 8000 --workers 4`
- Backend quick check (no test suite exists yet): `python -m compileall backend -q`
- Frontend install: `cd frontend && npm install`
- Frontend dev: `cd frontend && npm run dev`
- Frontend build (also type-checks via vue-tsc): `cd frontend && npm run build`
- Frontend lint: `cd frontend && npm run lint` — script exists but no ESLint config file is checked in, so it currently errors; see LESSONS.md.

## Architecture
FastAPI backend under `backend/` (API routers in `backend/api`, core services in `backend/core`, scanning in `backend/scanning`, transcription in `backend/transcription`), Vue 3 SPA under `frontend/`. See `docs/ARCHITECTURE.md`, `docs/API.md`, `docs/CONFIGURATION.md`, `docs/FRONTEND.md`.

## Conventions
- Only `DATABASE_URL` is read from the environment (`backend/config.py`); all other settings live in the database and are managed via the Settings API/UI.
- Keep `.env.example` limited to variable names actually read from the environment.

## Workflow quirks
- No backend linter/formatter (ruff/black/flake8) and no automated test suite (pytest/vitest) are configured yet. Do not assume `npm run lint` passes — it has no config.
- Single `frontend/package.json` version field; there is no root `package.json`/`pyproject.toml`, so the release workflow tracks the version in the root `VERSION` file.

- CI runs on both Gitea (`.gitea/workflows/ci.yml`) and GitHub (`.github/workflows/ci.yml`); keep them in sync. Versioning and the Gitea release (`version.yml`) exist only under `.gitea/workflows/`; the GitHub release (`.github/workflows/release.yml`) is created when the `v*` tag reaches GitHub.

## Deployment
Not yet documented here; no deployment workflow exists in this repo.

## Gotchas
- `models/`, `transcriptarr.db`, and `.env` are gitignored — expected to be created at runtime, not committed.
