# Excel Estimation Structure

## Sheet 1: Summary

- Project name, client, date
- Total hours by role (Dev, QA, PM, DevOps)
- Total cost at blended rate
- Three scenarios: Optimistic (-15%), Realistic, Pessimistic (+25%)
- PexAI savings line item

## Sheet 2: Task Breakdown

| Column           | Description                              |
| ---------------- | ---------------------------------------- |
| Task ID          | Sequential identifier                    |
| Category         | Feature area / module                    |
| Task Description | What needs to be done                    |
| Role             | Dev / QA / PM / DevOps                   |
| Base Hours       | Estimated effort                         |
| Complexity       | Simple / Medium / Complex / Very Complex |
| Multiplier       | 1.0 / 1.3 / 1.6 / 2.0                    |
| Adjusted Hours   | Base \* Multiplier (formula)             |
| Dependencies     | Other task IDs                           |
| Notes            | Assumptions, risks                       |

## Sheet 3: Assumptions & Risks

- Key assumptions underlying the estimate
- Identified risks with impact on hours
- Exclusions / out-of-scope items

## Formulas

- Adjusted Hours = Base Hours \* Complexity Multiplier
- QA Hours = SUM(Dev Adjusted Hours) \* QA Ratio
- PM Hours = SUM(All Hours) \* PM Ratio
- Total = SUM(Adjusted Hours) + QA + PM
