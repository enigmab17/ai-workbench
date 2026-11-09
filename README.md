# ai-workbench
Personal working rules and configuration for AI coding agents.

## What's here
- `AGENTS.md`: tool-neutral working rules (source of truth)
- `claude/CLAUDE-GLOBAL.md`: Claude Code global entry point, imports `AGENTS.md`
- `claude/settings.json`: Claude Code permissions
- `claude/rules/`: optional topic rules (planned)

## Install (Claude Code)
1. Clone the repo into your home folder:
   ```bash
   cd ~
   git clone https://github.com/enigmab17/ai-workbench.git
   ```

2. Import the global rules. In `~/.claude/CLAUDE.md` (create it if missing), add:
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

4. Start a session and run `/context` to confirm the rules loaded.

## Principles
- Small changes, explained briefly
- Never log or commit secrets or PII

MIT licensed.