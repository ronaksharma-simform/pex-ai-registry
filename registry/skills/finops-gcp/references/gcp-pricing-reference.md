# GCP Pricing Models & Discount Mechanisms Reference

## Pricing Models Overview

### On-Demand (Pay-As-You-Go)

- Per-second billing (1-minute minimum) for most compute resources
- Full list price — used as baseline for savings calculations
- Best for: unpredictable workloads, short-term needs, initial sizing

### Sustained Use Discounts (SUDs)

- **Automatic** discount for running VMs more than 25% of the month
- No commitment required — applied automatically at billing time
- Discount scales: 25% usage = small discount, 100% usage = up to 30% discount
- Applies to: N1, N2, N2D, C2, M1, M2 machine types and GPUs
- **Does NOT apply to**: E2, Tau (T2D/T2A), C3, A2, A3 machine types (CUD-eligible instead)
- GKE Autopilot workloads also get SUDs

### Committed Use Discounts (CUDs)

#### Resource-based CUDs

- Commit to specific vCPU and memory quantities in a region
- **1-year**: Up to 37% discount | **3-year**: Up to 57% discount
- Locked to machine family within a region
- Best for: predictable, steady-state workloads with known machine family

#### Spend-based CUDs

- Commit to $/hour spend on compute across a region
- **1-year**: Up to 25% discount | **3-year**: Up to 46% discount
- Flexible across machine families, GPU types, and regions (within scope)
- Best for: diverse workloads, organizations that change machine types frequently

### Spot / Preemptible VMs

- Up to 91% discount on spare GCP capacity
- Spot: Can be reclaimed with 30-second notice; no max lifetime
- Preemptible (legacy): 24-hour max lifetime, 30-second preemption notice
- Best for: batch processing, CI/CD, fault-tolerant stateless workloads, ML training
- Combine with MIG autoscaler for automatic Spot + On-Demand fallback

### Free Tier

- Compute: 1 e2-micro VM/month (us-central1, us-west1, us-east1)
- Cloud Storage: 5 GB Standard, 5,000 Class A ops, 50,000 Class B ops
- BigQuery: 1 TB queries/month, 10 GB storage/month
- Cloud Functions: 2M invocations/month
- Many other services have always-free quotas

## Key Service Pricing Notes

### Compute Engine

- **Custom machine types**: Pay for exact vCPU and memory — avoid paying for waste
- **e2 series**: Cheapest general purpose, shared-core options (e2-micro, e2-small)
- **Tau T2D/T2A**: Best price-performance for scale-out (T2A is Arm-based, cheapest)
- **C3**: Latest gen compute-optimized, replaces C2
- Sole-tenant nodes: Pay for the full node regardless of utilization

### Cloud Storage

| Storage Class | $/GB/month | Min Retention | Use Case                   |
| ------------- | ---------- | ------------- | -------------------------- |
| Standard      | $0.020     | None          | Frequently accessed        |
| Nearline      | $0.010     | 30 days       | Monthly access             |
| Coldline      | $0.004     | 90 days       | Quarterly access           |
| Archive       | $0.0012    | 365 days      | Annual access / compliance |

_Prices approximate, us-central1. Operation costs increase for colder classes._

**Autoclass**: Automatically moves objects between tiers based on access — $0.0025/1000 objects/month management fee + tier storage costs.

### Persistent Disk Pricing

| Type              | $/GB/month    | IOPS         | Best For              |
| ----------------- | ------------- | ------------ | --------------------- |
| pd-standard (HDD) | $0.04         | Low          | Dev/test, backups     |
| pd-balanced (SSD) | $0.10         | Moderate     | General purpose       |
| pd-ssd            | $0.17         | High         | Production, databases |
| pd-extreme        | $0.125 + IOPS | Very high    | Extreme performance   |
| Hyperdisk         | Configurable  | Configurable | Next-gen high perf    |

### Data Transfer

- Intra-zone: Free
- Cross-zone (same region): $0.01/GB
- Cross-region (within continent): $0.01/GB
- Cross-region (intercontinental): $0.02-0.08/GB
- Internet egress (Premium tier): Tiered — $0.12/GB first 1TB, decreasing with volume
- Internet egress (Standard tier): ~$0.085/GB (fewer PoPs, slightly cheaper)
- Private Google Access: Free (allows VMs without external IPs to reach Google APIs)
- Cloud Interconnect: Reduced egress rates ($0.02-0.05/GB depending on region)

### BigQuery

| Model              | Cost             | Best For                        |
| ------------------ | ---------------- | ------------------------------- |
| On-demand          | $6.25/TB scanned | Variable, low-volume queries    |
| Standard edition   | $0.04/slot-hour  | Medium workloads, autoscale     |
| Enterprise edition | $0.06/slot-hour  | Cross-region, advanced features |
| Enterprise Plus    | $0.10/slot-hour  | Advanced security, compliance   |

- Long-term storage (>90 days untouched): 50% cheaper — automatic, no action needed
- Flat-rate legacy: Being migrated to editions

### Cloud SQL

- Machine types mirror Compute Engine pricing
- HA: ~2x single instance cost
- Storage: SSD ($0.17/GB) vs HDD ($0.09/GB)
- Automated backups: Charged at storage rates
- CUD available: 1yr (~25% discount), 3yr (~52% discount)

## Discount Stacking Rules

1. SUDs are automatic — apply before CUDs are evaluated
2. CUDs replace SUDs when CUD provides deeper discount (they don't stack)
3. Spot pricing is independent — does not stack with CUDs/SUDs
4. BigQuery editions commitments are separate from compute CUDs
5. Free tier applies before any paid pricing
6. Volume discounts (networking) apply automatically at tier thresholds

## Savings Calculation Formula

```
Monthly Savings = (On-Demand Price - Optimized Price) × Usage Hours × Instance Count
Annual Savings = Monthly Savings × 12
ROI Period = Implementation Cost / Monthly Savings
```

## Common Savings Benchmarks

- Right-sizing (1 size down): 30-50% per VM
- Custom machine type (exact fit): 5-20% vs nearest predefined
- e2 vs n1 migration: 15-30% cost reduction for eligible workloads
- T2A (Arm) vs equivalent x86: ~20% cheaper
- Cloud Storage Standard → Nearline: 50% storage cost reduction
- Cloud Storage Standard → Archive: 94% storage cost reduction
- Spot/Preemptible VMs: 60-91% vs On-Demand
- 1yr resource-based CUD: ~37% discount
- 3yr resource-based CUD: ~57% discount
- 1yr spend-based CUD: ~25% discount
- 3yr spend-based CUD: ~46% discount
- SUDs (full month): Up to 30% automatic discount
- BigQuery on-demand → editions: variable, often 30-50% for heavy users
- Standard vs Premium network tier: ~30% savings on egress
