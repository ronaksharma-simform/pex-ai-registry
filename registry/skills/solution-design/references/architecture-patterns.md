# Common Architecture Patterns

## Monolith

- Single deployable unit
- Best for: Small teams, MVPs, simple domains
- Risk: Scaling bottlenecks, deployment coupling

## Microservices

- Independent services per domain
- Best for: Large teams, complex domains, independent scaling
- Risk: Operational complexity, network latency, data consistency

## Modular Monolith

- Single deployment with internal module boundaries
- Best for: Medium teams, growing complexity, eventual microservices
- Risk: Module coupling if boundaries not enforced

## Event-Driven

- Async communication via events/messages
- Best for: Decoupled systems, real-time processing, CQRS
- Risk: Eventual consistency, debugging complexity

## Serverless

- Function-as-a-service, managed infrastructure
- Best for: Variable workloads, event processing, cost optimization
- Risk: Cold starts, vendor lock-in, execution limits

## Jamstack

- Static frontend + API backends + CDN
- Best for: Content sites, marketing, high-performance frontends
- Risk: Dynamic feature limitations, build time scaling
