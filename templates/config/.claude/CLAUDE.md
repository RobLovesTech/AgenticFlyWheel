# AgenticFlywheel Framework

AFW install note:
- If this file already exists in a target repo, merge these AFW-specific instructions into the existing `CLAUDE.md`.
- Preserve the repo’s existing content, tone, and non-AFW rules.
- Add only what Claude needs to discover and use AFW correctly.

This repository uses AgenticFlywheel (AFW) for non-trivial feature work.

Authoritative paths:
- `AGENTS.md`: repo-specific process, paths, and verification commands
- `docs/ai/INDEX.md`: entry point for architecture, coding, testing, security, and ops docs
- `docs/features/REGISTRY.yaml`: feature inventory, dependencies, contracts, and packet links
- `docs/Agent Implementation Packets/**/CHECKLIST.yaml`: canonical execution status for each feature
- `.claude/skills/agentic-flywheel/SKILL.md`: procedural AFW workflow for bootstrap, AIP creation, validation, and handoff

Operating rules:
- Use the local `AGENTS.md` as the first repo-specific source of truth.
- Before changing an existing feature, check the registry and its AIP packet first.
- Use a lightweight or full AIP for non-trivial feature work; do not skip directly to implementation.
- Treat `CHECKLIST.yaml` as the canonical source of task order and completion state.
- Complete the final `Docs & Handoff` phase before considering a feature done.
- Generate `AGENT_PROMPT.txt` last, after packet docs are stable.

Scale guidance:
- No AIP: tiny bug fixes, typos, docs-only edits, or very small refactors
- Lightweight AIP: small, single-sided changes with simple contracts
- Full AIP: multi-system work, contract changes, migrations, rollout flags, or meaningful risk

Intent mapping:
- Requests like `new AIP`, `create AIP for <feature>`, `validate checklist`, `generate AGENT_PROMPT`, or `bootstrap AFW` should use the AFW project skill rather than ad hoc chat.

Keep this file factual and stable. Put repeatable AFW procedures in `.claude/skills/agentic-flywheel/`.
