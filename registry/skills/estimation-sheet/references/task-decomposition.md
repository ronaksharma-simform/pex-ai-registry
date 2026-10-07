# Task Decomposition Guidelines

## Right-Sized Tasks

- **Minimum:** 4 hours (anything less, combine with related work)
- **Ideal:** 10-40 hours
- **Maximum:** 60 hours (anything larger, decompose further)

## Task Categories

| Category                | Typical Range | Notes                     |
| ----------------------- | ------------- | ------------------------- |
| UI Component            | 8-24 hrs      | Per screen/feature        |
| API Endpoint            | 4-16 hrs      | CRUD set typically 16 hrs |
| Database Schema         | 4-8 hrs       | Per entity group          |
| Authentication          | 16-40 hrs     | Depends on providers      |
| Third-party Integration | 16-40 hrs     | Per integration           |
| Testing (Unit)          | 15-20% of dev | Per feature area          |
| Testing (E2E)           | 10-15% of dev | Per critical flow         |
| DevOps/CI-CD            | 16-40 hrs     | Initial setup             |
| Documentation           | 8-16 hrs      | Per major feature         |

## Complexity Multipliers

- **Simple:** 1.0x — Well-understood, standard patterns
- **Medium:** 1.3x — Some unknowns, moderate complexity
- **Complex:** 1.6x — Significant unknowns, novel patterns
- **Very Complex:** 2.0x — Research required, cutting edge
