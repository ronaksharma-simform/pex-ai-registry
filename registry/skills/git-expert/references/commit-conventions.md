# Conventional Commits Reference

## Specification

Based on https://www.conventionalcommits.org/en/v1.0.0/

## Full Format

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

## Types with Examples

### feat — New feature

```
feat(payments): add Stripe webhook handler

Listens for payment_intent.succeeded and payment_intent.failed
events to update order status in real-time.

Refs: PROJ-789
```

### fix — Bug fix

```
fix(auth): prevent session fixation on login

Regenerate session ID after successful authentication to prevent
session fixation attacks. Previously the pre-auth session ID was
retained.

Refs: PROJ-102
```

### docs — Documentation

```
docs(api): add rate limiting section to API guide
```

### style — Formatting (no logic change)

```
style(components): apply prettier formatting to Button module
```

### refactor — Restructure without changing behaviour

```
refactor(db): extract connection pooling into dedicated module

Moves pool configuration and health-check logic out of the
monolithic db.ts into pool-manager.ts for testability.
```

### test — Test additions or corrections

```
test(auth): add integration tests for OAuth2 PKCE flow
```

### chore — Build, deps, tooling

```
chore(deps): upgrade express from 4.18 to 4.21

Security patch for CVE-2024-XXXXX.
```

### perf — Performance improvement

```
perf(search): add database index on users.email column

Reduces login query time from ~120ms to ~3ms for tables
with 1M+ rows.
```

### ci — CI/CD changes

```
ci(github): add Node 20 to test matrix
```

## Breaking Changes

Add `BREAKING CHANGE:` in the footer OR append `!` after type:

```
feat(api)!: change authentication endpoint to /v2/auth

BREAKING CHANGE: The /v1/auth endpoint is removed. All clients
must migrate to /v2/auth which requires PKCE.
```

## Multi-Line Body Guidelines

- Wrap at 72 characters per line.
- Separate from summary with a blank line.
- Explain the motivation — what problem does this solve?
- Contrast with previous behaviour if relevant.

## Scope Suggestions

Use the module, component, or feature area as scope:

- `auth`, `payments`, `api`, `db`, `ui`, `config`, `deps`, `docs`
- Keep scopes consistent across the project.

## Co-Authorship

When pair programming or AI-assisted:

```
feat(dashboard): add real-time metrics widget

Co-Authored-By: Developer Name <dev@example.com>
Co-Authored-By: Claude <noreply@anthropic.com>
```
