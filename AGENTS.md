# Product-Incubation Agent Contract

Use with:
- `docs/WINDSURF-INTENT-CONTRACT.md`
- `docs/WINDSURF-QUICKSTART.md`
- `docs/PRODUCT-INCUBATION-DEPLOY.md`

Canonical user intents:
1. `save this version`
- stage all changes, commit once, push `HEAD` to `origin/main`

2. `deploy this app`
- deploy through manual relay using `aws-coolify-setup/scripts/riot-coolify-deploy-via-gateway.ps1`
- relay can auto-bootstrap first deploy when `coolify.appUuid` is missing
- first bootstrap requires GitHub repo-admin rights (deploy key + config commit)

3. `what is my app url?`
- read `riot.config.json` (`coolify.domain` fallback `metadata.data.deploy-url`)

## Next.js Rule

This template targets modern Next.js behavior. Validate assumptions against project docs before making framework-level changes.
