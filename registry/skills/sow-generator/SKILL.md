---
name: sow-generator
description: Generates a professional, client-ready Statement of Work (SOW) as a branded .docx document — business-focused scope, deliverables, and assumptions with no tech stack or pricing details
stage: discovery
triggers:
  - create a sow
  - create sow
  - generate a sow
  - generate sow
  - write a sow
  - write sow
  - statement of work
  - draft a statement of work
  - sow document
  - sow for this project
prerequisites: []
output_format: docx
version: 0
---

## Overview

Produces a polished, business-focused Statement of Work for client review. The SOW
describes WHAT will be built (scope, deliverables, assumptions) — never HOW (no tech
stack, frameworks, or architecture) and never pricing (estimation is a separate skill).

## Workflow

1. Read the project context (problem statement, assumptions, any discovery artifacts).
2. Write an Executive Summary framing the engagement in business terms.
3. Define Objectives and In/Out of Scope boundaries.
4. Write Feature Micro-Statements per module: `<Module> — <Feature>: <WHO does WHAT and OUTCOME>`.
5. List high-level Deliverables (interfaces/channels, not granular screens).
6. Call out Assumptions and open items as `[Details to be confirmed]` rather than fabricating them.
7. Save the document as a .docx via the artifact tools.

## Quality Gates

- [ ] No tech stack, framework, tool, or architecture details anywhere in the document
- [ ] No estimation, hours, or pricing content
- [ ] Every feature follows the Micro-Statement format
- [ ] Unknown details are marked `[Details to be confirmed]`, not invented
- [ ] Deliverables listed at the interface/channel level, not per-screen

## Output Format

Save as a branded `.docx` Statement of Work in the outputs directory.
