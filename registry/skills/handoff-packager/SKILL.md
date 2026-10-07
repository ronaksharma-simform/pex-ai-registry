---
name: handoff-packager
description: Package all project artifacts into a structured handoff archive for client delivery
stage: delivery
triggers:
  - handoff package
  - delivery package
  - package artifacts
  - client handoff
  - project handoff
  - create handoff
prerequisites: []
output_format: code
version: 0
---

# Handoff Packager Skill

## Overview

Collects and packages all project artifacts into a structured ZIP archive for client delivery. Includes a manifest index, README, and organized folder structure by SDLC stage.

## Prerequisites

- All upstream stages should be completed for a comprehensive package.
- Read artifact inventory from project context.

## Workflow

1. Inventory all artifacts produced across SDLC stages
2. Organize artifacts into stage-based folder structure
3. Generate a README with package contents and usage guide
4. Create a manifest index listing all artifacts with metadata
5. Bundle Git workspace information if available
6. Package everything into a ZIP archive

## Quality Gates

- [ ] All produced artifacts included in package
- [ ] Organized folder structure by SDLC stage
- [ ] README with overview and contents listing
- [ ] Manifest index with artifact metadata (name, type, stage, size)
- [ ] No sensitive credentials included in package
- [ ] ZIP archive is valid and complete

## Output Format

Save as `{ProjectName}_Handoff_v{Version}.zip` in the outputs directory.
