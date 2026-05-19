# Windsurf Intent Contract

This contract maps user language to exact operations.

## Supported User Intents

1. `save this version`
Action:
- Stage all changes.
- Create one commit.
- Push `HEAD` to `origin/main`.

2. `deploy this app`
Action:
- Ensure repo is in GitHub under `Product-Incubation`.
- Trigger manual relay deploy (`POST /deploy/manual`) with caller GitHub token and `auto_bootstrap=true`.
- If `riot.config.json.coolify.appUuid` is missing, relay bootstraps app/key wiring and commits config to `main`.
- Return deployment UUID, status URL, and app URL.
- If relay returns `first_bootstrap_requires_repo_admin`, stop and explain first bootstrap permission requirements.

3. `what is my app url?`
Action:
- Read URL from `riot.config.json` (`coolify.domain` fallback `metadata.data.deploy-url`).
- Return URL and latest known deploy state.

## Confirmation Rules

- Confirm before first-time GitHub repository creation.
- Confirm before first-time URL claim/deploy (`xxxxx.coolriotapps.com`).

## Standard Progress Stages

- Inspecting project
- Checking GitHub name
- Creating GitHub repo
- Checking URL availability
- Bootstrapping project
- Pushing to main
- Deploying to Coolify
- Verifying app URL
