---
name: github-issues
description: Create GitHub issues from user stories or task breakdowns with labels and acceptance criteria
stage: delivery
triggers:
  - create issues from stories
  - create github issues
  - create tickets
  - push stories to github
  - create issues
  - generate github issues
prerequisites: []
output_format: md
version: 0
---

## Overview

The GitHub Issues skill enables the delivery agent to create GitHub issues from user stories, task breakdowns, or feature lists. Each issue includes acceptance criteria, priority labels, and story point estimates.

## Workflow

1. **Read User Stories**: Load user stories from project context or artifacts
2. **Create Issues**: For each story, create a GitHub issue with:
   - Title: Story title
   - Body: Full acceptance criteria, edge cases, and technical notes
   - Labels: Priority (must/should/could), type (feature/bug/chore)
   - Story points as a label or in the body
3. **Report Results**: Return all created issue URLs

## Prerequisites

- GitHub repository must be configured in the project settings
- User stories must exist in the project context (from the discovery stage)

## Quality Gates

- Each issue has a clear title and acceptance criteria
- Priority labels are applied correctly (must/should/could)
- Issues are linked to the correct repository
- No duplicate issues created
