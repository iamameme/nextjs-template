# Required Environment

## Standard User Mode (Preferred)

No local `COOLIFY_*` variables are required.

Requirements:
- `gh` authenticated to `gh.riotgames.com`
- GitHub repo access in `Product-Incubation`
- `COOLIFY_MANUAL_GATEWAY_URL` set for the relay endpoint
- For first deploy bootstrap: caller must have GitHub repo-admin rights (deploy key management + commit to `main`)

## Operator Validation / Onboarding

Use shared machine-ops credentials file from `aws-coolify-setup`:
- `.\.machine-ops.env` with `COOLIFY_BASE_URL` and `COOLIFY_TOKEN` (or `COOLIFY_KEY`)
- Optional override: `-MachineOpsEnvFile`

Optional:
- `COOLIFY_MANUAL_GATEWAY_URL` (if not passed directly to scripts)

## Operator Direct Deploy Fallback

Set these locally before direct deploy actions:
- `COOLIFY_BASE_URL`
- `COOLIFY_TOKEN` (or `COOLIFY_KEY`)
- `COOLIFY_SERVER_UUID` (required on first create)
- `COOLIFY_DOMAIN_ROOT` (required on first create when domain is not set)

Optional:
- `COOLIFY_PROJECT_UUID`
- `COOLIFY_ENVIRONMENT_NAME`
- `COOLIFY_PRIVATE_KEY_UUID` (recommended for `gh.riotgames.com` private repos)
- `COOLIFY_GIT_REPOSITORY`
- `COOLIFY_GIT_BRANCH`
- `COOLIFY_BUILD_PACK`
