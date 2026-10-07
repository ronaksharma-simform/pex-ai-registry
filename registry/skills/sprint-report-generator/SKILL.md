---
name: sprint-report-generator
description: Generate sprint reports summarizing completed work, metrics, and next steps
stage: delivery
triggers:
  - sprint report
  - sprint summary
  - iteration report
  - progress report
  - sprint review
prerequisites:
  - docx
output_format: docx
version: 0
---

# Sprint Report Generator Skill

## Overview

Generates a sprint report document summarizing completed work, artifacts produced, metrics, blockers, and planned next steps. Suitable for stakeholder reviews and project tracking.

## Prerequisites

- Read project context for stage history and artifact inventory.
- Apply document formatting guidelines from docx skill.

## Workflow

1. Summarize sprint goals and scope
2. List completed stages and their outcomes
3. Inventory artifacts produced with types and sizes
4. Calculate velocity metrics (stages completed, artifacts created, time spent)
5. Document blockers and risks encountered
6. Define action items and next sprint goals
7. Format as professional report document

## Quality Gates

- [ ] Sprint goals and scope defined
- [ ] Completed work itemized by stage
- [ ] Artifact inventory with counts and types
- [ ] Velocity metrics included
- [ ] Blockers and risks documented
- [ ] Next steps and action items defined

## Output Format

Save as `{ProjectName}_Sprint_Report_v{Version}.docx` in the outputs directory.
