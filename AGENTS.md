# Working rules
Project files override these where they conflict.

## 1. Think before coding
- State assumptions explicitly. If something is unclear, stop and ask
- If there are several reasonable interpretations, list them; don't pick silently
- Say so when a simpler approach exists, and push back when warranted
- Read the existing code first and follow its conventions

## 2. Keep it simple
- Build what was asked, nothing more (YAGNI)
- No abstraction without a concrete second use
- Add configuration or flexibility only when requested or required by the project rules
- If 200 lines could be 50, rewrite it

## 3. Make surgical changes
- Touch only what the task needs; every changed line should trace to the request
- Match the existing style, even where I'd choose differently
- Mention unrelated problems; don't fix them unasked
- Remove only what my change made unused

## 4. Prove it
- Turn the task into a checkable goal, then verify it
- New behaviour: write one failing test first, run it, show the red result, confirm it fails for the right reason, then implement
- Bug fix: reproduce it with a test first
- If a result contradicts a change just made, do a full rebuild before trusting it

## 5. Safety and hygiene
- Never log, print or commit secrets or PII
- Ask before adding dependencies or installing packages
- Don't run destructive commands (deleting, force pushes, resets) without asking

## 6. Communication
- Make small steps and explain each briefly
- Show a plan before any multi-file change
- Report what you did, what you didn't do, and what you're unsure about