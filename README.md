# ai-workbench
Personal working rules and configuration for AI coding agents. Tool-neutral markdown, referenced from projects, never copied.

## What's here
- `rules/`: one topic per file, tool-neutral
  - `core.md`: how I work (think first, keep it simple, surgical changes, prove it, safety, communication)
  - `architecture.md`, `testing.md`, `git.md`: rules for every project
  - `dotnet.md`, `aspnetcore.md`, `web-api.md`, `serilog.md`: stack rules, including approved packages
- `profiles/`: bundles of rules, so a project references one file
  - `base.md`: core + architecture + testing + git; load globally
  - `dotnet-webapi.md`: dotnet + aspnetcore + web-api + serilog
- `claude/`: Claude Code adapter
  - `CLAUDE-GLOBAL.md`: global entry point; imports `profiles/base.md` and adds Claude specifics
  - `settings.json`: permissions

## How it fits together
```
~/.claude/CLAUDE.md ──► claude/CLAUDE-GLOBAL.md ──► profiles/base.md ──► rules/core, architecture, testing, git
<project>/AGENTS.md ──► profiles/dotnet-webapi.md ──► rules/dotnet, aspnetcore, web-api, serilog
```
Profiles use `@path` lines. Claude Code (and Gemini CLI) follow them as imports. Other agents see a plain path plus an instruction to read it.

The examples assume the repo is cloned to `~/ai-workbench`. If yours lives elsewhere, substitute that path.

## Install (once per machine)

### Claude Code
1. Clone the repo:
   ```bash
   cd ~
   git clone https://github.com/enigmab17/ai-workbench.git
   ```

2. In `~/.claude/CLAUDE.md` (create it if missing), add:
   ```
   @~/ai-workbench/claude/CLAUDE-GLOBAL.md
   ```

3. Link the settings file so edits in this repo apply automatically.

   **Windows (PowerShell).** Turn on Developer Mode first (Settings, For developers), or use an elevated prompt. Move any existing `~\.claude\settings.json` aside, then:
   ```powershell
   New-Item -ItemType SymbolicLink -Path "$HOME\.claude\settings.json" -Target "$HOME\ai-workbench\claude\settings.json"
   ```

   **macOS / Linux:**
   ```bash
   ln -s ~/ai-workbench/claude/settings.json ~/.claude/settings.json
   ```

   If linking isn't possible, copy the file instead and re-copy after changes.

4. Start a session and run `/context` to confirm the rules loaded. Claude Code asks once to approve imports from outside the project.

### Other agents
Put this in the agent's global instructions file (e.g. `~/.codex/AGENTS.md`, `~/.gemini/GEMINI.md`, or Copilot's user instructions):
```
Read and follow ~/ai-workbench/profiles/base.md and every rule file it lists.
```

## Use in a project
Add the stack profile to the project's `AGENTS.md`, the cross-agent convention:
```markdown
## Shared rules
Read and follow ~/ai-workbench/profiles/dotnet-webapi.md and every rule file it lists.
@~/ai-workbench/profiles/dotnet-webapi.md
```
Then give the project a `CLAUDE.md` containing just:
```
@AGENTS.md
```
Project-specific rules go below the shared ones in `AGENTS.md` and take precedence.

## Adding to it
- New topic: add `rules/<topic>.md`, one topic per file, short imperative bullets
- New stack: add `profiles/<stack>.md` listing its rule files
- New folders must be un-ignored in `.gitignore` (it ignores everything by default)

## Principles
- Small changes, explained briefly
- Never log or commit secrets or PII

MIT licensed.

## Credits
The working-rule structure (think before coding, simplicity first, surgical changes, goal-driven execution) is adapted from [multica-ai/andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills), whose `CLAUDE.md` is itself derived from Andrej Karpathy's observations on common LLM coding mistakes. The wording here is my own, extended with my own rules (TDD with a visible red test, safety and hygiene, communication).