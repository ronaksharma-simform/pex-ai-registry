---
name: tech-overview-generator
description: Generate technical overview documents for client handoff with architecture and technology choices
stage: documentation
triggers:
  - tech overview
  - technical overview
  - client handoff
  - handoff doc
  - project overview
  - technology overview
prerequisites:
  - docx
output_format: docx
version: 0
---

# Tech Overview Generator Skill

## Overview

Generates a technical overview document suitable for client handoff, covering system architecture, technology choices with justification, security posture, performance characteristics, integrations, and support model.

## Prerequisites

- Read PRD and design artifacts if available for accurate context.
- Apply document formatting guidelines from docx skill.

## Workflow

1. Write executive system summary
2. Describe high-level architecture with component relationships
3. Create technology choices table with justifications
4. Document security measures and compliance considerations
5. Define performance characteristics and SLAs
6. List integrations and external dependencies
7. Describe support model and maintenance approach
8. Save as both markdown and docx artifacts

## Quality Gates

- [ ] System summary section present
- [ ] Architecture section with component descriptions
- [ ] Technology choices table (Component | Technology | Justification)
- [ ] Security section covering auth, encryption, and compliance
- [ ] Performance section with expected SLAs
- [ ] Integration section listing external systems
- [ ] Support model and maintenance approach defined

## Output Format

Save as `{ProjectName}_Technical_Overview_v{Version}.docx` in the outputs directory.
