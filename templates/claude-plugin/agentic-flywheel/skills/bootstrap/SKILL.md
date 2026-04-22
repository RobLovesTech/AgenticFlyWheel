---
name: bootstrap
description: Bootstrap AgenticFlywheel in the current repository. Use when the user asks to install AFW, run the bootstrap wizard, or set up native Claude Code support for the framework.
disable-model-invocation: true
argument-hint: [mode-or-notes]
---

Bootstrap AgenticFlywheel in the current repository.

Process:
1. Detect whether the repo is:
   - the AFW framework source repo (`prompts/`, `templates/`, `spec/`)
   - a repo that vendors `AgenticFlywheel/`
   - a repo with installed AFW docs under `docs/`
2. Read `AGENTS.md` first.
3. Prefer these sources:
   - `prompts/SYSTEM_BOOTSTRAP.md` or `AgenticFlywheel/prompts/SYSTEM_BOOTSTRAP.md`
   - `prompts/AGENTS_CONFIG_TAILOR.md` or `AgenticFlywheel/prompts/AGENTS_CONFIG_TAILOR.md`
   - `spec/AIP_FRAMEWORK.md` or `AgenticFlywheel/spec/AIP_FRAMEWORK.md`
4. Inspect the repo before asking questions. Infer architecture, testing, validation, and verification commands from local files wherever possible.
5. Propose a file plan before writing.
6. Show concise diffs before writing.
7. For Claude Code, prefer:
   - `.claude/CLAUDE.md`
   - `.claude/skills/agentic-flywheel/`
   over the legacy `.claude/PROJECT_PROMPT.md` pattern.
8. If `.claude/CLAUDE.md` already exists, preserve it. Add only the minimum AFW-specific facts, paths, and routing rules needed for Claude to use AFW correctly. Do not replace unrelated sections unless the user explicitly asks for that.
9. After edits, summarize changed paths, validation status, and the next AFW command to run.

If no AFW layout exists, explain the missing prerequisite and ask the user whether to vendor or install the framework first.
