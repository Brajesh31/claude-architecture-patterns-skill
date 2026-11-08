# Architecture Patterns Implementation Playbook

Use this playbook to select, implement, and review architecture patterns. A pattern is justified only when it addresses a concrete requirement or recurring pain.

## 1. Start with boundaries
Map business capabilities, actors, data ownership, external systems, and critical workflows. Draw system context first, then containers, then components only where detail changes a decision.

## 2. Modular monolith
Recommended default for many new products.
- Organize modules around business capabilities, not technical file types alone.
- Keep module APIs explicit.
- Prevent direct access to another module's persistence internals.
- Use domain events or application interfaces for cross-module communication.
- Test dependency rules in CI.
- Split a module into a service only when independent deployment, scaling, ownership, or fault isolation is valuable.

## 3. Layered architecture
Typical flow: transport/controller -> application/use case -> domain -> infrastructure adapter.
- Controllers handle protocol concerns and validation.
- Use cases coordinate business workflows.
- Domain objects enforce business invariants.
- Infrastructure implements persistence and external integrations.
Avoid anemic pass-through layers that add no policy or isolation.

## 4. Hexagonal architecture
Define ports around capabilities the application needs. Implement adapters for databases, HTTP APIs, message brokers, and user interfaces.
- Keep domain/application code independent of vendor SDKs.
- Inject adapters at composition boundaries.
- Test core behavior with in-memory fakes, then test real adapters separately.
Do not create interfaces for every class without a meaningful boundary.

## 5. Event-driven systems
Specify event name, schema, owner, versioning policy, delivery semantics, ordering scope, retention, and replay behavior.
- Assume at-least-once delivery unless the platform proves otherwise.
- Make consumers idempotent.
- Use bounded retries with backoff and a dead-letter process.
- Avoid publishing secrets or unnecessary personal data.
- Monitor consumer lag and failed messages.
Do not claim end-to-end exactly-once processing without proving the full transaction boundary.

## 6. CQRS
Adopt separate read and write models only when query needs or scale justify the complexity.
- Keep command validation and invariants on the write side.
- Define projection rebuild and lag behavior.
- Communicate eventual consistency to clients.
- Test projection replay and schema evolution.

## 7. Saga and distributed workflows
Model each step, timeout, retry, compensation, and terminal failure state. Compensation is a business action, not necessarily a perfect rollback. Provide correlation IDs and an operator recovery path.

## 8. Caching
Choose cache key, TTL, invalidation trigger, stale-data tolerance, and outage behavior. Protect against stampedes and avoid caching authorization-sensitive responses across users. Measure hit rate and origin load.

## 9. Security and operations review
For every architecture, review authentication, authorization, trust boundaries, secret storage, encryption, input validation, auditability, backups, restore tests, health checks, logs, metrics, traces, capacity, and incident ownership.

## 10. Decision record template
Record context, drivers, options, decision, rationale, consequences, risks, and revisit triggers. Include diagrams only when they clarify boundaries or flows.

## Review checklist
- Does each component have a clear responsibility and owner?
- Are dependencies directed and intentional?
- Are failure modes and timeouts defined?
- Are data ownership and consistency guarantees explicit?
- Can the design be operated and debugged?
- Is there a simpler design that meets the same requirements?
