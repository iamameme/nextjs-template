# Windsurf Quickstart (Non-Technical)

This file is for project owners using Windsurf.

Canonical behavior:
- `docs/WINDSURF-INTENT-CONTRACT.md`

## What You Say

Use these exact phrases:

1. `save this version`
Result: AI commits current changes and pushes to `main`.

2. `deploy this app`
Result: AI calls the manual relay deploy endpoint for this repo.

3. `what is my app url?`
Result: AI returns the URL from `riot.config.json`.

## What Must Already Exist

- Repo is under `Product-Incubation` in GitHub Enterprise.
- Relay URL is configured (`COOLIFY_MANUAL_GATEWAY_URL`) in the environment used by scripts/agent.
- User is authenticated to `gh.riotgames.com`.
- For first deploy bootstrap: user has repo-admin rights (deploy keys + commit to `main`).

You do not need local `COOLIFY_*` credentials on your machine for standard deploy.

## First-Time Setup

If this repo came from the Product-Incubation template and already has `docs/`, `.codex/skills/`, and `AGENTS.md`, no extra bootstrap command is required.

Just run:
- `save this version`
- `deploy this app`

For operators running from terminal, guided runner:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File `
  <path-to-aws-coolify-setup>\scripts\riot-coolify-guided-flow.ps1 `
  -TargetRepoPath "C:\path\to\repo"
```

Deploy from terminal without local Coolify credentials:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File `
  <path-to-aws-coolify-setup>\scripts\riot-coolify-deploy-via-gateway.ps1 `
  -TargetRepoPath "C:\path\to\repo"
```

If this is the first deploy and `riot.config.json` is missing `coolify.appUuid`, relay will bootstrap it automatically when permissions allow.
