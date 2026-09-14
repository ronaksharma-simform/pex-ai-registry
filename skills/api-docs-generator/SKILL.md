---
name: api-docs-generator
description: Generate a comprehensive API reference documentation with endpoint specs, auth, and examples
stage: documentation
triggers:
  - api docs
  - api reference
  - api documentation
  - endpoint docs
  - rest docs
  - generate api reference
prerequisites:
  - docx
output_format: docx
version: 3
---

# API Docs Generator Skill

## Overview

Generates a comprehensive API reference document covering all endpoints, authentication, error handling, pagination, and request/response examples with curl snippets.

## Prerequisites

- Read project context for endpoint definitions and data models.
- If scaffold or design artifacts exist, load them first for accurate endpoint coverage.
- Apply document formatting guidelines from docx skill.

## Workflow

1. Identify all API endpoints from project context and code artifacts
2. Document authentication and authorization mechanisms
3. Define error response formats and status codes
4. Document pagination patterns and query parameters
5. Generate curl examples for each endpoint
6. Include JSON request/response body examples
7. Format as structured markdown with proper headings
8. Save as both markdown and docx artifacts

## Quality Gates

- [ ] Overview section with base URL and versioning
- [ ] Authentication section with token/key examples
- [ ] Error handling section with standard error response format
- [ ] Pagination section with query parameter documentation
- [ ] All endpoints documented with HTTP method, path, and description
- [ ] Curl examples provided for each endpoint
- [ ] JSON request/response examples in code blocks
- [ ] No hardcoded secrets or tokens in examples

## Output Format

Save as `{ProjectName}_API_Reference_v{Version}.docx` in the outputs directory.
