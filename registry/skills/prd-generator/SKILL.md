---
name: prd-generator
description: Generate a comprehensive PRD from a project brief
stage: discovery
triggers:
  - create prd
  - write prd
  - product requirements
  - product spec
  - requirements document
  - generate prd
  - create a prd
prerequisites:
  - docx
output_format: docx
version: 0
---

# PRD Generator Skill

## Overview

Generates a 12+ section Product Requirements Document from a project brief. The PRD serves as the foundation for all downstream SDLC activities including user story generation, architecture design, and estimation.

## Prerequisites

- Always read `docx/SKILL.md` first for document formatting guidelines.

## Workflow

1. Extract key information from the project brief
2. Identify target users and create detailed personas
3. Define functional requirements by feature area
4. Specify non-functional requirements (performance, security, scalability)
5. Document integrations and external dependencies
6. Define scope boundaries (in-scope vs out-of-scope)
7. Establish success metrics and KPIs
8. Apply formatting guidelines from docx skill
9. Validate completeness against quality gates

## Reference Files

- `references/prd-template.md` — Section template with guidance
- `references/quality-checklist.md` — Validation checklist

## Quality Gates

- [ ] All 12 sections present with substantive content
- [ ] Requirements are specific and testable
- [ ] At least 3 user personas defined
- [ ] Non-functional requirements cover 4+ categories
- [ ] In-scope and out-of-scope clearly differentiated
- [ ] Success metrics are quantifiable

## Output Format

Save as `{ProjectName}_PRD_v{Version}.docx` in the outputs directory.
