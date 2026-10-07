# Azure Cost Optimization Checklist

## 1. Compute — Virtual Machines & Containers

- [ ] Identify idle VMs (<10% avg CPU over 14 days) — check Azure Advisor
- [ ] Identify underutilized VMs (<30% avg CPU over 14 days)
- [ ] Right-size VMs — match VM SKU/series to workload profile
- [ ] Upgrade to latest generation — Dv3→Dv5, Ev4→Ev5 for better price-performance
- [ ] Evaluate ARM-based Dpsv5/Epsv5 (Ampere) VMs for Linux workloads — ~20% cheaper
- [ ] Review Spot VM viability for batch, CI/CD, dev/test, stateless workers
- [ ] Audit VM Scale Set min/max/scaling rules — over-provisioned sets waste money
- [ ] Check for VMs running outside business hours — implement Start/Stop VMs v2 (Azure Automation)
- [ ] Review App Service Plan SKU and utilization — consolidate underused plans
- [ ] Audit App Service instances — can multiple apps share a plan?
- [ ] Evaluate Azure Functions Consumption vs Premium plan based on execution patterns
- [ ] Review AKS node pool sizing — use cluster autoscaler, spot node pools, virtual nodes
- [ ] Check for Azure Container Instances running as long-lived services (should be AKS/App Service)

## 2. Storage — Blob Storage

- [ ] Analyze Storage Account access tier distribution (Hot / Cool / Cold / Archive)
- [ ] Move infrequently accessed blobs to Cool tier (>30 days between access)
- [ ] Move archival data to Cold (>90 days) or Archive tier
- [ ] Configure Blob Lifecycle Management policies per container/prefix
- [ ] Check for Storage Accounts defaulting to Hot when Cool/Cold would suffice
- [ ] Review blob versioning — excessive versions consuming storage
- [ ] Audit soft-delete retention periods — excessive retention adds cost
- [ ] Check for unused Storage Accounts with minimal data
- [ ] Review Storage Account redundancy — LRS vs ZRS vs GRS vs RA-GRS per criticality

## 3. Storage — Managed Disks & Snapshots

- [ ] Identify unattached Managed Disks — delete or snapshot and remove
- [ ] Evaluate disk type — Premium SSD vs Standard SSD vs Standard HDD per workload
- [ ] Right-size disk capacity — check actual usage vs provisioned
- [ ] Review disk snapshot retention — delete stale snapshots
- [ ] Identify orphaned snapshots (source disk/VM deleted)
- [ ] Check for Premium SSD on dev/test workloads (Standard SSD usually sufficient)
- [ ] Review Ultra Disk and Premium SSD v2 IOPS/throughput provisioning

## 4. Database

- [ ] Identify idle Azure SQL databases (<5% DTU/vCore usage over 14 days)
- [ ] Right-size Azure SQL — match DTU/vCore tier to actual consumption
- [ ] Evaluate Azure SQL Elastic Pools for multiple underutilized databases
- [ ] Review Azure SQL Serverless tier for intermittent workloads (auto-pause)
- [ ] Check Cosmos DB RU/s — switch autoscale for variable, provisioned for steady, serverless for light
- [ ] Audit Cosmos DB reserved capacity purchases
- [ ] Right-size Azure Database for MySQL/PostgreSQL Flexible Server
- [ ] Review Azure Synapse dedicated SQL pool — pause during off-hours, right-size DWUs
- [ ] Check Azure Cache for Redis tier — Basic for dev, Standard for prod, Premium only if needed

## 5. Networking & Data Transfer

- [ ] Analyze internet egress costs — largest data transfer expense
- [ ] Deploy Private Endpoints to keep traffic on Azure backbone
- [ ] Review cross-region data transfer — replicate only what's necessary
- [ ] Audit VNet Peering costs — consolidate where possible
- [ ] Review Application Gateway and WAF SKU — v2 vs v1, right-size capacity units
- [ ] Check for idle load balancers and Application Gateways
- [ ] Identify unused Public IP addresses (now charged even if unattached)
- [ ] Review VPN Gateway and ExpressRoute circuit sizing
- [ ] Optimize Azure Front Door / CDN caching hit rates

## 6. Commitment Discounts

- [ ] Calculate Azure Reservation coverage — target 60-80% of steady-state
- [ ] Identify expiring reservations — plan renewal or switch to Savings Plans
- [ ] Evaluate Azure Savings Plans for Compute — flexible across VMs, App Service, Functions
- [ ] Compare Reservation (deeper discount, locked SKU) vs Savings Plan (flexible, slightly less discount)
- [ ] Model 1-year vs 3-year commitment trade-offs
- [ ] **Azure Hybrid Benefit (AHUB)**: Apply Windows Server licenses to VMs (save up to 40%)
- [ ] **AHUB for SQL Server**: Apply SQL Server licenses to Azure SQL/VMs (save up to 55%)
- [ ] **Dev/Test pricing**: Ensure non-prod subscriptions use Dev/Test offer (no Windows license cost)
- [ ] Review EA/MCA monetary commitment levels and overage rates
- [ ] Check for unused reservations — exchange or refund eligible ones

## 7. Backup & Disaster Recovery

- [ ] Audit Azure Backup vault policies — excessive retention drives cost
- [ ] Review Recovery Services vault redundancy — LRS is cheaper than GRS for non-critical
- [ ] Check soft-delete retention for backup vaults (14 days mandatory, more is optional)
- [ ] Review Azure Site Recovery per-VM replication costs — disable for non-critical VMs
- [ ] Audit cross-region replication necessity per workload
- [ ] Clean up old VM images and snapshots
- [ ] Evaluate DR tier vs actual RPO/RTO requirements

## 8. Waste & Orphaned Resources

- [ ] Delete unattached Managed Disks
- [ ] Release unused Public IP addresses
- [ ] Remove idle Application Gateways and Load Balancers
- [ ] Clean up unused NICs (Network Interfaces)
- [ ] Delete empty Resource Groups
- [ ] Remove orphaned NSGs not attached to any subnet/NIC
- [ ] Check for test/dev resources left running (tag-based identification)
- [ ] Review Log Analytics workspace — reduce retention, filter noisy log sources
- [ ] Delete unused Azure DNS zones
- [ ] Review Azure Monitor diagnostic settings data volume and necessity

## 9. Governance & Visibility

- [ ] Implement mandatory tagging policy (Azure Policy — audit or deny)
- [ ] Set up Azure Budgets with alerts at 50%, 80%, 100% thresholds per subscription
- [ ] Enable Azure Cost Management anomaly detection
- [ ] Deploy Azure Policy to restrict allowed VM SKUs, regions, and resource types
- [ ] Review Management Group hierarchy for cost management alignment
- [ ] Use Azure Cost Management Power BI integration for stakeholder reporting
- [ ] Configure Azure Advisor to email weekly cost recommendations
