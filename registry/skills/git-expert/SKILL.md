---
name: git-expert
description: Manage git workflow including branch creation, commit messages, pull requests, and code pushes following standard development practices
stage: devops
triggers:
  - git
  - branch
  - commit
  - push code
  - pull request
  - create PR
  - merge
  - git workflow
  - version control
  - branch management
  - push to git
  - create branch
prerequisites: []
output_format: code
version: 0
---

# Git Expert Skill

## Overview

Enforces a disciplined git workflow for development agents. Handles branch creation per task, conventional commit messages, code pushes, and pull request generation. Ensures every development activity follows a traceable, reviewable, and standards-compliant version control process.

## Prerequisites

- The project must be a git repository (`.git/` directory exists).
- A remote origin must be configured for push and PR operations.
- The GitHub CLI (`gh`) must be available for pull request creation.

## Branch Naming Convention

Create branches using the pattern: `<type>/<ticket-or-short-description>`

| Type        | When to use                                 | Example                          |
| ----------- | ------------------------------------------- | -------------------------------- |
| `feature/`  | New functionality                           | `feature/user-authentication`    |
| `fix/`      | Bug fixes                                   | `fix/login-redirect-loop`        |
| `hotfix/`   | Urgent production fixes                     | `hotfix/payment-null-crash`      |
| `chore/`    | Maintenance, deps, config                   | `chore/upgrade-node-20`          |
| `refactor/` | Code restructuring without behaviour change | `refactor/extract-auth-service`  |
| `docs/`     | Documentation only                          | `docs/api-endpoint-readme`       |
| `test/`     | Adding or updating tests                    | `test/payment-integration-tests` |

Rules:

- All lowercase, hyphens as separators — no spaces, underscores, or uppercase.
- If a ticket ID is available, prefix the description: `feature/PROJ-123-user-auth`.
- Branch from `main` (or the project's default branch) unless instructed otherwise.

## Workflow

### 1. Start a New Task — Create Branch

```
git checkout main
git pull origin main
git checkout -b <type>/<description>
```

- Always pull the latest default branch before branching.
- One branch per task — never reuse branches across unrelated work.

### 2. Stage and Commit — Conventional Commits

Use the **Conventional Commits** format for every commit message:

```
<type>(<scope>): <short summary>

<optional body — explain WHY, not WHAT>

<optional footer — ticket refs, breaking changes>
```

**Commit types** (matching branch types):

| Type       | Purpose                     |
| ---------- | --------------------------- |
| `feat`     | New feature                 |
| `fix`      | Bug fix                     |
| `docs`     | Documentation only          |
| `style`    | Formatting, no logic change |
| `refactor` | Code restructuring          |
| `test`     | Adding or updating tests    |
| `chore`    | Build, tooling, deps        |
| `perf`     | Performance improvement     |
| `ci`       | CI/CD configuration         |

Rules:

- Summary line: imperative mood, lowercase, no period, max 72 characters.
- Body: wrap at 72 characters. Explain motivation and contrast with previous behaviour.
- Footer: reference tickets (`Refs: PROJ-123`), note breaking changes (`BREAKING CHANGE: ...`).
- Stage specific files — never use `git add .` or `git add -A` blindly. Review what is staged.
- Do not commit secrets, `.env` files, credentials, or large binaries.

**Example commit:**

```
feat(auth): add JWT refresh token rotation

Refresh tokens are now rotated on each use and old tokens are
invalidated. This closes the replay-attack window from the
previous static-token implementation.

Refs: PROJ-456
```

### 3. Push Branch to Remote

```
git push -u origin <branch-name>
```

- Push early and often to avoid large, hard-to-review diffs.
- Always use `-u` on first push to set upstream tracking.

### 4. Create Pull Request

Use `gh pr create` to open the PR against the default branch:

```
gh pr create \
  --title "<type>(<scope>): <short summary>" \
  --body "$(cat <<'EOF'
## Summary
<1-3 bullet points describing what changed and why>

## Changes
- <file-level or module-level change descriptions>

## Test Plan
- [ ] <how to verify the changes work>

## Checklist
- [ ] Code follows project conventions
- [ ] No secrets or credentials committed
- [ ] Tests added/updated for new behaviour
- [ ] Documentation updated if applicable

Refs: <ticket-id if available>
EOF
)"
```

Rules:

- PR title follows the same conventional commit format.
- Summary explains the **why**, not just the what.
- Include a test plan so reviewers know how to verify.
- Keep PRs focused — one logical change per PR.
- If the PR is large, note which files are most important to review.

### 5. Post-PR Maintenance

- Address review comments with follow-up commits (do not force-push unless requested).
- After approval and merge, delete the remote branch:
  ```
  git push origin --delete <branch-name>
  ```
- Switch back to `main` and pull:
  ```
  git checkout main
  git pull origin main
  ```

## Decision Guide — When to Invoke This Skill

| Situation                               | Action                                   |
| --------------------------------------- | ---------------------------------------- |
| Starting a new development task         | Create a new branch (Step 1)             |
| Code changes are ready to save          | Stage specific files and commit (Step 2) |
| Want to back up work or share progress  | Push to remote (Step 3)                  |
| Development task is complete            | Create a PR (Step 4)                     |
| PR is merged                            | Clean up branch (Step 5)                 |
| Need to fix something on an existing PR | Commit and push to the same branch       |
| Urgent production bug                   | Use `hotfix/` branch, fast-track PR      |

## Quality Gates

- [ ] Branch created from latest default branch with correct naming convention
- [ ] Each commit follows conventional commit format
- [ ] No secrets, `.env`, credentials, or large binaries committed
- [ ] Specific files staged — no blind `git add .`
- [ ] Branch pushed with upstream tracking set
- [ ] PR created with summary, changes, test plan, and checklist
- [ ] PR targets the correct base branch
- [ ] Branch cleaned up after merge

## Error Handling

- **Merge conflicts:** Do not force-push or discard changes. Resolve conflicts, test, then commit the resolution.
- **Failed pre-commit hooks:** Fix the underlying issue, re-stage, and create a new commit — never skip hooks with `--no-verify`.
- **Detached HEAD:** Checkout the correct branch before committing.
- **Accidentally committed to main:** Create a branch from current HEAD, reset main to origin, then push the new branch.

## Anti-Patterns to Avoid

- Committing directly to `main` or `master`.
- Using `git push --force` without explicit instruction.
- Amending published commits.
- Giant PRs covering multiple unrelated changes.
- Vague commit messages like "fix", "update", "wip".
- Committing generated files, `node_modules`, or build artifacts.
