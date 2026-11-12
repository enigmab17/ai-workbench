# Serilog logging rules
- Never log secrets, sensitive data or PII
- Use Serilog structured logging
- Console: human-readable output
- File: JSON using Serilog's compact JSON formatter
- Roll the file daily, and when it reaches the size limit; include the process start time in the file name
- Retained file count 10 and max file size 5 MB, both configurable
- The process start time in the file name identifies the run; don't add a separate RunId property
- ASP.NET Core: use the request/trace ID as the correlation ID, on every log line and in ProblemDetails; don't generate a custom correlation ID
- ASP.NET Core: always let the startup lines through to the console; the browser launch depends on them