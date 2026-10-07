---
name: finops-aws
description: Solution Architect-level AWS FinOps analysis — billing review, resource right-sizing, storage optimization, Reserved/Savings Plans evaluation, backup cost review, and actionable cost optimization recommendations
stage: discovery
triggers:
  - aws finops
  - aws cost optimization
  - aws billing analysis
  - aws cost review
  - optimize aws costs
  - aws spend analysis
  - aws right-sizing
  - aws savings plan
  - aws reserved instances
  - reduce aws bill
  - aws cost audit
  - aws cloud cost
prerequisites: []
output_format: docx
version: 0
---

# AWS FinOps Skill

## Overview

Performs a Solution Architect-level FinOps analysis of an AWS account or organization. Covers billing decomposition, compute right-sizing, storage tiering, data transfer costs, Reserved Instance and Savings Plans evaluation, backup cost optimization, unused resource identification, and generates a prioritized savings roadmap with estimated monthly/annual savings per recommendation.

## Prerequisites

- Access to AWS billing data (Cost Explorer exports, CUR files, or screenshots/exports from the AWS console).
- Resource inventory or AWS Config/Trusted Advisor exports if available.
- Current Reserved Instance and Savings Plans commitments.

## Workflow

### Phase 1: Data Collection & Intake

1. Gather billing data — CUR (Cost and Usage Report), Cost Explorer exports, or manual billing summaries
2. Collect resource inventory — EC2, RDS, EBS, S3, Lambda, ECS/EKS, ElastiCache, Redshift, etc.
3. Identify account structure — single account vs AWS Organizations, linked accounts, cost allocation tags
4. Note current commitment coverage — Reserved Instances, Savings Plans, spot usage

### Phase 2: Billing Decomposition

5. Break down spend by service (top 10 services by cost)
6. Break down spend by account/team (if Organizations)
7. Identify month-over-month cost trends and anomalies
8. Analyze cost allocation tag coverage and gaps
9. Identify untagged resources and their estimated cost

### Phase 3: Compute Optimization

10. Analyze EC2 instance utilization — identify idle (<10% CPU avg) and underutilized (<30% CPU avg) instances
11. Recommend right-sizing (downgrade instance family/size) with estimated savings
12. Evaluate EC2 generation upgrades (e.g., m5 → m7g/m7i for Graviton savings)
13. Assess Spot Instance opportunities for fault-tolerant workloads
14. Review Auto Scaling configurations — are min/max/desired properly tuned?
15. Analyze Lambda provisioned concurrency vs actual invocation patterns
16. Review ECS/EKS cluster right-sizing and Fargate vs EC2 launch type economics

### Phase 4: Storage & Data Optimization

17. Analyze S3 storage class distribution — identify Standard objects that should be IA, Glacier, or Deep Archive
18. Review S3 Lifecycle policies — are they configured? Are they optimal?
19. Check S3 Intelligent-Tiering adoption opportunity
20. Analyze EBS volume utilization — unattached volumes, oversized volumes, gp2 → gp3 migration savings
21. Review EBS snapshot retention — orphaned snapshots, excessive retention periods
22. Analyze data transfer costs — inter-AZ, inter-region, internet egress
23. Identify VPC endpoint opportunities to reduce NAT Gateway data processing costs
24. Review CloudFront distribution efficiency and caching hit rates

### Phase 5: Database Optimization

25. Analyze RDS instance utilization — idle or underutilized instances
26. Evaluate RDS right-sizing and Aurora Serverless v2 opportunities
27. Review RDS storage — provisioned IOPS vs gp3, over-provisioned storage
28. Check DynamoDB capacity mode — provisioned vs on-demand, auto-scaling configuration
29. Review ElastiCache node utilization and right-sizing
30. Analyze Redshift cluster utilization — RA3 migration, concurrency scaling costs

### Phase 6: Commitment & Purchasing Optimization

31. Analyze Reserved Instance coverage and utilization rates
32. Identify RI expiration schedule and renewal recommendations
33. Evaluate Savings Plans coverage — Compute vs EC2 Instance vs SageMaker
34. Model optimal Savings Plans commitment level (60-80% baseline coverage)
35. Identify convertible RI exchange opportunities
36. Review Spot usage and Spot Fleet diversification

### Phase 7: Backup & DR Cost Review

37. Analyze AWS Backup vault costs and retention policies
38. Review RDS automated backup retention vs manual snapshot proliferation
39. Check cross-region backup replication costs
40. Evaluate AMI sprawl — old, unused, or duplicate AMIs
41. Review disaster recovery architecture costs vs actual RPO/RTO requirements

### Phase 8: Waste Elimination

42. Identify idle resources — stopped EC2 with attached EBS, unused EIPs, idle load balancers
43. Find orphaned resources — unattached EBS volumes, unused ENIs, stale security groups
44. Check for development/test resources running 24/7 that should be scheduled
45. Review CloudWatch log retention — excessive retention generating storage costs
46. Identify unused or underutilized Elastic IPs, NAT Gateways, VPN connections

### Phase 9: Governance & Tagging

47. Assess cost allocation tag strategy and coverage percentage
48. Recommend tagging policy for cost attribution
49. Review AWS Budgets and Cost Anomaly Detection configuration
50. Recommend organizational guardrails (SCPs, budget alerts)

### Phase 10: Report Generation

51. Calculate total identified savings (monthly and annualized)
52. Prioritize recommendations by effort vs impact (quick wins, medium-term, strategic)
53. Generate executive summary with top 5 savings opportunities
54. Create detailed findings with per-item estimated savings
55. Build implementation roadmap with phased approach
56. Apply formatting guidelines and save report

## Reference Files

- `references/aws-optimization-checklist.md` — Comprehensive AWS cost optimization checklist
- `references/aws-pricing-reference.md` — Key AWS pricing models and discount mechanisms
- `references/aws-report-template.md` — Report structure and section templates

## Quality Gates

- [ ] Billing decomposition covers top 10 services by spend
- [ ] Compute analysis includes right-sizing recommendations with estimated savings
- [ ] Storage analysis covers S3, EBS, and snapshot optimization
- [ ] RI/Savings Plans coverage analyzed with renewal/purchase recommendations
- [ ] Data transfer costs analyzed with VPC endpoint and architecture recommendations
- [ ] Backup and DR costs reviewed with retention optimization
- [ ] Waste elimination identifies idle and orphaned resources
- [ ] Each recommendation includes estimated monthly savings (USD)
- [ ] Recommendations prioritized into quick wins / medium-term / strategic
- [ ] Executive summary highlights top 5 savings opportunities with total savings estimate
- [ ] Implementation roadmap with phased approach provided

## Output Format

Save as `{ClientName}_AWS_FinOps_Report_v{Version}.docx` in the outputs directory.
