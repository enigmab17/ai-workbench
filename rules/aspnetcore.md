# ASP.NET Core rules
How to apply `web-api.md` in ASP.NET Core.

## Approved packages
- Testing helpers: Microsoft.AspNetCore.Mvc.Testing
- OpenAPI document: Microsoft.AspNetCore.OpenApi
- API docs UI: Swashbuckle.AspNetCore.SwaggerUI (alternative: Scalar.AspNetCore)
- Logging: Serilog.AspNetCore (see `serilog.md`)

## Structure
- Follow the existing endpoint style (controllers or minimal APIs); for a new project, ask
- Layers: endpoint/controller → service → typed client; separate DTOs from domain models
- Outbound HTTP goes through `IHttpClientFactory` typed clients, with resilience from Microsoft.Extensions.Http.Resilience

## HTTPS
- No HTTP-only launch profile or HTTP URL; use `UseHttpsRedirection`, and `UseHsts` outside Development
- Use the development certificate locally (`dotnet dev-certs https --trust`)

## Behaviour
- Errors: `AddProblemDetails`, `UseExceptionHandler` and `UseStatusCodePages`; make sure responses carry `traceId`
- Use the built-in OpenAPI support; declare responses with `TypedResults` or `Produces`/`ProducesProblem`; map the document and UI in Development only
- Endpoints take a `CancellationToken` and pass it down to every async call
- Health: `AddHealthChecks` and `MapHealthChecks("/health")`
- Rate limiting, when wanted, uses the built-in `AddRateLimiter` middleware

## Testing
- Integration tests use `WebApplicationFactory` from Microsoft.AspNetCore.Mvc.Testing, with outbound HTTP stubbed