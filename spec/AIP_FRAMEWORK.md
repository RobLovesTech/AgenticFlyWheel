AgenticFlywheel Framework - Agent Implementation Packet (AIP) Specification

Purpose
- Provide a lightweight, self-contained, repeatable structure for large multi-phase changes driven by agentic collaboration between AI agents and humans.
- Minimize cross-linking and context hunting: all needed artifacts live under one folder per feature.
- Enable self-sustaining development momentum where better docs lead to better AI results, which lead to better docs.

Name
- Agent Implementation Packet (AIP)
- Example path: docs/Agent Implementation Packets/<Feature_Slug>/

Core Principles
- Self-contained: Everything required to plan, implement, verify, and track lives in the packet folder.
- Single source of truth: CHECKLIST.yaml is canonical for task status; CHECKLIST.md mirrors it for human scanning.
- Re-issuable prompt: AGENT_PROMPT.txt allows new agent sessions to bootstrap without relying on prior chat history.
- Self-maintaining: Documentation is updated as part of the implementation process, creating flywheel momentum.
- Two-layer operation: repo-tracked AIPs/docs/registry are the control plane; local runtime artifacts under `.agentic-flywheel/state/` are an advisory execution layer.
- Parity: Packets should capture any environment parity needs (e.g., local Postgres == prod Databricks).
- Privacy & security: Document constraints explicitly (e.g., FERPA/COPPA, PII redaction, retention).
- Complete features: AIPs drive implementation of complete, production-ready features, not prototypes.

Minimum Required Sections (Quality Bar)
Every AIP MUST include the following content. Use the templates in `docs/templates/AIP/`:
- README.md
  - Executive Summary (what changes and why)
  - Goals and Non‑Goals (scoping guardrails)
  - Signals & Flags Summary (runtime flags, defaults, core computations in one glance)
  - Scope (Backend, Frontend, Docs)
  - Outcomes, Success Criteria, Rollout Plan, Acceptance
- REVIEWS.md
  - Discovery Reframe
  - Product Review
  - Engineering Review
  - Design Review
  - DevEx Review
  - Outside Voice (optional, non-gating in v1)
  - Accepted Decisions
  - Implementation Audit
  - Open Risks
  - Final Verdict
- CONTRACTS.md
  - Signals & Semantics (exact formulas/algorithms)
  - Buckets/Thresholds & Copy expectations (if any UI surfaces a score)
  - Event & API contracts (fields, optional/fallbacks)
  - Docs Contract (what global docs say after this AIP lands)
- BACKEND_IMPLEMENTATION.md
  - File‑by‑file touchpoints (paths + functions/methods)
  - Flags, feature gates, and pseudocode for non‑trivial logic
  - Data persistence semantics (exact columns and values)
- ORCHESTRATION_AND_UI.md
  - Frontend file‑by‑file tasks (components, utils, constants)
  - Copy/threshold updates and fallbacks
- OBSERVABILITY.md
  - New/updated metrics (names, labels, semantics)
  - Dashboards and validation panels; flicker/stability definitions when applicable
- RUNBOOK.md
  - Flags and defaults; local validation steps; flip/rollback; example queries
- RISKS.md
  - Top risks and mitigations; test coverage calls; back‑compat considerations
- DATA_MODEL.sql
  - DDL diffs (if needed) or explicit “No schema changes” note

Standard Packet Contents
- README.md: Objective, scope, constraints, outcomes
- REVIEWS.md: Review gauntlet output and accepted decisions that implementation agents may rely on
- CHECKLIST.yaml: Canonical phases/tasks, env defaults, acceptance
- CHECKLIST.md: Human-friendly checklist and notes
- AGENT_PROMPT.txt: Restartable instructions for agents
- CONTEXT.md: Decisions, constraints, environment defaults, acceptance goals
- CONTRACTS.md: API/events/DB contracts & compatibility
- DATA_MODEL.sql: DDL and retention notes for all stores
- BACKEND_IMPLEMENTATION.md: File-level guidance and flags
- ORCHESTRATION_AND_UI.md: Flows and UI changes
- OBSERVABILITY.md: Metrics/logs and quick checks
- RUNBOOK.md: Commands and acceptance
- RISKS.md: Risks and mitigations

Documentation Tasks (required)
- Every AIP MUST include a final phase in CHECKLIST.yaml named "Docs & Handoff" that:
  - Verifies the change is shippable by running the repo’s defined verification commands (tests/build/lint as applicable) for every impacted component before the AIP can be marked `completed`.
  - Updates all packet docs (README/REVIEWS/CONTEXT/RUNBOOK/OBSERVABILITY) to reflect reality.
  - Integrates links into relevant global docs (e.g., docs/ai/INDEX.md) if applicable.
  - Updates core specifications and AI-facing guides (e.g., docs/ai/**, other specs) to reflect the new or changed behavior.
  - Records new/changed env vars in the appropriate repo docs.
  - Captures operator notes (how to verify/rollback) and any UI screenshots if relevant.
  - Confirms parity notes (local == prod) are accurate.
  - Runs the Agent Prompt QA Checklist (docs/templates/AIP/AGENT_PROMPT_QA_CHECKLIST.md) before finalizing AGENT_PROMPT.txt
  - Runs the required implementation audit (`AgenticFlywheel/prompts/IMPLEMENTATION_AUDIT.md`) after implementation, verification, docs sync, and AGENT_PROMPT generation, but before packet closure.
  - Records the audit verdict and accepted findings in packet truth (`REVIEWS.md` for full AIPs, README.md for AIP-Lite).
  - Creates remediation checklist tasks for every actionable audit finding, fixes or explicitly dispositions each finding, and re-runs targeted verification before closure.
  - Refreshes AGENT_PROMPT.txt if audit findings change packet docs, task order, acceptance criteria, or handoff instructions.
  - Includes a final packet-closure task that confirms the audit passed, findings are resolved, and the packet may be marked `completed`.

Authoring Checklist (copy into CHECKLIST.md)
- [ ] README has Exec Summary, Goals/Non‑Goals, Signals/Flags, Scope, Outcomes, Success, Rollout, Acceptance
- [ ] REVIEWS documents the review gauntlet, accepted decisions, open risks, and final verdict
- [ ] REVIEWS documents the implementation audit verdict, accepted findings, remediation evidence, and closure decision
- [ ] CONTRACTS includes formulas, buckets/thresholds, event fields, and fallbacks
- [ ] BACKEND_IMPLEMENTATION lists every file/function to touch and pseudocode for tricky bits
- [ ] ORCHESTRATION_AND_UI lists frontend files and copy changes
- [ ] OBSERVABILITY has metric names/labels and validation dashboard calls
- [ ] RUNBOOK includes flags, commands, queries, and rollback
- [ ] RISKS calls out flicker/instability, drift, and back‑compat
- [ ] AGENT_PROMPT is zero‑context and explicit (file paths, flags, acceptance)

Checklist YAML Schema (informal)
- version: integer
- feature: string (slug)
- status: pending | in_progress | blocked | completed | abandoned | incomplete
- constraints: [string]
- parity: { <key>: boolean }
- env_defaults: { KEY: value }
- phases: [
  { id: string, name: string, description: string, tasks: [
      { id: string, title: string, files: [string], status: pending|in_progress|blocked|completed|abandoned|incomplete }
    ]
  }
]
- verification: { commands: [string], acceptance: [string] }
- Required final gate tasks for full AIPs: `implementation-audit`, `audit-remediation`, `audit-reverify`, `packet-closure`

Completion Status
- `CHECKLIST.yaml` includes a top-level `status` that tracks packet lifecycle.
- Start new packets in `pending` (or `in_progress` once execution begins).
- Use `blocked` when progress is paused on an external dependency, unresolved decision, or failing prerequisite that is documented in packet docs.
- Build verification is required: the AIP must successfully run the repo’s verification commands (tests/build/lint as applicable) before it can be marked `completed`.
- Implementation audit is required: the AIP must run `IMPLEMENTATION_AUDIT.md`, promote accepted findings into packet docs, resolve or explicitly disposition every actionable finding, and re-run targeted verification before it can be marked `completed`.
- When every task in `phases[*].tasks` is marked `completed`, including audit/remediation/reverify/closure tasks, update the top-level `status` to `completed`.
- Mirror the same state at the top of `CHECKLIST.md` so humans can confirm completion quickly.

Usage
1) Scaffold a new AIP from templates (see docs/templates/AIP/ and associated prompts).
2) Fill in README.md, CONTEXT.md, DATA_MODEL.sql as needed for the initiative.
3) During planning, explicitly check for reuse opportunities (shared modules/components/design system) to avoid duplicating patterns. If you identify a new reusable pattern, implement it in the repo’s shared layer/package.
4) Populate CHECKLIST.yaml with phases/tasks and keep statuses current.
5) Generate AGENT_PROMPT.txt late in Docs & Handoff using the Agent Prompt Generator prompt (`AgenticFlywheel/prompts/AGENT_PROMPT_GENERATOR.md`) together with the Authoring Guide (`docs/templates/AIP/AGENT_PROMPT_AUTHORING_GUIDE.md`). Run the Agent Prompt QA Checklist (`docs/templates/AIP/AGENT_PROMPT_QA_CHECKLIST.md`) before finalizing.
6) Run `AgenticFlywheel/prompts/IMPLEMENTATION_AUDIT.md`, fix or explicitly disposition all findings, refresh AGENT_PROMPT.txt if audit-driven packet changes affect it, re-run targeted verification, then complete the packet-closure task and flip the top-level `status` to `completed`.

Zero‑Context Agent Prompt Guidance
- The AGENT_PROMPT.txt MUST:
  - Enumerate concrete file paths to edit and their purpose
  - List flags and defaults
  - Include step‑by‑step tasks and acceptance criteria
  - Use only accepted conclusions from REVIEWS.md; runtime logs under `.agentic-flywheel/state/` are advisory and never override packet docs
  - Instruct the agent to run the implementation audit gate before packet closure and to treat actionable audit findings as completion blockers
  - Reference packet docs by path; avoid relying on chat history
 - Be created after all packet docs are complete (README, REVIEWS, CONTRACTS, BACKEND_IMPLEMENTATION, ORCHESTRATION_AND_UI, OBSERVABILITY, RUNBOOK, RISKS, CONTEXT, DATA_MODEL, CHECKLIST)

Validation (optional, recommended)
- CHECKLIST schema: docs/templates/AIP/CHECKLIST.schema.json
- Validate structure quickly via prompt validators or local scripts if available.
- Execution-layer conventions: spec/EXECUTION_LAYER.md

Features Registry (platform index)
- Location: docs/features/REGISTRY.yaml (+ schema at docs/features/REGISTRY.schema.json)
- Every AIP’s “Docs & Handoff” phase must add or update a registry entry for new/changed features.
- Every AIP’s final phase must include implementation audit, remediation, targeted re-verification, and packet closure gates. AIP-Lite uses the same gate scaled to README.md + CHECKLIST.yaml.

Best Practices
- Keep tasks small and file-scoped where possible.
- Always include verification and acceptance for each phase.
- Prefer environment-agnostic instructions; call out provider-specific steps where needed.
- Update CHECKLIST.yaml on every material change to status.
