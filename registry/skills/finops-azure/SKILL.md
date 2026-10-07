---
name: finops-azure
description: Solution Architect-level Azure FinOps analysis — billing review, resource right-sizing, storage optimization, Reserved Instances/Savings Plans evaluation, backup cost review, and actionable cost optimization recommendations
stage: discovery
triggers:
  - azure finops
  - azure cost optimization
  - azure billing analysis
  - azure cost review
  - optimize azure costs
  - azure spend analysis
  - azure right-sizing
  - azure reservations
  - reduce azure bill
  - azure cost audit
  - azure cloud cost
prerequisites: []
output_format: docx
version: 0
---

# Azure FinOps Skill

## Overview

Performs a Solution Architect-level FinOps analysis of an Azure subscription or enterprise enrollment. Covers billing decomposition, compute right-sizing, storage tiering, data transfer costs, Azure Reservations and Savings Plans evaluation, backup cost optimization, Azure Advisor integration, unused resource identification, and generates a prioritized savings roadmap with estimated monthly/annual savings per recommendation.

## Prerequisites

- Access to Azure billing data (Cost Management exports, invoice summaries, or portal screenshots/exports).
- Resource inventory or Azure Advisor/Azure Resource Graph exports if available.
- Current Azure Reservation and Savings Plans commitments.
- EA/MCA/CSP agreement type for pricing context.

## Workflow

### Phase 1: Data Collection & Intake

1. Gather billing data — Cost Management exports, Azure invoices, or manual billing summaries
2. Collect resource inventory — VMs, SQL DBs, Storage Accounts, App Services, AKS, Cosmos DB, etc.
3. Identify account structure — Management Groups, Subscriptions, Resource Groups, EA enrollment
4. Note current commitment coverage — Azure Reservations, Savings Plans, Hybrid Benefit, Dev/Test pricing
5. Collect Azure Advisor cost recommendations if available

### Phase 2: Billing Decomposition

6. Break down spend by service meter category (top 10 by cost)
7. Break down spend by subscription/resource group/team
8. Identify month-over-month cost trends and anomalies
9. Analyze resource tagging coverage and gaps
10. Identify untagged resources and their estimated cost
11. Review Azure Marketplace third-party spend

### Phase 3: Compute Optimization

12. Analyze VM utilization — identify idle (<10% CPU avg) and underutilized (<30% CPU avg) VMs
13. Recommend right-sizing (downgrade VM SKU/series) with estimated savings
14. Evaluate VM generation upgrades (e.g., Dv3 → Dv5, Ev4 → Ev5) and ARM-based options (Dpsv5/Epsv5)
15. Assess Spot VM opportunities for fault-tolerant and batch workloads
16. Review VM Scale Set configurations — are scaling rules and min/max properly tuned?
17. Analyze App Service Plan utilization — consolidate or right-size plans
18. Review Azure Functions consumption vs premium plan economics
19. Analyze AKS cluster right-sizing — node pool sizing, cluster autoscaler, virtual nodes

### Phase 4: Storage & Data Optimization

20. Analyze Storage Account tier distribution — Hot vs Cool vs Cold vs Archive
21. Review Blob Lifecycle Management policies — are they configured and optimal?
22. Check Storage Account access tier defaults (Hot should not be default for archival data)
23. Analyze Managed Disk utilization — unattached disks, oversized disks, Standard HDD → SSD migration economics
24. Review disk snapshot retention — orphaned snapshots, excessive retention
25. Analyze data transfer costs — cross-region, internet egress, VNet peering costs
26. Identify Private Endpoint opportunities to reduce data transfer costs
27. Review Azure CDN/Front Door caching efficiency

### Phase 5: Database Optimization

28. Analyze Azure SQL Database utilization — DTU/vCore utilization, idle databases
29. Evaluate Azure SQL elastic pools for consolidation savings
30. Review serverless SQL tier opportunities (auto-pause, auto-scale)
31. Check Cosmos DB RU/s provisioning — provisioned vs serverless vs autoscale
32. Analyze Azure Database for MySQL/PostgreSQL flexible server sizing
33. Review Azure Synapse Analytics (dedicated SQL pool) pause schedules and DWU sizing
34. Check Azure Cache for Redis tier and sizing optimization

### Phase 6: Commitment & Purchasing Optimization

35. Analyze Azure Reservation coverage and utilization rates
36. Identify reservation expiration schedule and renewal recommendations
37. Evaluate Azure Savings Plans coverage (Compute)
38. Model optimal reservation/savings plan commitment (60-80% baseline coverage)
39. Review Azure Hybrid Benefit (AHUB) enrollment — Windows Server and SQL Server licenses
40. Verify Dev/Test subscription pricing is applied for non-production workloads
41. Review EA/MCA commitment levels and overage rates

### Phase 7: Backup & DR Cost Review

42. Analyze Azure Backup vault costs and retention policies
43. Review Recovery Services vault — redundancy type (LRS vs GRS), soft delete costs
44. Check Azure Site Recovery licensing and replication costs
45. Evaluate cross-region backup replication costs
46. Review VM image/snapshot sprawl — old, unused, or duplicate images
47. Assess DR architecture costs vs actual RPO/RTO requirements

### Phase 8: Waste Elimination

48. Identify idle resources — deallocated VMs with Premium disks, unused Public IPs, idle Application Gateways
49. Find orphaned resources — unattached disks, unused NICs, empty resource groups, orphaned NSGs
50. Check for dev/test resources running 24/7 that should be scheduled (Azure Automation, Start/Stop VMs)
51. Review Log Analytics workspace retention — excessive retention generating ingestion/storage costs
52. Identify unused or underutilized Application Gateways, VPN Gateways, ExpressRoute circuits
53. Review Azure Monitor and diagnostic settings data volume

### Phase 9: Governance & Tagging

54. Assess resource tagging strategy and coverage percentage
55. Recommend tagging policy for cost attribution (Azure Policy enforce/audit)
56. Review Azure Budgets and Cost Alerts configuration
57. Recommend Azure Policy guardrails for allowed VM SKUs, regions, resource types
58. Review Management Group hierarchy for cost management alignment

### Phase 10: Report Generation

59. Calculate total identified savings (monthly and annualized)
60. Prioritize recommendations by effort vs impact (quick wins, medium-term, strategic)
61. Generate executive summary with top 5 savings opportunities
62. Create detailed findings with per-item estimated savings
63. Build implementation roadmap with phased approach
64. Apply formatting guidelines and save report

## Reference Files

- `references/azure-optimization-checklist.md` — Comprehensive Azure cost optimization checklist
- `references/azure-pricing-reference.md` — Key Azure pricing models, Hybrid Benefit, and discount mechanisms
- `references/azure-report-template.md` — Report structure and section templates

## Quality Gates

- [ ] Billing decomposition covers top 10 service meter categories by spend
- [ ] Compute analysis includes right-sizing recommendations with estimated savings
- [ ] Storage analysis covers Blob tiers, Managed Disks, and snapshot optimization
- [ ] Reservation/Savings Plans coverage analyzed with renewal/purchase recommendations
- [ ] Azure Hybrid Benefit and Dev/Test pricing opportunities identified
- [ ] Data transfer costs analyzed with Private Endpoint and architecture recommendations
- [ ] Backup and DR costs reviewed with retention and redundancy optimization
- [ ] Waste elimination identifies idle and orphaned resources
- [ ] Each recommendation includes estimated monthly savings (USD)
- [ ] Recommendations prioritized into quick wins / medium-term / strategic
- [ ] Executive summary highlights top 5 savings opportunities with total savings estimate
- [ ] Implementation roadmap with phased approach provided

## Output Format

Save as `{ClientName}_Azure_FinOps_Report_v{Version}.docx` in the outputs directory.
