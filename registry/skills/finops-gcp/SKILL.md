---
name: finops-gcp
description: Solution Architect-level Google Cloud FinOps analysis — billing review, resource right-sizing, storage optimization, CUD/SUD evaluation, backup cost review, and actionable cost optimization recommendations
stage: discovery
triggers:
  - gcp finops
  - google cloud finops
  - gcp cost optimization
  - gcp billing analysis
  - gcp cost review
  - optimize gcp costs
  - google cloud cost
  - gcp right-sizing
  - gcp committed use
  - reduce gcp bill
  - gcp cost audit
  - google cloud billing
prerequisites: []
output_format: docx
version: 0
---

# GCP FinOps Skill

## Overview

Performs a Solution Architect-level FinOps analysis of a Google Cloud project or organization. Covers billing decomposition, compute right-sizing, storage tiering, data transfer costs, Committed Use Discounts (CUDs) and Sustained Use Discounts (SUDs) evaluation, backup cost optimization, unused resource identification, and generates a prioritized savings roadmap with estimated monthly/annual savings per recommendation.

## Prerequisites

- Access to GCP billing data (BigQuery billing export, Cloud Billing reports, or console screenshots/exports).
- Resource inventory or Recommender API/Asset Inventory exports if available.
- Current CUD commitments and SUD coverage data.
- Billing account and organization structure details.

## Workflow

### Phase 1: Data Collection & Intake

1. Gather billing data — BigQuery billing export, Cloud Billing reports, or manual billing summaries
2. Collect resource inventory — Compute Engine, GKE, Cloud SQL, Cloud Storage, BigQuery, Cloud Run, etc.
3. Identify account structure — Organization, Folders, Projects, Billing accounts
4. Note current commitment coverage — CUDs (resource-based and spend-based), SUD coverage
5. Collect Active Assist / Recommender recommendations if available

### Phase 2: Billing Decomposition

6. Break down spend by service (top 10 services by cost)
7. Break down spend by project/team/label
8. Identify month-over-month cost trends and anomalies
9. Analyze label coverage and gaps (GCP equivalent of tags)
10. Identify unlabeled resources and their estimated cost
11. Review Marketplace third-party solution spend

### Phase 3: Compute Optimization

12. Analyze Compute Engine VM utilization — identify idle (<10% CPU avg) and underutilized (<30% CPU avg) VMs
13. Recommend right-sizing using Recommender API findings or manual analysis with estimated savings
14. Evaluate machine type generation upgrades (e.g., n1 → n2/n2d, c2 → c3, e2 for cost-efficient workloads)
15. Assess Preemptible/Spot VM opportunities for fault-tolerant workloads
16. Review Managed Instance Group (MIG) autoscaling configurations — are min/max/target properly tuned?
17. Evaluate custom machine types vs predefined for better cost-performance fit
18. Analyze Cloud Run min instances, concurrency, and CPU allocation (always-on vs request-based)
19. Analyze Cloud Functions gen2 vs gen1 and memory/CPU allocation efficiency
20. Review GKE cluster right-sizing — node pool sizing, cluster autoscaler, Autopilot vs Standard economics

### Phase 4: Storage & Data Optimization

21. Analyze Cloud Storage class distribution — Standard vs Nearline vs Coldline vs Archive
22. Review Object Lifecycle Management policies — are they configured and optimal?
23. Check Autoclass adoption opportunity for mixed-access-pattern buckets
24. Analyze Persistent Disk utilization — unattached disks, oversized disks, pd-standard → pd-balanced migration
25. Review disk snapshot retention — orphaned snapshots, excessive retention, snapshot scheduling
26. Analyze data transfer costs — inter-region, internet egress, cross-project
27. Identify Private Google Access and Cloud Interconnect optimization opportunities
28. Review Cloud CDN caching efficiency and cache hit rates

### Phase 5: Database & Analytics Optimization

29. Analyze Cloud SQL instance utilization — idle or underutilized instances
30. Evaluate Cloud SQL right-sizing and High Availability necessity per instance
31. Review Cloud SQL storage — provisioned vs actual usage, SSD vs HDD economics
32. Check BigQuery pricing model — on-demand vs flat-rate/editions, slot utilization
33. Analyze BigQuery storage — active vs long-term storage, partitioning and clustering for query cost reduction
34. Review Bigtable cluster sizing and autoscaling configuration
35. Check Memorystore (Redis/Memcached) tier and sizing optimization
36. Analyze Spanner node count vs actual read/write throughput requirements
37. Review Firestore pricing — document reads/writes optimization, TTL policies

### Phase 6: Commitment & Purchasing Optimization

38. Analyze CUD (Committed Use Discount) coverage — resource-based and spend-based
39. Identify CUD expiration schedule and renewal recommendations
40. Model optimal CUD commitment level (60-80% baseline coverage)
41. Evaluate spend-based CUDs vs resource-based CUDs trade-offs
42. Review Sustained Use Discount (SUD) effectiveness — are workloads running long enough to benefit?
43. Assess Flex CUD opportunities for variable workloads
44. Review BigQuery editions commitment and slot autoscaling

### Phase 7: Backup & DR Cost Review

45. Analyze Cloud SQL automated backup retention and on-demand backup sprawl
46. Review Compute Engine snapshot costs and scheduling policies
47. Check cross-region backup replication costs
48. Evaluate machine image sprawl — old, unused, or duplicate images
49. Review disaster recovery architecture costs vs actual RPO/RTO requirements
50. Analyze Filestore backup costs and retention

### Phase 8: Waste Elimination

51. Identify idle resources — stopped VMs with attached persistent disks, unused static IPs, idle load balancers
52. Find orphaned resources — unattached persistent disks, unused forwarding rules, stale firewall rules
53. Check for dev/test resources running 24/7 that should be scheduled (Cloud Scheduler, instance schedules)
54. Review Cloud Logging ingestion and retention — excessive log sinks, log exclusion filter opportunities
55. Identify unused or underutilized Cloud NAT, VPN tunnels, Interconnect attachments
56. Review Cloud Monitoring and alerting data ingestion costs

### Phase 9: Governance & Labeling

57. Assess resource labeling strategy and coverage percentage
58. Recommend labeling policy for cost attribution (Organization Policies to enforce)
59. Review GCP Budgets and budget alerts configuration
60. Recommend Organization Policy constraints for allowed machine types, regions, APIs
61. Review folder/project hierarchy for cost management alignment
62. Check billing export to BigQuery for advanced FinOps analytics enablement

### Phase 10: Report Generation

63. Calculate total identified savings (monthly and annualized)
64. Prioritize recommendations by effort vs impact (quick wins, medium-term, strategic)
65. Generate executive summary with top 5 savings opportunities
66. Create detailed findings with per-item estimated savings
67. Build implementation roadmap with phased approach
68. Apply formatting guidelines and save report

## Reference Files

- `references/gcp-optimization-checklist.md` — Comprehensive GCP cost optimization checklist
- `references/gcp-pricing-reference.md` — Key GCP pricing models, CUDs, SUDs, and discount mechanisms
- `references/gcp-report-template.md` — Report structure and section templates

## Quality Gates

- [ ] Billing decomposition covers top 10 services by spend
- [ ] Compute analysis includes right-sizing recommendations with estimated savings
- [ ] Storage analysis covers Cloud Storage tiers, Persistent Disks, and snapshot optimization
- [ ] CUD/SUD coverage analyzed with commitment purchase/renewal recommendations
- [ ] BigQuery pricing model and slot utilization reviewed
- [ ] Data transfer costs analyzed with networking architecture recommendations
- [ ] Backup and DR costs reviewed with retention optimization
- [ ] Waste elimination identifies idle and orphaned resources
- [ ] Each recommendation includes estimated monthly savings (USD)
- [ ] Recommendations prioritized into quick wins / medium-term / strategic
- [ ] Executive summary highlights top 5 savings opportunities with total savings estimate
- [ ] Implementation roadmap with phased approach provided

## Output Format

Save as `{ClientName}_GCP_FinOps_Report_v{Version}.docx` in the outputs directory.
