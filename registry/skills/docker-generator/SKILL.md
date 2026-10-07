---
name: docker-generator
description: Generate Dockerfile and docker-compose configurations for containerized development and deployment
stage: devops
triggers:
  - docker
  - dockerfile
  - container
  - docker compose
  - containerize
  - docker config
prerequisites: []
output_format: code
version: 0
---

# Docker Generator Skill

## Overview

Generates Docker configuration files including multi-stage Dockerfiles for backend and frontend services, docker-compose for local development, and .dockerignore files.

## Prerequisites

- Read project tech stack for base image selection and build steps.

## Workflow

1. Generate backend Dockerfile with multi-stage build (build + runtime)
2. Generate frontend Dockerfile with multi-stage build (build + nginx serve)
3. Create docker-compose.yml for local development with all services
4. Generate .dockerignore files to exclude unnecessary files
5. Use `# FILE: <path>` comment pattern in code blocks

## Quality Gates

- [ ] Backend Dockerfile with multi-stage build
- [ ] Frontend Dockerfile with multi-stage build
- [ ] docker-compose.yml with all services (app, db, cache)
- [ ] .dockerignore files present
- [ ] No secrets or credentials in Dockerfiles
- [ ] Health checks defined for services
- [ ] Proper use of build cache layers

## Output Format

Save manifest as `{ProjectName}_Docker_v{Version}.md` in the outputs directory.
