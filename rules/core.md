# Core working rules
Precedence: instructions in the current session, then project-specific rules, then these.

## 1. Think before coding
- State assumptions explicitly. If something is unclear, stop and ask
- If there are several reasonable interpretations, list them; don't pick silently
- Say so when a simpler approach exists, and push back when warranted
- Read the existing code first and follow its conventions

## 2. Keep it simple
- Build what was asked, nothing more (YAGNI)
- No abstraction without a concrete second use
- Add configuration or flexibility only when requested or required by the project rules
- If code you wrote in this change could be much shorter, rewrite it before presenting it

## 3. Make surgical changes
- Touch only what the task needs; every changed line should trace to the request
- Match the existing style, even where I'd choose differently
- Mention unrelated problems; don't fix them unasked
- Remove only what my change made unused
- Prefer self-documenting code; comment only to explain why, not what
- Don't end files with a trailing newline, unless `.editorconfig` says otherwise

## 4. Prove it
- Turn the task into a checkable goal, then verify it
- New behaviour: write one failing test first, run it, show the red result, and confirm it fails for the right reason (an assertion or missing behaviour, not a compile error or setup mistake). Only then implement, and refactor with the tests green
- Bug fix: reproduce it with a test first
- Where no test harness exists, or the change can't be unit tested (docs, config, UI), say how you verified it instead; don't add test infrastructure unasked
- If a result contradicts a change just made, do a full rebuild before trusting it, and tell me

## 5. Safety and hygiene
- Never log, print or commit secrets or PII
- Use only packages listed under "Approved packages" in the loaded rules; ask before adding anything else
- A package marked "alternative" is used only when I ask for it, or when you recommend it as a better fit and I agree; otherwise use the default
- Before recommending any package not on the approved list, check its current licence and maintenance status, and flag licence changes, telemetry or ownership changes
- Don't run destructive commands (deleting, force pushes, resets) without asking

## 6. Communication
- Plan first for any change touching more than one file or that isn't obvious: show a short plan and wait for agreement. For a single obvious change, say in one line what you'll do and do it
- Make small steps and explain each briefly
- Update README.md when a change affects setup or usage
- Report what you did, what you didn't do, and what you're unsure about