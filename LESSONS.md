# LESSONS.md

Recurring mistakes and how to avoid them. Read before starting work; add an entry when a mistake repeats.

## Frontend lint has no config
`frontend/package.json` declares `npm run lint` (ESLint), but no `.eslintrc*`/`eslint.config.*` is checked into the repo, so the command errors immediately. Don't rely on it as a working gate until a config is added; use `npm run build` (runs `vue-tsc`) as the available type-check instead.

## Backend has no test suite or linter
There is no `pytest`/`ruff`/`black`/`flake8` configuration in this repo. Don't assume a `test`/`lint` command exists for the backend — the closest available quick check is `python -m compileall backend -q`.
