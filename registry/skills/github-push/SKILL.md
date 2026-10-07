---
name: github-push
description: Push generated code and artifacts to a GitHub repository with proper branching and commit messages
stage: delivery
triggers:
  - push to github
  - create repo
  - create repository
  - push the code
  - push scaffold to github
  - push to git
  - publish to github
prerequisites: []
output_format: code
version: 0
---

## Overview

The GitHub Push skill enables the delivery agent to push generated project code, scaffolding, and artifacts to a GitHub repository. It leverages the git workspace provisioned by the orchestrator.

## Workflow

1. **Verify Git Workspace**: Ensure a git workspace is provisioned with the target repository
2. **Stage Artifacts**: Add all generated artifacts to the git staging area
3. **Create Commit**: Commit with a descriptive message following Conventional Commits format
4. **Push to Remote**: Push the branch to the remote repository
5. **Report Result**: Return the push result with branch name and commit SHA

## Prerequisites

- GitHub repository must be configured in the project settings
- Git workspace must be provisioned by the orchestrator

## Quality Gates

- No secrets or credentials committed
- Commit message follows Conventional Commits format
- Branch pushed with upstream tracking
