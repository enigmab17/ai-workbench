@../AGENTS.md

## Claude Code specifics
- Use plan mode for changes touching more than one file
- Keep replies short; don't restate code I can read in the diff
- When delegating to a subagent, give it the goal, the files to read, and what to return