# AWS Pricing Models & Discount Mechanisms Reference

## Pricing Models Overview

### On-Demand Pricing

- Pay per second (Linux) or per hour (Windows) with no commitment
- Full list price — used as baseline for savings calculations
- Best for: unpredictable workloads, short-term needs, initial sizing

### Reserved Instances (RIs)

- 1-year or 3-year commitment for specific instance type in a specific region
- **Standard RIs**: Up to 72% discount, limited modification (size flexibility within family)
- **Convertible RIs**: Up to 66% discount, can change instance family/OS/tenancy
- Payment options: No Upfront (lowest commitment), Partial Upfront, All Upfront (deepest discount)
- Applies to: EC2, RDS, ElastiCache, Redshift, OpenSearch
- **Key metric**: RI Utilization — target >80%, RI Coverage — target 60-80% of steady-state

### Savings Plans

- **Compute Savings Plans**: Up to 66% discount, applies across EC2, Fargate, Lambda — most flexible
- **EC2 Instance Savings Plans**: Up to 72% discount, locked to instance family + region — deepest discount
- **SageMaker Savings Plans**: Up to 64% discount for ML workloads
- Commitment: $/hour for 1 or 3 years
- Unused commitment is wasted — size commitment carefully

### Spot Instances

- Up to 90% discount on spare EC2 capacity
- Can be interrupted with 2-minute notice
- Best for: batch processing, CI/CD, stateless web workers, big data, ML training
- Use Spot Fleet with diversification across instance types and AZs
- Combine with On-Demand base capacity via mixed instances policy

### Sustained Use (Implicit)

- AWS does not offer SUDs — unlike GCP, there's no automatic discount for sustained usage
- Commitment discounts (RIs/SPs) serve this purpose

## Key Service Pricing Notes

### EC2

- Graviton instances: ~20% cheaper than x86 equivalents
- gp3 EBS: 20% cheaper than gp2 with higher baseline IOPS/throughput
- Latest generation (m7g, c7g, r7g): better price-performance than m5, c5, r5
- Data transfer: First 100GB/month egress to internet is free

### S3

| Storage Class              | $/GB/month              | Use Case                    |
| -------------------------- | ----------------------- | --------------------------- |
| Standard                   | $0.023                  | Frequently accessed         |
| Intelligent-Tiering        | $0.023 + monitoring fee | Unknown/changing access     |
| Standard-IA                | $0.0125                 | Infrequent (>30 days)       |
| One Zone-IA                | $0.01                   | Infrequent, non-critical    |
| Glacier Instant Retrieval  | $0.004                  | Archive, millisecond access |
| Glacier Flexible Retrieval | $0.0036                 | Archive, minutes-hours      |
| Glacier Deep Archive       | $0.00099                | Long-term archive           |

_Prices approximate, us-east-1. Check current pricing._

### Data Transfer

- Intra-AZ: Free (same AZ, using private IP)
- Cross-AZ: $0.01/GB each direction
- Cross-Region: $0.02/GB (varies by region pair)
- Internet Egress: Tiered — $0.09/GB first 10TB, decreasing with volume
- NAT Gateway: $0.045/hr + $0.045/GB processed
- VPC Endpoint (Gateway): Free for S3 and DynamoDB
- VPC Endpoint (Interface): $0.01/hr + $0.01/GB

### RDS

- Multi-AZ: ~2x single-AZ cost
- Storage: gp3 cheaper than gp2 with higher baseline
- Automated backups: Free up to DB size, charged beyond retention
- Aurora Serverless v2: $0.12/ACU-hour, min 0.5 ACU

### EBS Volume Comparison

| Type | $/GB/month    | IOPS              | Throughput    | Best For                |
| ---- | ------------- | ----------------- | ------------- | ----------------------- |
| gp3  | $0.08         | 3,000 base (free) | 125 MB/s base | General purpose         |
| gp2  | $0.10         | 3 IOPS/GB         | Burst         | Legacy (migrate to gp3) |
| io2  | $0.125 + IOPS | Up to 64,000      | 1,000 MB/s    | High performance        |
| st1  | $0.045        | N/A               | 500 MB/s      | Throughput (HDD)        |
| sc1  | $0.015        | N/A               | 250 MB/s      | Cold HDD                |

## Discount Stacking Rules

1. Spot pricing is independent — does not stack with RIs/SPs
2. RIs and Savings Plans do NOT stack — the deeper discount applies first
3. Volume discounts (S3, data transfer) apply automatically at tier thresholds
4. Free tier applies before any paid pricing (first 12 months or always-free)
5. Enterprise Discount Program (EDP): org-level spend commitment for additional discount

## Savings Calculation Formula

```
Monthly Savings = (On-Demand Price - Optimized Price) × Usage Hours × Instance Count
Annual Savings = Monthly Savings × 12
ROI Period = Implementation Cost / Monthly Savings
```

## Common Savings Benchmarks

- Right-sizing (1 size down): 30-50% per instance
- Graviton migration: 20-40% price-performance improvement
- gp2 → gp3 migration: 20% storage cost reduction
- S3 Standard → IA: 45% storage cost reduction
- S3 Standard → Glacier: 80-95% storage cost reduction
- Spot Instances: 60-90% vs On-Demand
- 1yr Compute Savings Plan (No Upfront): ~30% discount
- 3yr Compute Savings Plan (All Upfront): ~52% discount
- NAT Gateway → VPC Endpoints: variable, often 50-80% of NAT data costs
