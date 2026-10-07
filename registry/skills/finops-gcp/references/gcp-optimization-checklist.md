# GCP Cost Optimization Checklist

## 1. Compute — Compute Engine & Containers

- [ ] Identify idle VMs (<10% avg CPU over 14 days) — check Active Assist Recommender
- [ ] Identify underutilized VMs (<30% avg CPU over 14 days)
- [ ] Right-size VMs using Recommender API suggestions with estimated savings
- [ ] Upgrade to latest machine type generation — n1→n2/n2d, c2→c3 for better price-performance
- [ ] Evaluate e2 (cost-optimized) machine types for general workloads — cheapest option
- [ ] Consider custom machine types — pay only for exact vCPU/memory needed (no waste)
- [ ] Evaluate Tau T2D/T2A VMs for scale-out workloads — best price-performance
- [ ] Review Spot/Preemptible VM viability for batch, CI/CD, dev/test, fault-tolerant workloads
- [ ] Audit MIG autoscaler min/max/target — over-provisioned MIGs waste money
- [ ] Check for VMs running outside business hours — use instance schedules or Cloud Scheduler
- [ ] Review GKE node pool sizing — enable cluster autoscaler, use spot node pools
- [ ] Evaluate GKE Autopilot vs Standard — Autopilot auto-right-sizes pods
- [ ] Audit Cloud Run min instances and CPU allocation (always-on vs request-based billing)
- [ ] Review Cloud Functions memory/CPU allocation vs execution time trade-off
- [ ] Evaluate Cloud Functions gen2 vs gen1 (gen2 has better pricing for longer executions)
- [ ] Check for sole-tenant nodes with low utilization

## 2. Storage — Cloud Storage

- [ ] Analyze bucket storage class distribution (Standard / Nearline / Coldline / Archive)
- [ ] Move infrequently accessed objects to Nearline (>30 day access pattern)
- [ ] Move archival data to Coldline (>90 days) or Archive (>365 days)
- [ ] Enable Autoclass for buckets with mixed/unpredictable access patterns
- [ ] Configure Object Lifecycle Management policies per bucket
- [ ] Review object versioning — excessive non-current versions consuming storage
- [ ] Check for soft-delete retention costs
- [ ] Audit multi-region vs dual-region vs single-region per criticality
- [ ] Review requester-pays bucket configuration for shared datasets

## 3. Storage — Persistent Disks & Snapshots

- [ ] Identify unattached Persistent Disks — delete or snapshot and remove
- [ ] Evaluate disk type — pd-balanced vs pd-ssd vs pd-standard per workload
- [ ] Migrate pd-standard to pd-balanced where SSD performance not needed (better price-performance)
- [ ] Right-size disk capacity — check actual usage vs provisioned
- [ ] Review snapshot retention — delete stale snapshots
- [ ] Identify orphaned snapshots (source disk/VM deleted)
- [ ] Use scheduled snapshot policies via Cloud Scheduler or snapshot schedules
- [ ] Check for pd-ssd on dev/test workloads (pd-balanced usually sufficient)

## 4. Database & Analytics

- [ ] Identify idle Cloud SQL instances (<5% CPU over 14 days)
- [ ] Right-size Cloud SQL — match machine type to actual CPU/memory needs
- [ ] Evaluate Cloud SQL high availability necessity per instance — dev/test rarely needs HA
- [ ] Review Cloud SQL storage type — SSD vs HDD economics per workload
- [ ] Check Cloud SQL storage auto-increase — can lead to oversized disks over time
- [ ] Analyze BigQuery pricing model — on-demand vs editions (Standard/Enterprise/Enterprise Plus)
- [ ] Review BigQuery slot utilization if using editions — right-size baseline and autoscale
- [ ] Optimize BigQuery queries — use partitioning, clustering, and avoid SELECT \*
- [ ] Check BigQuery storage — active vs long-term (50% cheaper after 90 days, automatic)
- [ ] Review Bigtable cluster sizing — enable autoscaling, check node utilization
- [ ] Right-size Memorystore instances — check memory utilization and connection counts
- [ ] Analyze Spanner node count — processing units vs actual throughput requirements
- [ ] Review Firestore — document read/write patterns, TTL policies for auto-cleanup
- [ ] Check AlloyDB cluster sizing and read pool optimization

## 5. Networking & Data Transfer

- [ ] Analyze internet egress costs — GCP's largest hidden cost
- [ ] Review network service tier — Premium vs Standard tier per workload
- [ ] Enable Private Google Access for VMs without external IPs to reach Google APIs
- [ ] Audit cross-region data transfer — replicate only what's necessary
- [ ] Review Cloud Interconnect/VPN bandwidth provisioning
- [ ] Optimize Cloud CDN caching hit rates — check backend and CDN cache configuration
- [ ] Check for idle Cloud NAT gateways and external static IPs
- [ ] Identify unused forwarding rules, target pools, and load balancers
- [ ] Review Cloud Armor pricing if configured — standard vs managed rules

## 6. Commitment Discounts

- [ ] Calculate CUD coverage — target 60-80% of steady-state compute
- [ ] **Resource-based CUDs**: Locked to machine family + region — deepest discount (up to 57% for 3yr)
- [ ] **Spend-based CUDs**: Flexible across machine families and regions — up to 46% for 3yr
- [ ] Evaluate resource-based vs spend-based CUD trade-offs per workload pattern
- [ ] Model 1-year vs 3-year commitment trade-offs
- [ ] Review Sustained Use Discounts (SUDs) — automatic, up to 30% for VMs running >25% of month
- [ ] Note: E2 and Tau machine types use SUDs; N2/N2D/C2/C3 eligible for CUDs
- [ ] Check for Flex CUD availability for short-term commitments
- [ ] Review BigQuery editions commitments and slot reservation sizing
- [ ] Audit Cloud SQL committed use discounts

## 7. Backup & Disaster Recovery

- [ ] Audit Cloud SQL automated backup retention and on-demand backup sprawl
- [ ] Review Compute Engine snapshot costs and scheduling policies
- [ ] Check cross-region backup replication costs
- [ ] Clean up old machine images and custom images
- [ ] Evaluate DR architecture costs vs actual RPO/RTO requirements
- [ ] Review Filestore backup costs and retention periods
- [ ] Check for excessive Cloud Storage versioning used as backup strategy

## 8. Waste & Orphaned Resources

- [ ] Delete unattached Persistent Disks
- [ ] Release unused static external IP addresses (charged when unattached)
- [ ] Remove idle load balancers and forwarding rules
- [ ] Clean up unused VPC firewall rules and routes
- [ ] Delete unused Cloud SQL replicas
- [ ] Check for dev/test resources running 24/7 — use instance schedules
- [ ] Review Cloud Logging ingestion — exclude noisy log sources, set appropriate retention
- [ ] Identify unused Cloud NAT configurations
- [ ] Delete stale GKE clusters (especially in dev/test projects)
- [ ] Review Cloud Monitoring — custom metrics and alerting data volume

## 9. Governance & Visibility

- [ ] Implement mandatory labeling policy (Organization Policy constraints)
- [ ] Set up GCP Budgets with alerts at 50%, 80%, 100% thresholds per project
- [ ] Enable billing export to BigQuery for advanced FinOps analytics
- [ ] Deploy Organization Policy constraints for allowed machine types, regions, APIs
- [ ] Review folder/project hierarchy for cost management alignment
- [ ] Use Looker Studio dashboards with billing export data for stakeholder reporting
- [ ] Configure Active Assist Recommender notifications
- [ ] Review IAM roles — restrict expensive service launches (custom roles for budget control)
