---
name: solution-design
description: Create a professional Solution Design and Architecture Document
stage: architecture
triggers:
  - solution design
  - design the solution
  - architecture document
  - technical design
  - system design document
  - tech spec
  - design document
prerequisites:
  - docx
output_format: docx
version: 0
---

# Solution Design Skill

## Overview

Produces a comprehensive Solution Design & Architecture Document covering technical options, component design, NFR strategy, effort scenarios, and risk register. The document is structured for both technical and business stakeholders.

## Prerequisites

- Read PRD for requirements context.
- Apply document formatting guidelines from docx skill.

## Workflow

1. Review PRD and user stories for requirements context
2. Identify architectural drivers and constraints
3. Evaluate technology options with scored comparison
4. Design component-level architecture
5. Define integration patterns and data flow
6. Specify NFR strategy (performance, security, scalability)
7. Create effort estimation scenarios
8. Document risks with mitigation strategies
9. Apply formatting guidelines

## Reference Files

- `references/option-comparison-template.md` — Technology option scoring template
- `references/architecture-patterns.md` — Common architecture patterns reference

## Quality Gates

- [ ] 2+ technology options compared with scoring
- [ ] Component diagram described or referenced
- [ ] Integration points fully specified
- [ ] NFR strategy covers performance, security, scalability
- [ ] Risk register has 5+ entries with mitigations
- [ ] Effort scenarios cover optimistic/realistic/pessimistic

## Output Format

Save as `{ProjectName}_SolutionDesign_v{Version}.docx` in the outputs directory.
