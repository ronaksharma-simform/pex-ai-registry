# Azure Pricing Models & Discount Mechanisms Reference

## Pricing Models Overview

### Pay-As-You-Go (PAYG)

- Per-second billing for most compute resources
- Full list price — used as baseline for savings calculations
- Best for: unpredictable workloads, short-term needs, initial sizing

### Azure Reservations

- 1-year or 3-year commitment for specific SKU in a specific region
- **Discounts**: Up to 72% for VMs, up to 65% for Azure SQL, varies by service
- Applies to: VMs, Azure SQL, Cosmos DB, App Service, Azure Cache for Redis, Synapse, Databricks, Storage
- Instance size flexibility: Reservations apply across sizes within the same series/family
- **Key metric**: Reservation Utilization — target >80%, Coverage — target 60-80% of steady-state
- Exchangeable within same reservation type; refundable up to $50K/year

### Azure Savings Plans for Compute

- 1-year or 3-year commitment for $/hour spend on compute
- **Discounts**: Up to 65% on VMs, extends to App Service, Functions, Container Instances
- More flexible than reservations — applies across VM families, regions, and compute services
- Stacks with Azure Hybrid Benefit

### Azure Hybrid Benefit (AHUB)

- Bring existing Windows Server and SQL Server licenses to Azure
- **Windows Server**: Save up to 40% on VM costs (eliminates Windows license surcharge)
- **SQL Server**: Save up to 55% on Azure SQL, SQL Managed Instance, SQL on VMs
- Can combine with reservations for maximum discount (up to 80% total)
- Requires Software Assurance or qualifying subscription licenses

### Dev/Test Pricing

- No Windows license charges on VMs
- Reduced rates on several services (Azure SQL, App Service, Logic Apps, etc.)
- Requires Visual Studio subscription or Enterprise Dev/Test offer
- Apply to ALL non-production subscriptions

### Spot VMs

- Up to 90% discount on spare Azure capacity
- Can be evicted with 30-second notice
- Best for: batch processing, CI/CD, dev/test, fault-tolerant workloads
- Set maximum price to control costs
- Use across multiple VM sizes and regions for availability

## Key Service Pricing Notes

### Virtual Machines

- Dv5/Ev5: Latest general-purpose, better price-performance than Dv3/Ev4
- Dpsv5/Epsv5 (ARM/Ampere): ~20% cheaper than x86 equivalents for Linux
- B-series: Burstable VMs — excellent for low-utilization workloads (cheapest option)

### Storage Account Tiers

| Access Tier | $/GB/month (LRS) | Min Retention | Use Case            |
| ----------- | ---------------- | ------------- | ------------------- |
| Hot         | $0.018           | None          | Frequently accessed |
| Cool        | $0.01            | 30 days       | Infrequent access   |
| Cold        | $0.0036          | 90 days       | Rare access         |
| Archive     | $0.00099         | 180 days      | Long-term archive   |

_Prices approximate, East US. Read/write operation costs increase for cooler tiers._

### Managed Disk Pricing

| Type                    | $/GB/month                           | IOPS         | Best For             |
| ----------------------- | ------------------------------------ | ------------ | -------------------- |
| Standard HDD (S-series) | $0.04                                | 500          | Dev/test, backups    |
| Standard SSD (E-series) | $0.075                               | 500          | Light production     |
| Premium SSD (P-series)  | $0.132                               | 120/GB       | Production workloads |
| Premium SSD v2          | Pay for capacity + IOPS + throughput | Configurable | High performance     |
| Ultra Disk              | Pay for capacity + IOPS + throughput | Configurable | Extreme performance  |

### Data Transfer

- Intra-VNet (same region): Free
- Cross-VNet peering (same region): $0.01/GB each direction
- Cross-region: $0.02-0.08/GB depending on region pair
- Internet egress: Tiered — $0.087/GB first 10TB, decreasing with volume (first 100GB/month free)
- Private Endpoint: $0.01/hour + $0.01/GB processed
- ExpressRoute: Metered or unlimited plans

### Azure SQL

- DTU model: Bundled compute/storage/IO — simpler, less flexible
- vCore model: Independent compute and storage — better for right-sizing
- Serverless: Auto-pause after idle period (min 1 hour), auto-scale vCores
- Elastic Pools: Share DTUs/vCores across multiple databases

### Cosmos DB

| Pricing Model | Cost                                     | Best For                 |
| ------------- | ---------------------------------------- | ------------------------ |
| Serverless    | Per RU consumed + storage                | <5000 RU/s, intermittent |
| Provisioned   | Per 100 RU/s/hour + storage              | Steady, predictable      |
| Autoscale     | Per 100 RU/s/hour (10% of max) + storage | Variable with peaks      |
| Reserved      | 1yr/3yr commitment on provisioned        | Steady, committed        |

## Discount Stacking Rules

1. Azure Hybrid Benefit + Reservation = maximum discount (up to 80%)
2. Azure Hybrid Benefit + Savings Plan = also stacks
3. Reservations and Savings Plans do NOT stack — reservation applies first, then SP covers remaining
4. Dev/Test pricing is a separate subscription offer, stacks with AHUB
5. Spot pricing is independent — does not stack with reservations/SPs
6. EA/MCA commitment discounts apply on top of other discounts

## Savings Calculation Formula

```
Monthly Savings = (PAYG Price - Optimized Price) × Usage Hours × Instance Count
Annual Savings = Monthly Savings × 12
ROI Period = Implementation Cost / Monthly Savings
```

## Common Savings Benchmarks

- Right-sizing (1 size down): 30-50% per VM
- ARM/Ampere migration: ~20% cost reduction
- B-series for low-utilization: 50-70% vs D-series
- Blob Hot → Cool: 44% storage cost reduction
- Blob Hot → Archive: 95% storage cost reduction
- Azure Hybrid Benefit (Windows): Up to 40% on VM
- Azure Hybrid Benefit (SQL): Up to 55% on Azure SQL
- Dev/Test pricing: ~40% on Windows VMs
- 1yr Reservation (VM): ~30-40% discount
- 3yr Reservation (VM): ~55-72% discount
- Spot VMs: 60-90% vs PAYG
