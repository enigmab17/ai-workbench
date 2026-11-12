# Testing rules
- Add or update tests with each behaviour change
- Name tests so they document themselves: `<MethodName>_When_<Condition>_Should_<ExpectedResult>`
- Test hygiene:
  - No network access
  - No writing into the project folder; use a temp directory
  - No shared global state
  - Keep real-time waits short