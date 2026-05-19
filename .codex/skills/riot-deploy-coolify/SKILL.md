---
name: riot-deploy-coolify
description: Handle deploy and URL intents for Product-Incubation apps through the manual Coolify deploy relay, including first-time bootstrap when appUuid is missing.
---

# Riot Deploy Coolify

Use with:
- `docs/WINDSURF-INTENT-CONTRACT.md`

## Required Inputs

- Repo is in `gh.riotgames.com/Product-Incubation/*`.
- Manual relay URL is available (`COOLIFY_MANUAL_GATEWAY_URL`).
- Caller is authenticated to `gh.riotgames.com` (`gh auth` or token env).

Read `references/required-env.md` before deploy actions.

## Workflow

1. Confirm git state.
If local changes are uncommitted, recommend running the save-version flow first.

2. Deploy via manual relay (preferred, no local Coolify creds).
Run:
`aws-coolify-setup/scripts/riot-coolify-deploy-via-gateway.ps1`

3. First-time bootstrap handling.
- If relay response indicates first bootstrap occurred, report app UUID and deploy URL.
- If relay returns `first_bootstrap_requires_repo_admin`, explain that first deploy needs repo-admin rights (GitHub deploy key + riot.config commit), then stop.

4. Fallback operator mode (only when relay path is unavailable or explicitly requested).
Run:
`aws-coolify-setup/scripts/riot-coolify-deploy.ps1`

5. Return deployment URL.
Use `coolify.domain` from `riot.config.json` if present, else `metadata.data.deploy-url`.

## Guardrails

- Do not request local Coolify credentials for standard user deploy flow.
- Use direct local deploy mode only for operator troubleshooting.
- Do not rotate credentials or mutate global machine config.
- Prefer `-DryRun` for mock/practice flows.
