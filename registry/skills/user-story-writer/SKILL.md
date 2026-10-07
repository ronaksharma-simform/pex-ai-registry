---
name: user-story-writer
description: Generate structured user stories with acceptance criteria from a PRD or project brief
stage: discovery
triggers:
  - write stories
  - user stories
  - acceptance criteria
  - break this down into stories
  - create stories
  - generate stories
  - backlog items
prerequisites:
  - docx
output_format: md
version: 0
---

# User Story Writer Skill

## Overview

Generates structured user stories with acceptance criteria, edge cases, and priority assignments from a PRD or project brief. Stories follow the "As a [persona], I want [action], so that [benefit]" format.

## Prerequisites

- Read existing PRD content if available for requirements traceability.

## Workflow

1. Identify all functional requirements from the PRD or brief
2. Map requirements to user personas
3. Write user stories in standard format
4. Define acceptance criteria for each story (minimum 3 per story)
5. Identify edge cases and error scenarios
6. Assign priority using MoSCoW method
7. Estimate story points (Fibonacci: 1, 2, 3, 5, 8, 13)
8. Validate coverage against original requirements

## Reference Files

- `references/story-format.md` — User story format specification

## Quality Gates

- [ ] Minimum 8 user stories generated
- [ ] Each story has 3+ acceptance criteria
- [ ] Stories cover all functional requirement areas
- [ ] MoSCoW priorities assigned to every story
- [ ] Edge cases identified for critical flows
- [ ] Story points reflect relative complexity

## Output Format

Save as `{ProjectName}_UserStories_v{Version}.md` in the outputs directory.
