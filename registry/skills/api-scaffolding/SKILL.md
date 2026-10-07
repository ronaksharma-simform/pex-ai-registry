---
name: api-scaffolding
description: Generate backend API scaffolding with TypeScript types, database schema, and route handlers
stage: development
triggers:
  - scaffold api
  - scaffold the api
  - scaffold api layer
  - generate backend
  - create api
  - backend scaffolding
  - generate routes
  - server code
  - api code
  - api layer
prerequisites:
  - docx
output_format: code
version: 0
---

# API Scaffolding Skill

## Overview

Generates a complete backend API scaffold including TypeScript interfaces, Prisma database schema, RESTful route handlers, server entry point with middleware, and package configuration.

## Prerequisites

- Read solution design and user stories for accurate endpoint and model coverage.
- If design artifacts exist, load them for data model definitions.

## Workflow

1. Define TypeScript interfaces for all entities in `shared/types/models.ts`
2. Generate Prisma database schema with relations and indexes
3. Create RESTful route handlers per resource with CRUD operations
4. Build server entry point with middleware (CORS, auth, validation, error handling)
5. Generate package.json with required dependencies
6. Configure the production build to EXCLUDE all test code so tests never ship in the
   app. In the build tsconfig (e.g. `tsconfig.build.json`) the `exclude` list MUST cover
   the test dir, the PexAI `generated/` dir, and the test globs
   `**/*spec.ts`, `**/*.spec.tsx`, `**/*.test.ts`, `**/*.test.tsx`. The app entry
   (`node dist/main`) and its build must not depend on any test file or test-only devDep.
7. Use `// FILE: path/to/file.ts` comment pattern in all code blocks
8. Save a manifest summarizing all generated files

## Quality Gates

- [ ] TypeScript interfaces for all entities
- [ ] Prisma schema with proper relations and field types
- [ ] Route handlers for each resource with standard CRUD
- [ ] Server entry point with middleware chain
- [ ] No hardcoded secrets or credentials
- [ ] Minimal use of `any` type
- [ ] All routes reference corresponding controllers
- [ ] Package.json with all required dependencies
- [ ] Production build excludes test code (test dir, `generated/`, `*spec.ts`/`*.test.ts(x)`) — tests never compile into `dist/` or affect the app's run

## Output Format

Save manifest as `{ProjectName}_API_Scaffold_v{Version}.md` in the outputs directory.
