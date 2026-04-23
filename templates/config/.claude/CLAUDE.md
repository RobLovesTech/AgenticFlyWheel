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
- `AgenticFlywheel/prompts/AIP_COLLAB.md`: required active-collaboration intake for new AIP requests unless collaboration readiness is already satisfied
- `AgenticFlywheel/prompts/AIP_NEW.md`: scaffold/write path after collaboration readiness is satisfied
- `docs/Agent Implementation Packets/**/CHECKLIST.yaml`: canonical execution status for each feature
- `AgenticFlywheel/prompts/IMPLEMENTATION_AUDIT.md`: required post-implementation audit gate before packet closure
- `.claude/skills/agentic-flywheel/SKILL.md`: procedural AFW workflow for bootstrap, AIP creation, validation, and handoff

Operating rules:
- Use the local `AGENTS.md` as the first repo-specific source of truth.
- Before changing an existing feature, check the registry and its AIP packet first.
- Use a lightweight or full AIP for non-trivial feature work; do not skip directly to implementation.
- For `new AIP`, `create AIP`, `start AIP`, or packet-sized work, actively collaborate with the user before scaffolding. Confirm goals, scope, non-goals, acceptance, risks, rollout, and verification rather than silently choosing them.
- New full AIPs must record a `Collaboration Summary` in `REVIEWS.md`; AIP-Lite must record it in README.md.
- New full and lite checklists must include `collaboration-readiness` before implementation tasks.
- Treat `CHECKLIST.yaml` as the canonical source of task order and completion state.
- Complete the final `Docs & Handoff` phase before considering a feature done.
- Generate `AGENT_PROMPT.txt` last, after packet docs are stable.
- Run the required implementation audit before packet closure; fix or explicitly disposition findings, re-run targeted verification, and refresh `AGENT_PROMPT.txt` if audit-driven packet changes affect it.

Scale guidance:
- No AIP: tiny bug fixes, typos, docs-only edits, or very small refactors
- Lightweight AIP: small, single-sided changes with simple contracts
- Full AIP: multi-system work, contract changes, migrations, rollout flags, or meaningful risk

Intent mapping:
- Requests like `new AIP` or `create AIP for <feature>` should use the AFW project skill and default to `AIP_COLLAB.md`.
- Requests like `implementation audit`, `validate checklist`, `generate AGENT_PROMPT`, `update AFW`, or `bootstrap AFW` should use the AFW project skill rather than ad hoc chat.

Keep this file factual and stable. Put repeatable AFW procedures in `.claude/skills/agentic-flywheel/`.
