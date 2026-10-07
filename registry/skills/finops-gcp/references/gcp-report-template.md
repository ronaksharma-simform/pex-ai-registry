# GCP FinOps Report Template

## Document Structure

### 1. Cover Page

- Client Name
- Report Title: "Google Cloud Cost Optimization Report"
- Date
- Prepared By: [Your Company Name]
- Confidentiality Notice

### 2. Executive Summary (1-2 pages)

- Current monthly GCP spend
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

#### 3.1 Organization & Project Structure

- Organization / Folder hierarchy
- Number of projects, billing accounts, regions in use
- Support plan level

#### 3.2 Billing Overview

- Monthly spend trend (last 6-12 months) — table and trend description
- Top 10 services by spend — table with monthly cost
- Spend by project/team/label — table with allocation
- Label coverage assessment — percentage of spend labeled

#### 3.3 Current Commitment Coverage

- Active CUDs (resource-based and spend-based) — commitment, utilization, expiry dates
- Sustained Use Discount effectiveness
- Spot/Preemptible VM usage percentage
- On-Demand vs committed/discounted ratio

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

- Delete unattached Persistent Disks
- Release unused static IPs
- Terminate idle VMs
- Apply Active Assist Recommender suggestions

#### 4.2 Medium-Term Optimizations (2-6 weeks)

- Right-size VMs and databases
- Optimize Cloud Storage tiers and lifecycle policies
- Implement instance schedules for non-production
- Right-size BigQuery slots or switch pricing model
- Switch to custom machine types for better fit

#### 4.3 Strategic Optimizations (1-3 months)

- Purchase Committed Use Discounts (resource or spend-based)
- Migrate to cost-efficient machine types (e2, Tau, C3)
- Architecture refactoring for cost efficiency
- GKE Autopilot migration
- Serverless migration (Cloud Run, Cloud Functions)

### 5. Commitment Strategy

- Current CUD/SUD coverage analysis
- Resource-based vs spend-based CUD recommendation per workload
- Recommended CUD purchases — table with:
  - Service / Machine family
  - Type (resource-based / spend-based)
  - Term (1yr/3yr)
  - Commitment amount
  - Expected savings
- SUD optimization (ensure VMs run full-month for max discount)
- CUD expiry calendar and renewal plan
- BigQuery editions commitment recommendation

### 6. Governance Recommendations

- Labeling strategy and mandatory labels (Organization Policy enforcement)
- Budget alert configuration per project
- Billing export to BigQuery setup
- Organization Policy constraints (allowed machine types, regions, APIs)
- FinOps process recommendations (weekly/monthly reviews)
- Active Assist Recommender integration and automation
- Looker Studio dashboard recommendations

### 7. Implementation Roadmap

| Phase            | Timeline  | Actions      | Expected Savings | Effort |
| ---------------- | --------- | ------------ | ---------------- | ------ |
| 1 — Quick Wins   | Week 1-2  | List actions | $X/month         | Low    |
| 2 — Right-sizing | Week 3-6  | List actions | $X/month         | Medium |
| 3 — Commitments  | Month 2   | List actions | $X/month         | Low    |
| 4 — Architecture | Month 2-3 | List actions | $X/month         | High   |

### 8. Savings Summary Table

| Category              | Monthly Savings | Annual Savings | Effort | Priority |
| --------------------- | --------------- | -------------- | ------ | -------- |
| Compute Right-sizing  | $X              | $X             | Medium | High     |
| Storage Optimization  | $X              | $X             | Low    | High     |
| Waste Elimination     | $X              | $X             | Low    | Critical |
| CUD Purchase          | $X              | $X             | Low    | High     |
| BigQuery Optimization | $X              | $X             | Medium | High     |
| Networking            | $X              | $X             | Medium | Medium   |
| **TOTAL**             | **$X**          | **$X**         |        |          |

### 9. Appendix

- Detailed resource inventory analyzed
- Full list of idle/orphaned resources
- CUD expiry schedule
- Active Assist Recommender export
- Methodology and data sources
- Glossary of GCP FinOps terms

## Formatting Guidelines

- Use tables for all quantitative data
- Include estimated savings ($/month) for every recommendation
- Color-code priority: Critical (red), High (orange), Medium (yellow), Low (green)
- Use consistent currency formatting (USD with commas)
- Number all recommendations for reference in implementation tracking
- Include Recommender IDs where applicable
