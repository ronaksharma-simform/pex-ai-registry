---
name: estimation-sheet
description: Generate a professional project estimation workbook with task breakdown
stage: estimation
triggers:
  - estimate this
  - how many hours
  - create estimation
  - task breakdown
  - price this project
  - estimation sheet
  - effort estimate
prerequisites:
  - docx
output_format: xlsx
version: 0
---

# Estimation Sheet Skill

## Overview

Generates a formula-driven project estimation Excel workbook from a PRD or project description. Includes task decomposition, complexity multipliers, QA/PM ratios, and optional PexAI savings percentages.

## Prerequisites

- Read PRD and user stories for accurate scope.
- Apply document formatting guidelines from docx skill.

## Workflow

1. Perform gap analysis to identify missing requirements
2. Run commercial qualification checks
3. Decompose into right-sized tasks (10-60 hours typical)
4. Apply complexity multipliers per task category
5. Calculate QA allocation (15-25% of dev hours)
6. Calculate PM allocation (10-15% of total)
7. Apply PexAI savings percentage where applicable
8. Build formula-driven Excel with summary and detail sheets
9. Validate totals and cross-check with similar projects

## Reference Files

- `references/gap-analysis.md` — Gap analysis question framework
- `references/commercial-guard.md` — Commercial qualification criteria
- `references/task-decomposition.md` — Task sizing guidelines
- `references/excel-builder.md` — Excel structure specification

## Quality Gates

- [ ] All user stories/requirements have corresponding tasks
- [ ] Task estimates are between 4-60 hours (no oversized tasks)
- [ ] QA and PM ratios are within standard ranges
- [ ] Formulas calculate correctly
- [ ] Three scenarios provided (optimistic, realistic, pessimistic)
- [ ] Summary sheet shows total effort, cost, and timeline

## Output Format

Save as `{ProjectName}_Estimation_v{Version}.xlsx` in the outputs directory.
