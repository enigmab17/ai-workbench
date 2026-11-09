# ai-dev-workbench

Personal working rules and configuration for AI coding agents.

## What's here
- `AGENTS.md`: tool-neutral working rules (source of truth)
- `claude/CLAUDE.md`: Claude Code entry point, imports `AGENTS.md`
- `claude/settings.json`: Claude Code permissions
- `claude/rules/`: optional topic rules (for example .NET)

## Install (Claude Code)
1. Clone this repo, for example to `~/ai-dev-workbench`.
2. In `~/.claude/CLAUDE.md`, add: `@~/ai-dev-workbench/claude/CLAUDE.md`
3. Copy or link `claude/settings.json` to `~/.claude/settings.json`.
4. Start a session and run `/context` to confirm the files loaded.

## Principles
- Small changes, explained briefly
- Failing test first, shown red, then implement
- Ask before adding packages
- Never log or commit secrets or PII

MIT licensed.