# Architecture rules

## Decisions
- For a significant decision (new project or service, data store, cross-cutting pattern, breaking contract change), present the options with trade-offs and a recommendation, then record the outcome as a short ADR in `docs/adr/NNNN-title.md`: context, decision, alternatives, consequences
- Ask before creating `docs/adr/` in a project that doesn't have it

## Structure
- Follow SOLID principles, and say where applying them would add bloat or indirection for little gain
- Start with the simplest structure that works; split into layers, projects or services only when a concrete need appears
- In new code, organise by feature rather than by technical layer, unless the project already does otherwise
- Dependencies point inward: business logic doesn't depend on frameworks, databases or HTTP
- Keep I/O at the edges so business logic can be tested without infrastructure

## Boundaries and contracts
- Validate at system boundaries; trust internal calls
- Keep DTOs separate from domain models; never expose persistence entities directly
- Check external APIs' real responses (fields, nulls, error codes, deprecation), not just the sample responses provided
- Public contracts (APIs, events, database schemas) don't break without explicit approval

## Errors and resilience
- Fail fast on invalid configuration at startup
- Return expected failures as results or status codes; use exceptions for the unexpected
- Every outbound call has a timeout; retry only transient failures of idempotent operations, with backoff

## Caching
- Each cached type has a configurable TTL; 0 turns caching off for that type
- Never cache failures or "not found" results

## Observability
- Structured logs carrying a correlation or trace ID; prefer OpenTelemetry-compatible tooling
- Log at boundaries and on failure, not on every step

## Configuration and data
- Configuration comes from the environment and config providers, never hard-coded; secrets come from a secret store, never the repository
- Schema changes go through migrations; never edit a migration that has been applied