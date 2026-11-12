# Web API rules
Stack-neutral HTTP API rules. Pair with a stack file (e.g. `aspnetcore.md`).

## Transport and security
- HTTPS only, never HTTP; HSTS outside Development
- Every endpoint requires authentication unless it is explicitly marked anonymous
- No secrets or PII in URLs, logs or error bodies

## Contract
- Use correct verbs and status codes; GET is safe and idempotent; make unsafe operations idempotent with an Idempotency-Key where it matters
- Validate input at the edge and return 400 before calling services
- Errors are Problem Details (RFC 9457) with the correct status code (400, 401, 403, 404, 409, 429, 502/503); include the trace ID
- Pass an upstream error message on to callers only when they can act on it
- Paginate collection endpoints; never return unbounded lists
- When responses are cached, `Cache-Control` mirrors the cache TTL
- Declare success and error responses on every endpoint in the OpenAPI document
- Expose the OpenAPI document and UI in Development only, unless the project says otherwise

## Operations
- Propagate cancellation to outbound calls and set a timeout on each one
- Add a health endpoint
- Before the API is public, ask about versioning, rate limiting and authentication scheme