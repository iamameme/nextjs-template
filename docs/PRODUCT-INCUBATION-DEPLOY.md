# Product-Incubation Deploy Flow

This repository uses a manual deploy gateway contract:

- Save intent: commit and push to `main`
- Deploy intent: call the Coolify manual relay (`POST /deploy/manual`)

For non-technical prompts, see:
- `docs/WINDSURF-QUICKSTART.md`
- `docs/WINDSURF-INTENT-CONTRACT.md`

## Prerequisites

1. Repo is hosted in:
`gh.riotgames.com/Product-Incubation/<repo-name>`

2. `riot.config.json` includes:
- `coolify.appUuid`
- user-facing URL in `coolify.domain` or `metadata.data.deploy-url`

If missing, relay can bootstrap these values on first deploy.

3. Manual relay endpoint is available:
- env `COOLIFY_MANUAL_GATEWAY_URL` set to relay base URL
- relay can reach Coolify API

4. User auth for deploy trigger:
- `gh` authenticated to `gh.riotgames.com`
- repo read access in `Product-Incubation`
- for first bootstrap: repo-admin rights to manage deploy keys and commit config

Note: users do not need local `COOLIFY_*` credentials for deploys through the relay.

## User Deploy Trigger (Preferred)

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File `
  <path-to-aws-coolify-setup>\scripts\riot-coolify-deploy-via-gateway.ps1 `
  -TargetRepoPath "C:\path\to\repo"
```

The script resolves `Product-Incubation/<repo>` from git origin, sends your GitHub token to the relay, and prints:
- `run_id`
- `deployment_uuid`
- status URL
- app URL

On first deploy, it can also bootstrap app wiring and commit `riot.config.json` when permissions allow.

## Operator Onboarding / Validation

Use this once per repo (or after config drift) to validate `coolify.appUuid` and optional metadata:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File `
  <path-to-aws-coolify-setup>\scripts\riot-coolify-onboard-manual-gateway.ps1 `
  -TargetRepoPath "C:\path\to\repo" `
  -SetDeployProvider
```

Operator end-to-end check (health + onboarding + dry-run + real deploy):

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File `
  <path-to-aws-coolify-setup>\scripts\riot-coolify-manual-gateway-operator.ps1 `
  -TargetRepoPath "C:\path\to\repo"
```

## Local Direct Fallback (Operator Only)

Use direct local deploy only for troubleshooting:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File `
  <path-to-aws-coolify-setup>\scripts\riot-coolify-deploy.ps1 `
  -ConfigPath riot.config.json `
  -DryRun
```
