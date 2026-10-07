---
name: presentation-generator
description: Generate interactive HTML slide deck presentations for project delivery and client demos
stage: delivery
triggers:
  - presentation
  - generate presentation
  - project presentation
prerequisites: []
output_format: html
version: 0
---

# Presentation Generator Skill

## Overview

Generates an interactive HTML slide deck presentation summarizing the project for client delivery, sprint reviews, or stakeholder demos. Includes inline CSS and JavaScript for a self-contained, portable file.

## Prerequisites

- Read all project artifacts (PRD, design, estimation, test plan) for comprehensive coverage.
- Gather project metrics (artifacts count, stages completed, estimation data).

## Workflow

1. Collect project summary, goals, and key decisions
2. Summarize architecture and technology choices
3. Include estimation highlights and timeline
4. Present key deliverables and artifacts produced
5. Generate HTML slide deck with inline CSS and JavaScript
6. Ensure slides are navigable with keyboard arrows
7. Validate HTML structure, styles, and scripts are present

## Quality Gates

- [ ] Valid HTML document with DOCTYPE
- [ ] Inline CSS styles (no external stylesheets)
- [ ] Inline JavaScript for slide navigation
- [ ] Project overview slide with goals
- [ ] Architecture/technology slide
- [ ] Timeline/estimation slide
- [ ] Deliverables summary slide
- [ ] Professional visual design

## Output Format

Save as `{ProjectName}_Presentation_v{Version}.html` in the outputs directory.
