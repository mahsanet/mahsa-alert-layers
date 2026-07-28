# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Keeping this file current

When a change contradicts or extends anything documented here (or in `.claude/skills/`), update the doc **in the same commit** as the code change. Stale sections cost real debugging time — treat a doc that disagrees with the code as a bug.

## Commit author convention (MANDATORY)

Every commit in this repo must be authored as **`MahsaAlert <noreply@mahsaalert.com>`** — never a personal identity. The commit message itself can be normal.

```bash
git commit --author="MahsaAlert <noreply@mahsaalert.com>" -m "..."
# or set it once for this repo:
git config user.name "MahsaAlert" && git config user.email "noreply@mahsaalert.com"
```

The automated publisher already commits with this identity; manual commits must match it.

## What this repo is

Public open-data repo (CC BY 4.0) — no code. It holds:

- **~35 GeoJSON files at the root**, one `FeatureCollection` per map layer (`newTargets`, `basijBase`, `cameraPoint`, …).
- **`state.json`** — publish manifest: `lastUpdated` plus per-layer git blob SHA.
- **`README.md`** — the feature schema and layer catalog.

## How it gets updated — do NOT hand-edit the data

An automated backend job exports layers from the production database daily and commits directly to `main` via the GitHub API, skipping unchanged layers by blob-SHA comparison. Data commits follow the format `data: YYYY-MM-DD (N layers changed)`.

Consequences:

- **Never hand-edit the `.geojson` files or `state.json`** — the next nightly export overwrites them. Data fixes go into the production database (via the dashboard or backend SQL); this repo just mirrors it.
- Manual commits are appropriate only for docs (README, this file, license).

## Consumers

- Public open-data users (the repo is the published dataset).
- The team's internal report-verification tooling, which compares new reports against these layer sources.
