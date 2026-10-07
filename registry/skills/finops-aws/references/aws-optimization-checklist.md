# AWS Cost Optimization Checklist

## 1. Compute — EC2 & Containers

- [ ] Identify idle EC2 instances (<10% avg CPU over 14 days)
- [ ] Identify underutilized EC2 instances (<30% avg CPU over 14 days)
- [ ] Right-size instances — match instance family/size to workload profile (CPU, memory, network, storage)
- [ ] Upgrade to latest generation — m5→m7g (Graviton), c5→c7g, r5→r7g for 20-40% price-performance gain
- [ ] Evaluate Graviton (ARM) for Linux workloads — typically 20% cheaper, 40% better performance
- [ ] Review Spot Instance viability for batch, CI/CD, dev/test, stateless workers
- [ ] Audit Auto Scaling Group min/max/desired — over-provisioned ASGs waste money
- [ ] Check for EC2 instances running outside business hours that could be stopped/scheduled
- [ ] Review ECS Fargate vs EC2 launch type — Fargate for variable, EC2+Spot for steady-state
- [ ] Audit EKS node groups — use Karpenter or Cluster Autoscaler, mix On-Demand + Spot
- [ ] Review Lambda memory allocation vs execution time trade-off (right-size with Power Tuning)
- [ ] Check Lambda Provisioned Concurrency — remove if invocation patterns don't justify it

## 2. Storage — S3

- [ ] Analyze S3 storage class distribution per bucket (S3 Storage Lens)
- [ ] Move infrequently accessed objects to S3-IA (>30 day access pattern)
- [ ] Move archive data to Glacier Instant Retrieval, Glacier Flexible, or Deep Archive
- [ ] Enable S3 Intelligent-Tiering for unpredictable access patterns
- [ ] Configure Lifecycle policies to auto-transition and expire objects
- [ ] Review multipart upload abort policies (incomplete uploads consume storage)
- [ ] Check for versioning-enabled buckets with excessive non-current versions
- [ ] Audit S3 request costs — LIST operations on large buckets can be expensive
- [ ] Enable S3 Storage Lens for org-wide visibility

## 3. Storage — EBS & Snapshots

- [ ] Identify unattached EBS volumes — delete or snapshot and remove
- [ ] Migrate gp2 volumes to gp3 — 20% cheaper with better baseline performance
- [ ] Right-size provisioned IOPS (io1/io2) volumes — check actual IOPS usage
- [ ] Review EBS snapshot retention — delete snapshots older than retention policy
- [ ] Identify orphaned snapshots (source volume deleted)
- [ ] Use Amazon Data Lifecycle Manager (DLM) to automate snapshot lifecycle
- [ ] Check for oversized EBS volumes — actual usage vs provisioned capacity

## 4. Database

- [ ] Identify idle RDS instances (<5% CPU, <100 connections over 14 days)
- [ ] Right-size RDS instances — match db.instance to actual CPU/memory/IOPS needs
- [ ] Evaluate Aurora Serverless v2 for variable workloads (auto-scales 0.5-128 ACUs)
- [ ] Review RDS Multi-AZ necessity per instance — dev/test rarely needs Multi-AZ
- [ ] Migrate RDS gp2 storage to gp3
- [ ] Check RDS provisioned IOPS vs actual consumption
- [ ] Review DynamoDB capacity mode — switch to On-Demand for spiky, Provisioned+Auto-Scaling for steady
- [ ] Audit DynamoDB reserved capacity purchases
- [ ] Right-size ElastiCache nodes — check memory utilization and eviction rates
- [ ] Review Redshift cluster — pause during off-hours, evaluate RA3 nodes for storage flexibility

## 5. Networking & Data Transfer

- [ ] Analyze NAT Gateway data processing costs — often #1 hidden cost
- [ ] Deploy VPC endpoints (Gateway: S3/DynamoDB free; Interface: per-hour + data) to bypass NAT
- [ ] Review cross-AZ data transfer — consider AZ affinity for high-traffic services
- [ ] Audit cross-region data transfer — replicate only what's necessary
- [ ] Optimize CloudFront — increase cache hit rate, use Origin Shield
- [ ] Review Elastic IP costs — unused EIPs now charged ($0.005/hr since Feb 2024)
- [ ] Consolidate load balancers where possible (ALB host/path routing)
- [ ] Check for idle load balancers (no healthy targets, no traffic)
- [ ] Evaluate AWS Global Accelerator necessity vs CloudFront

## 6. Commitment Discounts

- [ ] Calculate RI coverage rate — target 60-80% of steady-state compute
- [ ] Identify expiring RIs — plan renewal or conversion to Savings Plans
- [ ] Evaluate Compute Savings Plans — flexible across EC2, Fargate, Lambda
- [ ] Compare EC2 Instance Savings Plans (deeper discount) vs Compute Savings Plans (more flexible)
- [ ] Model 1-year vs 3-year commitment trade-offs
- [ ] Review No Upfront vs Partial Upfront vs All Upfront payment options
- [ ] Check for unused or underutilized Reserved Instances (RI utilization <80%)
- [ ] Assess Convertible RI exchange opportunities for newer instance types
- [ ] Review RDS Reserved Instances coverage

## 7. Backup & Disaster Recovery

- [ ] Audit AWS Backup retention policies — excessive retention adds cost
- [ ] Review RDS automated backup retention (default 7 days, check if more is needed)
- [ ] Check for manual RDS snapshots that are never cleaned up
- [ ] Audit cross-region backup replication — is it necessary for all resources?
- [ ] Review AMI sprawl — delete old/unused AMIs and their backing snapshots
- [ ] Evaluate DR architecture cost vs business requirements (pilot light vs warm standby)

## 8. Waste & Orphaned Resources

- [ ] Delete unattached EBS volumes
- [ ] Release unused Elastic IPs
- [ ] Remove idle load balancers (ELB/ALB/NLB)
- [ ] Clean up unused ENIs (Elastic Network Interfaces)
- [ ] Delete stale CloudFormation stacks
- [ ] Remove unused VPN connections and Direct Connect virtual interfaces
- [ ] Check for test/dev resources left running (tag-based identification)
- [ ] Review CloudWatch log group retention — set appropriate retention, default is "never expire"

## 9. Governance & Visibility

- [ ] Implement mandatory tagging policy (AWS Organizations Tag Policies)
- [ ] Verify cost allocation tags are activated in Billing Console
- [ ] Set up AWS Budgets with alerts at 50%, 80%, 100% thresholds
- [ ] Enable Cost Anomaly Detection (free, ML-based)
- [ ] Review IAM policies — restrict expensive service launches
- [ ] Implement SCPs to restrict regions, instance types, and services
- [ ] Enable CUR (Cost and Usage Report) for detailed billing analysis
