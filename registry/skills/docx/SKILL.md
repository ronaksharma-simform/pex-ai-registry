---
name: docx
description: Document formatting guidelines and standards for all generated documents
stage: documentation
triggers:
  - format document
  - document guidelines
  - formatting standards
prerequisites: []
output_format: docx
version: 0
---

# Document Formatting Skill

## Overview

Provides consistent document formatting guidelines used by all document-producing skills. This skill is a prerequisite for PRD generation, solution design, and other skills that produce formatted documents.

## Workflow

1. Apply standard heading hierarchy (H1 for title, H2 for sections, H3 for subsections)
2. Use consistent bullet and numbering styles
3. Include table of contents for documents exceeding 5 pages
4. Apply professional font and spacing standards
5. Ensure all tables have headers and consistent formatting

## Reference Files

- `references/formatting-guidelines.md` — Complete formatting specification

## Quality Gates

- [ ] Heading hierarchy is consistent throughout
- [ ] Tables have headers and consistent column widths
- [ ] Font sizes follow the standard scale
- [ ] Page margins and spacing are uniform

## Output Format

Apply these guidelines to all `.docx` output files.
