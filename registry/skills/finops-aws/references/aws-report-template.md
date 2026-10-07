# AWS FinOps Report Template

## Document Structure

### 1. Cover Page

- Client Name
- Report Title: "AWS Cloud Cost Optimization Report"
- Date
- Prepared By: [Your Company Name]
- Confidentiality Notice

### 2. Executive Summary (1-2 pages)

- Current monthly AWS spend
- Total identified savings opportunity (monthly and annualized)
- Top 5 savings recommendations ranked by impact
- Summary savings breakdown by category:
  - Compute optimization: $X/month
  - Storage optimization: $X/month
  - Commitment optimization: $X/month
  - Waste elimination: $X/month
  - Networking optimization: $X/month
- Recommended implementation timeline (quick wins vs strategic)
- Risk/effort matrix visualization

### 3. Current State Assessment

#### 3.1 Account & Organization Structure

- AWS Organizations hierarchy (if applicable)
- Number of accounts, regions in use
- EA/Support plan level

#### 3.2 Billing Overview

- Monthly spend trend (last 6-12 months) — table and trend description
- Top 10 services by spend — table with monthly cost
- Spend by account/team — table with allocation
- Tag coverage assessment — percentage of spend tagged

#### 3.3 Current Commitment Coverage

- Active Reserved Instances — count, utilization rate, expiry dates
- Active Savings Plans — commitment level, utilization rate
- Spot usage percentage
- On-Demand vs committed ratio

### 4. Findings & Recommendations

#### 4.1 Quick Wins (Implement within 1-2 weeks)

_For each finding:_

- **Finding**: Description of the issue
- **Current State**: What is happening now (with data)
- **Recommendation**: Specific action to take
- **Estimated Savings**: $/month and $/year
- **Effort**: Low / Medium / High
- **Risk**: Low / Medium / High
- **Implementation Steps**: Numbered steps

Example categories:

- Delete unattached EBS volumes
- Release unused Elastic IPs
- Terminate idle resources
- Migrate gp2 → gp3

#### 4.2 Medium-Term Optimizations (2-6 weeks)

- Right-size EC2 instances
- Optimize S3 storage classes
- Implement lifecycle policies
- Right-size RDS instances
- Configure scheduling for non-production

#### 4.3 Strategic Optimizations (1-3 months)

- Purchase Savings Plans / Reserved Instances
- Graviton migration
- Architecture refactoring for cost efficiency
- Implement VPC endpoints
- Containerization/serverless migration

### 5. Commitment Strategy

- Current RI/SP coverage analysis
- Recommended RI/SP purchases — table with:
  - Service
  - Instance type/family
  - Term (1yr/3yr)
  - Payment option
  - Monthly commitment
  - Expected savings
- Optimal coverage target rationale
- Expiry calendar and renewal plan

### 6. Governance Recommendations

- Tagging strategy and mandatory tags
- Budget alert configuration
- Cost anomaly detection setup
- SCP/IAM guardrail recommendations
- FinOps process recommendations (weekly/monthly reviews)

### 7. Implementation Roadmap

| Phase            | Timeline  | Actions      | Expected Savings | Effort |
| ---------------- | --------- | ------------ | ---------------- | ------ |
| 1 — Quick Wins   | Week 1-2  | List actions | $X/month         | Low    |
| 2 — Right-sizing | Week 3-6  | List actions | $X/month         | Medium |
| 3 — Commitments  | Month 2   | List actions | $X/month         | Low    |
| 4 — Architecture | Month 2-3 | List actions | $X/month         | High   |

### 8. Savings Summary Table

| Category             | Monthly Savings | Annual Savings | Effort | Priority |
| -------------------- | --------------- | -------------- | ------ | -------- |
| Compute Right-sizing | $X              | $X             | Medium | High     |
| Storage Optimization | $X              | $X             | Low    | High     |
| Waste Elimination    | $X              | $X             | Low    | Critical |
| Commitment Purchase  | $X              | $X             | Low    | High     |
| Networking           | $X              | $X             | Medium | Medium   |
| **TOTAL**            | **$X**          | **$X**         |        |          |

### 9. Appendix

- Detailed resource inventory analyzed
- Full list of idle/orphaned resources
- RI/SP expiry schedule
- Methodology and data sources
- Glossary of AWS FinOps terms

## Formatting Guidelines

- Use tables for all quantitative data
- Include estimated savings ($/month) for every recommendation
- Color-code priority: Critical (red), High (orange), Medium (yellow), Low (green)
- Use consistent currency formatting (USD with commas)
- Number all recommendations for reference in implementation tracking
