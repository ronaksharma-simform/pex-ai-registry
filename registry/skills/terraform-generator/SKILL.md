---
name: terraform-generator
description: Generate Terraform infrastructure modules for networking, compute, database, storage, and monitoring
stage: devops
triggers:
  - terraform
  - infrastructure as code
  - iac
  - generate infra
  - cloud infrastructure
  - terraform modules
prerequisites: []
output_format: code
version: 0
---

# Terraform Generator Skill

## Overview

Generates a complete Terraform infrastructure with modular HCL files covering networking, compute, database, storage, and monitoring. Supports AWS, Azure, and GCP based on project context.

## Prerequisites

- Read solution design for architecture and infrastructure requirements.
- Resolve cloud provider from project tech stack context.

## Workflow

1. Determine target cloud provider from project context
2. Generate networking module (VPC, subnets, security groups)
3. Generate compute module (ECS/EKS/App Service/Cloud Run)
4. Generate database module (RDS/Cloud SQL/Cosmos DB)
5. Generate storage module (S3/Blob Storage/GCS)
6. Generate monitoring module (CloudWatch/Azure Monitor/Cloud Monitoring)
7. Create root main.tf with provider config and backend
8. Generate environment-specific tfvars (dev, staging, production)
9. Use `# FILE: modules/<module>/main.tf` comment pattern in code blocks

## Quality Gates

- [ ] All 5 modules present (networking, compute, database, storage, monitoring)
- [ ] Each module has main.tf, variables.tf, and outputs.tf
- [ ] Root main.tf with required_providers and backend configuration
- [ ] Environment tfvars for dev, staging, and production
- [ ] No hardcoded AWS account IDs, secrets, or credentials
- [ ] Variables have descriptions and sensible defaults
- [ ] Outputs defined for cross-module references

## Output Format

Save manifest as `{ProjectName}_Terraform_v{Version}.md` in the outputs directory.
