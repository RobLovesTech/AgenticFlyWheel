# AgenticFlywheel Claude Plugin

This plugin gives AgenticFlywheel native Claude Code skill entry points instead of relying on pasted prompt files.

Included commands:
- `/agentic-flywheel:bootstrap`
- `/agentic-flywheel:create-aip <feature-slug>`
- `/agentic-flywheel:validate-checklist <path-or-feature-slug>`
- `/agentic-flywheel:generate-agent-prompt <feature-slug>`

Scope:
- This plugin assumes the working repo already contains either:
  - the AFW framework source layout (`prompts/`, `templates/`, `spec/`)
  - a vendored `AgenticFlywheel/` folder, or
  - an installed AFW docs layout under `docs/`
- The plugin is a native command surface for AFW workflows. It does not package the entire framework by itself.

Local development:
```bash
claude --plugin-dir /absolute/path/to/AgenticFlyWheel/templates/claude-plugin/agentic-flywheel
```

Recommended pairing:
- Install the project-local Claude config from `templates/config/.claude/`
- Keep repo facts in `.claude/CLAUDE.md`
- Keep AFW procedures in `.claude/skills/agentic-flywheel/`
