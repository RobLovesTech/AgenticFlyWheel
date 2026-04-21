AgenticFlywheel Execution Layer

Purpose
- Define the AFW runtime layer that complements AIPs without replacing them.
- Standardize local execution artifacts, review flows, recovery behavior, and host routing.
- Keep runtime state private, local-first, and subordinate to repo-tracked packet docs.

Control Plane vs Runtime Layer
- Control Plane
  - Repo-tracked, reviewable, canonical.
  - Primary artifacts: `docs/AIP_FRAMEWORK.md`, `docs/Agent Implementation Packets/**`, `docs/features/REGISTRY.yaml`, `docs/ai/**`.
  - Used for decisions that must survive handoff, review, and implementation.
- Runtime Layer
  - Repo-local, gitignored, advisory.
  - Primary artifacts live under `.agentic-flywheel/state/`.
  - Used for execution-time memory, review logs, checkpoints, and host preferences.

Canonical Runtime Paths
- `.agentic-flywheel/state/checkpoints/`
- `.agentic-flywheel/state/learnings.jsonl`
- `.agentic-flywheel/state/reviews.jsonl`
- `.agentic-flywheel/state/timeline.jsonl`
- `.agentic-flywheel/state/question-prefs.json`

Precedence Rules
- Packet docs always outrank runtime state on conflict.
- `REVIEWS.md` is the only review artifact an implementation prompt may treat as authoritative.
- Runtime logs may inform drafting, summarization, and recovery, but they do not change contracts or acceptance by themselves.
- If a runtime conclusion matters, it must be promoted into `REVIEWS.md`, `CHECKLIST.*`, or another packet doc before it can gate work.

Data Contracts
- `checkpoints/*.md`
  - Required sections: `Summary`, `Decisions`, `Remaining Work`, `Notes`.
  - Optional metadata header: feature slug, branch, checkpoint time.
- `learnings.jsonl`
  - Object shape: `type`, `key`, `insight`, `confidence`, optional `files`, `created_at`.
  - Intended for durable local patterns, pitfalls, and preferences.
- `reviews.jsonl`
  - Object shape: `feature_slug`, `branch`, `commit`, `prompt`, `status`, `via`, `findings_count`, `created_at`.
  - One line per completed review run.
- `timeline.jsonl`
  - Lightweight append-only run log with event name, prompt name, branch, feature slug, and timestamp.
- `question-prefs.json`
  - Local-only interaction preferences and lightweight session state such as active guard boundaries.

Review Promotion Flow
1) Discovery or review prompt writes provisional output to runtime state.
2) The user or a follow-on prompt chooses which findings are accepted.
3) Accepted conclusions are written into `docs/Agent Implementation Packets/<slug>/REVIEWS.md`.
4) If accepted conclusions affect implementation scope, update `README.md`, `CONTRACTS.md`, `CHECKLIST.yaml`, or other packet docs.
5) `AGENT_PROMPT_GENERATOR.md` reads packet docs, not raw runtime logs.

Host Strategy
- Codex is the primary host in v1.
- Claude and Cursor should receive compatible, smaller overlays after the Codex path is stable.
- Host configs should route natural-language commands for planning, reviews, checkpointing, QA, shipping, and guard mode to the matching AFW prompt.

Privacy and Retention
- First cut is local-only. No hosted telemetry.
- Runtime state may include implementation notes and branch names; treat it as private project state.
- Store only what improves recovery and review quality.
- Delete stale or misleading runtime artifacts when they no longer reflect current packet truth.

Non-Goals
- No browser binary, Chrome extension, or hidden home-directory dependency.
- No requirement to sync runtime state across machines.
- No hosted analytics or community telemetry in v1.
