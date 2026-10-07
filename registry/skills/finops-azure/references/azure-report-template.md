# Azure FinOps Report Template

## Document Structure

### 1. Cover Page

- Client Name
- Report Title: "Azure Cloud Cost Optimization Report"
- Date
- Prepared By: [Your Company Name]
- Confidentiality Notice

### 2. Executive Summary (1-2 pages)

- Current monthly Azure spend
- Total identified savings opportunity (monthly and annualized)
- Top 5 savings recommendations ranked by impact
- Summary savings breakdown by category:
  - Compute optimization: $X/month
  - Storage optimization: $X/month
  - Commitment & licensing optimization: $X/month
  - Waste elimination: $X/month
  - Networking optimization: $X/month
- Recommended implementation timeline (quick wins vs strategic)
- Risk/effort matrix visualization

### 3. Current State Assessment

#### 3.1 Subscription & Organization Structure

- Management Group hierarchy
- Number of subscriptions, regions in use
- EA/MCA/CSP agreement type and support level

#### 3.2 Billing Overview

- Monthly spend trend (last 6-12 months) — table and trend description
- Top 10 meter categories by spend — table with monthly cost
- Spend by subscription/resource group — table with allocation
- Tag coverage assessment — percentage of spend tagged

#### 3.3 Current Commitment & Licensing Coverage

- Active Azure Reservations — count, utilization rate, expiry dates
- Active Savings Plans — commitment level, utilization rate
- Azure Hybrid Benefit enrollment status
- Dev/Test subscription identification
- Spot VM usage percentage

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

- Delete unattached Managed Disks
- Release unused Public IPs
- Apply Azure Hybrid Benefit to eligible VMs
- Enable Dev/Test pricing on non-production subscriptions

#### 4.2 Medium-Term Optimizations (2-6 weeks)

- Right-size VMs and databases
- Optimize Blob Storage tiers and lifecycle policies
- Implement VM start/stop schedules
- Right-size App Service Plans
- Configure Azure SQL serverless or elastic pools

#### 4.3 Strategic Optimizations (1-3 months)

- Purchase Azure Reservations or Savings Plans
- ARM-based VM migration
- Architecture refactoring for cost efficiency
- Implement Private Endpoints
- AKS optimization with spot node pools

### 5. Commitment & Licensing Strategy

- Current reservation/SP coverage analysis
- Azure Hybrid Benefit opportunity analysis:
  - Windows Server licenses available
  - SQL Server licenses available
  - Estimated savings if fully applied
- Recommended reservation/SP purchases — table with:
  - Service
  - SKU/Family
  - Term (1yr/3yr)
  - Monthly commitment
  - Expected savings
- Dev/Test subscription recommendations
- Expiry calendar and renewal plan

### 6. Governance Recommendations

- Tagging strategy and mandatory tags (with Azure Policy enforcement)
- Budget alert configuration per subscription
- Cost anomaly detection setup
- Azure Policy guardrails (allowed SKUs, regions, resource types)
- FinOps process recommendations (weekly/monthly reviews)
- Azure Advisor integration and automation

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
| AHUB & Licensing     | $X              | $X             | Low    | Critical |
| Networking           | $X              | $X             | Medium | Medium   |
| **TOTAL**            | **$X**          | **$X**         |        |          |

### 9. Appendix

- Detailed resource inventory analyzed
- Full list of idle/orphaned resources
- Reservation/SP expiry schedule
- Azure Advisor recommendations export
- Methodology and data sources
- Glossary of Azure FinOps terms

## Formatting Guidelines

- Use tables for all quantitative data
- Include estimated savings ($/month) for every recommendation
- Color-code priority: Critical (red), High (orange), Medium (yellow), Low (green)
- Use consistent currency formatting (USD with commas)
- Number all recommendations for reference in implementation tracking
- Include Azure Advisor recommendation IDs where applicable
