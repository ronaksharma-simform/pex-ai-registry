---
name: frontend-scaffolding
description: Generate React frontend scaffolding with pages, API client, and routing
stage: development
triggers:
  - scaffold frontend
  - generate frontend
  - generate the frontend
  - create ui
  - react pages
  - frontend code
  - generate components
prerequisites:
  - docx
output_format: code
version: 0
---

# Frontend Scaffolding Skill

## Overview

Generates a complete React frontend scaffold including page components for all major user flows, a typed API client, root App component with routing, and package configuration.

## Prerequisites

- Read solution design and user stories for page and flow coverage.
- If API scaffold artifacts exist, load them for typed API client generation.

## Workflow

1. Create React page components for all major user flows
2. Generate a typed API client in `client/src/services/api.ts`
3. Build root App component with React Router setup
4. Define route configuration in `client/src/routes.tsx`
5. Generate package.json with frontend dependencies
6. Use `// FILE: path/to/file.tsx` comment pattern in all code blocks
7. Save a manifest summarizing all generated files

## Quality Gates

- [ ] Page components for all major user flows
- [ ] Typed API client matching backend endpoints
- [ ] Root App component with router setup
- [ ] Route configuration referencing all pages
- [ ] No hardcoded API URLs (use environment variables)
- [ ] Responsive layout patterns applied
- [ ] Package.json with all required dependencies

## Output Format

Save manifest as `{ProjectName}_Frontend_Scaffold_v{Version}.md` in the outputs directory.
