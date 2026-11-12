# .NET rules

## Versions
- In existing solutions, respect `global.json` and each project's `TargetFramework`; don't upgrade unasked
- New solutions: use the latest LTS SDK, pin it in `global.json` (`rollForward: latestFeature`) and set `TargetFramework` explicitly

## Approved packages
- Testing framework: MSTest (alternative: xUnit)
- Assertions: Shouldly
- Mocking: NSubstitute (alternative: Moq)
- API communication: Microsoft.Extensions.Http.Resilience
- Logging: Serilog, Serilog.Sinks.Console, Serilog.Sinks.File (see `serilog.md`)
- Caching: Microsoft.Extensions.Caching.Hybrid

## Blocked packages
Don't add or recommend these; if a solution already uses one, say so but don't remove it unasked.
- FluentAssertions v8+: moved to a paid commercial licence (2025); use Shouldly
- AutoMapper, MediatR (newer versions): moved to commercial licences (2025); map by hand, call services directly
- MassTransit v9+: moved to a commercial licence

## Project settings
- New projects: `Nullable` and `ImplicitUsings` enabled, `TreatWarningsAsErrors` on
- Existing projects: don't introduce new warnings
- Put shared settings in `Directory.Build.props`; use central package management (`Directory.Packages.props`) once there is more than one project
- Follow `.editorconfig` where present; use file-scoped namespaces in new files

## Code
- Follow the standard Microsoft C# coding conventions
- Large XML doc comments aren't required
- Async all the way: no `.Result`, `.Wait()` or `async void` (except event handlers); accept and pass on `CancellationToken`
- Use the built-in dependency injection container with constructor injection; no service locator
- Strongly typed configuration: bind with the options pattern (`IOptions<T>`) and validate at startup (`ValidateOnStart`); no hard-coded URLs or keys
- Log with `ILogger<T>` and message templates (`"Order {OrderId} failed"`), never string interpolation

## Testing
- Use the test framework and mocking library already in the solution; otherwise use the defaults above
- No static loggers or other global state in tests (e.g. `Log.Logger`)
- If the build reports MSB3021 (output locked by a running process), stop that process and rebuild; don't trust test results from that build

## Commands
- Build: `dotnet build`
- Test: `dotnet test`
- Full rebuild (only if results look wrong): `dotnet build --no-incremental`
- Run: `dotnet run --project <ProjectName>`
- Watch: `dotnet watch`
- Before reporting done, run build and test and report the results