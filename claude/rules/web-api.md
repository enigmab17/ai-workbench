# Web API rules
- HTTPS only, never HTTP; no http profile or endpoint; HSTS outside Development
- Errors are ProblemDetails with the correct status code (400, 404, 409, 429, 502/503); include the trace ID
- Validate input at the edge and return 400 before calling services
- Use correct verbs and status codes; GET is safe and idempotent; make unsafe operations idempotent with an Idempotency-Key where it matters
- Declare success and error responses on every endpoint (OpenAPI)
- Expose the OpenAPI document and UI in Development only
- No secrets or PII in URLs, logs or error bodies
- Pass CancellationToken from the endpoint down to outbound calls
- Add a health endpoint; consider rate limiting and versioning before the API is public