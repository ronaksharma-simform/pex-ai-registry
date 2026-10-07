# Branch Strategy Reference

## Git Flow vs Trunk-Based Development

### Trunk-Based (Recommended for most projects)

- Single long-lived branch: `main`
- Short-lived feature branches (1-3 days max)
- Merge via PR with squash or merge commit
- Deploy from `main` after merge
- Best for: CI/CD-heavy teams, small-to-medium projects

### Git Flow (For projects with release cycles)

- Long-lived branches: `main`, `develop`
- Feature branches from `develop`
- Release branches for stabilization: `release/v1.2.0`
- Hotfix branches from `main`: `hotfix/critical-fix`
- Best for: versioned software, mobile apps, enterprise releases

## Branch Protection Rules (Recommended)

Configure on the default branch:

- Require pull request reviews (minimum 1 approval)
- Require status checks to pass (CI/CD)
- Require branches to be up to date before merging
- Do not allow force pushes
- Do not allow deletions

## Merge Strategies

| Strategy     | When to use                                      |
| ------------ | ------------------------------------------------ |
| Merge commit | Preserve full branch history                     |
| Squash merge | Clean linear history, one commit per PR          |
| Rebase merge | Linear history with individual commits preserved |

Default recommendation: **Squash merge** for feature branches to keep `main` history clean.

## Stale Branch Cleanup

- Delete remote branches after PR merge.
- Periodically prune local tracking branches: `git fetch --prune`
- Branches older than 30 days without activity should be reviewed and deleted.

## Tag and Release Convention

Use semantic versioning tags for releases:

```
git tag -a v1.2.0 -m "Release v1.2.0 — feature summary"
git push origin v1.2.0
```

- `vMAJOR.MINOR.PATCH` — e.g., `v1.2.0`
- Tag from `main` after merge, never from feature branches.
