---
name: riot-save-version
description: Handle save and publish intents for Product-Incubation repos by staging changes, creating a commit, and pushing to origin main. Use when a user says "save this version", "commit this", "publish changes", or similar wording.
---

# Riot Save Version

Use with:
- `docs/WINDSURF-INTENT-CONTRACT.md`

## Workflow

1. Validate this is a Product-Incubation repo.
Check `git remote get-url origin` and continue only if it points to `gh.riotgames.com/Product-Incubation/...`.

2. Capture the working state.
Run `git status --short` and summarize what will be committed.

3. Stage all local changes for the checkpoint.
Run `git add -A`.

4. Create a commit.
Use the user-specified message when provided. Otherwise use `chore: save version`.

5. Push to `main`.
Run `git push origin HEAD:main`.

6. Report the result.
Return the commit SHA and branch.

## Guardrails

- Do not force-push.
- If there is no `origin` remote, stop and ask to configure it first.
- If there are no changes, report "nothing to commit" and stop.
- If push fails due auth/permissions, surface the git error and next required action.
