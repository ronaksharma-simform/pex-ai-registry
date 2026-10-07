---
name: cicd-generator
description: Generate GitHub Actions CI/CD pipeline workflows for build, test, and deployment
stage: devops
triggers:
  - ci/cd
  - cicd
  - pipeline
  - github actions
  - deployment pipeline
  - ci cd pipeline
prerequisites: []
output_format: code
version: 0
---

# CI/CD Generator Skill

## Overview

Generates GitHub Actions workflow files for continuous integration (lint, test, build) and continuous deployment (staging and production) with PR checks.

## Prerequisites

- Read project tech stack to determine build tools and test runners.
- If Terraform artifacts exist, reference infrastructure for deployment targets.

## Workflow

1. Generate CI pipeline workflow (lint, test, build on push/PR)
2. Generate CD pipeline workflow (deploy to staging on merge, production on release)
3. Generate PR checks workflow (type check, test coverage, security scan)
4. Define environment secrets and variables needed
5. Use `# FILE: .github/workflows/<name>.yml` comment pattern in code blocks

## Quality Gates

- [ ] CI pipeline with lint, test, and build jobs
- [ ] CD pipeline with staging and production deployment
- [ ] PR checks workflow with quality gates
- [ ] No hardcoded secrets (use GitHub secrets references)
- [ ] Proper job dependencies and conditions
- [ ] Caching configured for dependencies

## Output Format

Save manifest as `{ProjectName}_CICD_v{Version}.md` in the outputs directory.
