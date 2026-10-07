---
name: code-review
description: Review one completed change (a diff) against what was asked for and the project's own conventions, reporting located, explained findings without modifying anything
stage: qa
triggers:
  - review this change
  - review the diff
  - review this diff
  - review the pull request
  - review completed work
  - review before merge
prerequisites: []
output_format: md
version: 0
---

# Code Review Skill

## Overview

Reviews a single completed change — the diff, not a summary of it — against the task's own
specification (description plus executed acceptance-criteria results) and the project's written
conventions (`CLAUDE.md`, `CONTEXT.md`, ADRs). Produces findings that name a file and line and
state the concrete failure, never edits: the owning agent is read-only by capability.

Distinct from `code-audit`, which sweeps a whole codebase across quality dimensions and produces a
report document. This skill judges one change.

This file is the registry/routing declaration only: the review runner builds the reviewer's prompt
from the `code-reviewer` agent manifest and does not load skill content, so the operational
procedure lives there and this workflow is its summary.

## Workflow

1. Read the diff, then the changed files for the context the diff hides
2. Check the change against the task description and each acceptance criterion's executed outcome
3. Check the change against written project conventions the touched files are subject to
4. Report each problem as a located finding with the concrete failure it causes, most severe first
5. Conclude: findings, or a plain statement that the change is sound

## Output

Findings with `{file, line, category, severity, summary, failureScenario, verdict}`, ordered most
severe first, plus a one-paragraph conclusion.
