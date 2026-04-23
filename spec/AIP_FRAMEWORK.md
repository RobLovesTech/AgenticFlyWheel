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
- Active collaboration: AIP packets are created through user-agent collaboration, not silent template filling. The agent must lock intent with the user before scaffolding packet truth.
- Re-issuable prompt: AGENT_PROMPT.txt allows new agent sessions to bootstrap without relying on prior chat history.
- Self-maintaining: Documentation is updated as part of the implementation process, creating flywheel momentum.
- Two-layer operation: repo-tracked AIPs/docs/registry are the control plane; local runtime artifacts under `.agentic-flywheel/state/` are an advisory execution layer.
- Parity: Packets should capture any environment parity needs (e.g., local Postgres == prod Databricks).
- Privacy & security: Document constraints explicitly (e.g., FERPA/COPPA, PII redaction, retention).
- Complete features: AIPs drive implementation of complete, production-ready features, not prototypes.

Collaboration by Default
- AFW treats active collaboration as the default intake behavior for every explicit `new AIP`, `create AIP`, or packet-sized work request.
- The agent should not need the user to say `AIP_COLLAB`; exact command phrases are shortcuts, not prerequisites.
- Auto-trigger collaboration when the request involves any of the following:
  - a new feature, initiative, or implementation packet
  - a non-trivial feature change that likely needs an AIP or AIP update
  - an existing AIP, contract, rollout, acceptance gate, registry entry, or packet doc
  - work touching APIs, data models, migrations, flags, observability, rollout, or cross-cutting behavior
  - requests that clearly need planning, scoping, or accepted decisions before safe implementation
- Do not force collaboration for clearly narrow no-AIP work such as:
  - typos, tiny copy edits, docs-only fixes, or low-risk single-purpose bug fixes
  - small refactors with no contract, rollout, or acceptance impact
- Default intake flow for packet-sized work:
  1) inspect docs, Feature Registry, and relevant AIPs first
  2) restate the goal, likely AIP level, and likely packet path
  3) ask only the remaining high-impact questions needed to lock decisions
  4) summarize confirmed decisions, accepted assumptions, and open questions
  5) get user confirmation before scaffolding or updating packet docs
- A detailed feature request is still only seed context until the user confirms the Collaboration Summary. Specificity can shorten the collaboration round, but it cannot replace the confirmation step.
- Agents must not create or update packet files, mark `collaboration-readiness` complete, or begin implementation in the same turn that first infers the Collaboration Summary for an explicit `new AIP` / `create AIP` / `start AIP` request.
- Escalate to a fuller planning gauntlet such as `OFFICE_HOURS -> AUTOPLAN -> AIP_COLLAB` when risk is high, the scope is unresolved, or tradeoffs need deeper review.

Collaboration Readiness Gate
- A new or updated AIP is not ready to scaffold until these decisions are user-confirmed or explicitly accepted as assumptions:
  - Goal/problem and desired outcome
  - Primary user/operator and job-to-be-done
  - In scope and out of scope
  - Success criteria and acceptance signals
  - Constraints, privacy/security/compliance requirements
  - Impacted surfaces: backend, frontend, data, docs, integrations, operations
  - Contracts/data model implications or explicit "none"
  - Rollout, flags, migration/backfill, and rollback expectations
  - Verification commands and manual QA expectations
  - Known risks, non-goals, and unresolved assumptions
- AIP packets must record a Collaboration Summary:
  - Full AIP: `REVIEWS.md` → `Collaboration Summary`
  - AIP-Lite: README.md → `Collaboration Summary`
- CHECKLIST.yaml must include a `collaboration-readiness` task before implementation tasks.
- `collaboration-readiness` may be marked `completed` only when the packet records a user-confirmed Collaboration Summary or a user-requested direct/template-only scaffold exception. Agent-inferred assumptions are proposed assumptions, not accepted assumptions.

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
  - Collaboration Summary
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
- [ ] Collaboration Summary captures confirmed decisions, accepted assumptions, open questions, and user confirmation
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
- Required planning gate task for all AIPs: `collaboration-readiness`
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
1) Start with active collaboration (`AIP_COLLAB.md`) for every explicit new-AIP request or packet-sized work request.
2) Inspect registry/docs/AIPs, ask targeted questions, summarize confirmed decisions, and get user confirmation before writing packet docs.
3) Scaffold a new AIP or update the existing packet from templates only after the collaboration readiness gate is satisfied.
4) Fill in README.md, REVIEWS.md or README Collaboration Summary, CONTEXT.md, DATA_MODEL.sql, and CHECKLIST.yaml from confirmed decisions and accepted assumptions.
5) During planning, explicitly check for reuse opportunities (shared modules/components/design system) to avoid duplicating patterns. If you identify a new reusable pattern, implement it in the repo’s shared layer/package.
6) Populate CHECKLIST.yaml with phases/tasks and keep statuses current.
7) Generate AGENT_PROMPT.txt late in Docs & Handoff using the Agent Prompt Generator prompt (`AgenticFlywheel/prompts/AGENT_PROMPT_GENERATOR.md`) together with the Authoring Guide (`docs/templates/AIP/AGENT_PROMPT_AUTHORING_GUIDE.md`). Run the Agent Prompt QA Checklist (`docs/templates/AIP/AGENT_PROMPT_QA_CHECKLIST.md`) before finalizing.
8) Run `AgenticFlywheel/prompts/IMPLEMENTATION_AUDIT.md`, fix or explicitly disposition all findings, refresh AGENT_PROMPT.txt if audit-driven packet changes affect it, re-run targeted verification, then complete the packet-closure task and flip the top-level `status` to `completed`.

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
