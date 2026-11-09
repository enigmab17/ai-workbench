# Working rules

## Working style
- Make small changes and explain them briefly
- Read existing code first and follow its conventions
- Ask before adding new packages or dependencies
- Say when you're unsure; don't guess APIs or versions

## Tests
- Write one failing test first, run it, and show the red result
- Confirm it fails for the right reason, then implement the smallest change
- If a result contradicts a change just made, do a full rebuild before trusting it

## Code
- Prefer self-documenting code; comment only to explain why
- Keep it simple (YAGNI); no abstractions without a concrete need
- Never log or commit secrets or PII