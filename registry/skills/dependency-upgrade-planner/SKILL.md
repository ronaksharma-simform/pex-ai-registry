---
name: dependency-upgrade-planner
description: Plans a safe dependency upgrade. Reads the manifest and lockfile, groups outdated packages by risk, and proposes an ordered upgrade plan with a rollback step. Use when asked to update, bump or audit project dependencies.
metadata:
  version: "1.0.0"
---

# Dependency Upgrade Planner

Produce an upgrade plan. Do not change any file unless the user asks for it after reading the plan.

## Steps

1. **Find the manifests.** Locate every `package.json`, `requirements.txt`, `pom.xml`, `go.mod` or
   equivalent, and the lockfile next to it. Note the package manager and its version.
2. **List what is outdated.** Run the project's own outdated command (for example `pnpm outdated`).
   Record current, wanted and latest versions for each package.
3. **Group by risk.** Put each package in one group, using `references/risk-checklist.md`:
   patch and minor bumps, major bumps, packages with breaking-change notes, and packages that are
   security fixes.
4. **Order the work.** Security fixes first, then patch and minor bumps together, then one major bump
   at a time. Packages that depend on each other move in the same step.
5. **Write the plan.** For each step give the packages, the exact command, the tests to run, and what
   a failure looks like.
6. **Add a rollback.** State how to return to the previous lockfile (a git revert of the upgrade
   commit) and what to check afterwards.

## Output

A numbered plan the user can approve step by step. Keep it short: one line per package, grouped by
step. Say plainly when a package could not be assessed.
