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
  - All impacted personas enumerated with per-persona scope confirmation (in-scope / deferred / out-of-scope for this AIP)
  - In scope and out of scope
  - For large features (3+ capability areas): priority tier assignment per capability area (P0 must-have / P1 fast-follow / P2 future)
  - Success criteria and acceptance signals
  - Constraints, privacy/security/compliance requirements
  - Impacted surfaces: backend, frontend, data, docs, integrations, operations
  - Contracts/data model implications or explicit "none"
  - Reference/taxonomy data completeness confirmed (enum values, seed data, mapping tables)
  - Cross-cutting behaviors: entity lifecycle states and transitions, retroactivity/grandfathering rules, evaluation semantics (short-circuit vs. exhaustive), system defaults, audit/logging scope beyond core feature
  - Rollout, flags, migration/backfill, and rollback expectations
  - Verification commands and manual QA expectations
  - Known risks, non-goals, and unresolved assumptions
- AIP packets must record a Collaboration Summary:
  - Full AIP: `REVIEWS.md` → `Collaboration Summary`
  - AIP-Lite: README.md → `Collaboration Summary`
- The Collaboration Summary is an evidence-bearing collaboration receipt, not a loose narrative.
- Required receipt fields for new or updated packets:
  - `Confirmation Basis`: `user-confirmed summary`, `accepted prior planning artifacts`, or `direct/template-only scaffold exception`
  - `Confirmed By`
  - `Confirmed At`
  - `Confirmed Decisions`
  - `Accepted Assumptions`
  - `Open Questions / Deferred Follow-Ups`
  - `Persona Scope Decisions`
  - `Priority Tier Assignments` when applicable
  - `Reference Data Completeness` when applicable
  - `Cross-Cutting Behavior Decisions` when applicable
  - `Interaction Surface Decisions` when applicable
- If the packet used accepted prior planning artifacts or a direct/template-only scaffold exception, record the exact source artifacts or exception rationale in the receipt.
- CHECKLIST.yaml must include a `collaboration-readiness` task before implementation tasks.
- `collaboration-readiness` may be marked `completed` only when the packet records a user-confirmed Collaboration Summary or a user-requested direct/template-only scaffold exception. Agent-inferred assumptions are proposed assumptions, not accepted assumptions.

Minimum Required Sections (Quality Bar)
Every AIP MUST include the following content. Use the templates in `docs/templates/AIP/`:
- Core full-AIP docs (always present)
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
  - CHECKLIST.yaml / CHECKLIST.md
    - Canonical phase/task ledger plus human-readable mirror
    - Packet manifest fields: `packet_level`, `enabled_modules`, `omitted_modules`
  - CONTEXT.md
    - Decisions, constraints, environment defaults, acceptance goals
  - RISKS.md
    - Top risks and mitigations; test coverage calls; back‑compat considerations
  - AGENT_PROMPT.txt
    - Restartable implementation handoff
  - IMPLEMENTATION_AUDIT_PROMPT.txt
    - Packet-specific audit wrapper artifact for full AIPs
- Optional capability modules (enable only when relevant)
  - CONTRACTS.md
    - Enable when API, event, validation, integration, compatibility, or docs-contract changes are in scope
    - Signals & Semantics (exact formulas/algorithms)
    - Buckets/Thresholds & Copy expectations (if any UI surfaces a score)
    - Event & API contracts (fields, optional/fallbacks)
    - Docs Contract (what global docs say after this AIP lands)
  - DATA_MODEL.sql
    - Enable when schema, persistence, retention, backfill, or storage semantics change
    - DDL diffs (if needed) or explicit “No schema changes” note
  - BACKEND_IMPLEMENTATION.md
    - Enable when backend/services/jobs/workers are in scope
    - File‑by‑file touchpoints (paths + functions/methods)
    - Flags, feature gates, and pseudocode for non‑trivial logic
    - Data persistence semantics (exact columns and values)
  - ORCHESTRATION_AND_UI.md
    - Enable when UI, orchestration, or user/operator journeys are in scope
    - Frontend file‑by‑file tasks (components, utils, constants)
    - Copy/threshold updates and fallbacks
  - OBSERVABILITY.md
    - Enable when metrics/logging/alerts/tracing/operational validation materially change
    - New/updated metrics (names, labels, semantics)
    - Dashboards and validation panels; flicker/stability definitions when applicable
  - RUNBOOK.md
    - Enable when rollout, flags, migrations, rollback, or manual operator actions matter
    - Flags and defaults; local validation steps; flip/rollback; example queries

Standard Packet Contents
- README.md: Objective, scope, constraints, outcomes
- REVIEWS.md: Review gauntlet output and accepted decisions that implementation agents may rely on
- CHECKLIST.yaml: Canonical phases/tasks, acceptance, and packet manifest (`packet_level`, `enabled_modules`, `omitted_modules`)
- CHECKLIST.md: Human-friendly checklist and notes
- AGENT_PROMPT.txt: Restartable instructions for agents
- IMPLEMENTATION_AUDIT_PROMPT.txt: Packet-specific audit wrapper artifact for full AIPs
- CONTEXT.md: Decisions, constraints, environment defaults, acceptance goals
- RISKS.md: Risks and mitigations
- Optional capability modules: CONTRACTS.md, DATA_MODEL.sql, BACKEND_IMPLEMENTATION.md, ORCHESTRATION_AND_UI.md, OBSERVABILITY.md, RUNBOOK.md

Capability-Driven Module Manifest
- Record packet scope directly in `CHECKLIST.yaml`; do not create a second manifest file.
- New full AIPs should write:
  - `packet_level: full`
  - `enabled_modules: [contracts, data_model, backend_implementation, orchestration_and_ui, observability, runbook]` with only the relevant modules present
  - `omitted_modules:` entries with `module` + `reason` for intentionally skipped modules
- New AIP-Lite packets may stay on the existing lightweight surface without adding the module manifest immediately.
- Existing full AIPs that predate the manifest remain valid; treat them as legacy full packets and infer enabled modules from the packet docs and checklist until they are refreshed.

Artifact Matrix
- Full AIP required tracked artifacts:
  - README.md
  - REVIEWS.md
  - CHECKLIST.yaml
  - CHECKLIST.md
  - CONTEXT.md
  - RISKS.md
  - AGENT_PROMPT.txt
  - IMPLEMENTATION_AUDIT_PROMPT.txt
- Full AIP optional capability modules:
  - CONTRACTS.md
  - DATA_MODEL.sql
  - BACKEND_IMPLEMENTATION.md
  - ORCHESTRATION_AND_UI.md
  - OBSERVABILITY.md
  - RUNBOOK.md
- AIP-Lite required tracked artifacts:
  - README.md
  - CHECKLIST.yaml
- AIP-Lite optional artifacts:
  - AGENT_PROMPT.txt when the repo wants a zero-context handoff artifact for the change
- AIP-Lite does not require `REVIEWS.md` or a packet-local `IMPLEMENTATION_AUDIT_PROMPT.txt` unless a repo explicitly chooses to add them.
- Full AIP packet creation must include an initial `AGENT_PROMPT.txt` and `IMPLEMENTATION_AUDIT_PROMPT.txt` in the approval bundle.
- Docs & Handoff must generate or refresh prompt artifacts again after packet docs are stable and before the required implementation audit runs.

Documentation Tasks (required)
- Every AIP MUST include a final phase in CHECKLIST.yaml named "Docs & Handoff" that:
  - Verifies the change is shippable by running the repo’s defined verification commands (tests/build/lint as applicable) for every impacted component before the AIP can be marked `completed`.
  - Updates all core packet docs plus any enabled capability modules to reflect reality.
  - Integrates links into relevant global docs (e.g., docs/ai/INDEX.md) if applicable.
  - Updates core specifications and AI-facing guides (e.g., docs/ai/**, other specs) to reflect the new or changed behavior.
  - Records new/changed env vars in the appropriate repo docs.
  - Captures operator notes (how to verify/rollback) and any UI screenshots if relevant.
  - Confirms parity notes (local == prod) are accurate.
  - Runs the Agent Prompt QA Checklist (docs/templates/AIP/AGENT_PROMPT_QA_CHECKLIST.md) before finalizing prompt artifacts.
  - Generates or refreshes `AGENT_PROMPT.txt` and, for full AIPs, `IMPLEMENTATION_AUDIT_PROMPT.txt` from the current packet docs before the required implementation audit.
  - Runs the required implementation audit (`AgenticFlywheel/prompts/IMPLEMENTATION_AUDIT.md`) after implementation, verification, docs sync, and prompt-artifact refresh, but before packet closure.
  - Records the audit verdict and accepted findings in packet truth (`REVIEWS.md` for full AIPs, README.md for AIP-Lite).
  - Creates remediation checklist tasks for every actionable audit finding, fixes or explicitly dispositions each finding, and re-runs targeted verification before closure.
  - Refreshes prompt artifacts if audit findings change packet docs, task order, acceptance criteria, or handoff instructions.
  - Includes a final packet-closure task that confirms the audit passed, findings are resolved, and the packet may be marked `completed`.

Execution Review Prompt Scope
- Mandatory closure chain for all AIPs:
  - verification commands
  - implementation audit
  - audit remediation
  - audit re-verification
  - packet closure
- Recommended execution-review prompts:
  - `PRELANDING_REVIEW.md`
  - `QA.md`
  - `SHIP.md`
- These review prompts are reusable gauntlet surfaces, but they are not universal checklist requirements unless the repo explicitly adds packet tasks for them.

Authoring Checklist (copy into CHECKLIST.md)
- [ ] README has Exec Summary, Goals/Non‑Goals, Signals/Flags, Scope, Outcomes, Success, Rollout, Acceptance
- [ ] Collaboration Summary captures confirmed decisions, accepted assumptions, open questions, and user confirmation
- [ ] REVIEWS documents the review gauntlet, accepted decisions, open risks, and final verdict
- [ ] REVIEWS documents the implementation audit verdict, accepted findings, remediation evidence, and closure decision
- [ ] CHECKLIST.yaml records packet level plus enabled/omitted modules when using the capability-driven full AIP model
- [ ] CONTRACTS includes formulas, buckets/thresholds, event fields, and fallbacks when the `contracts` module is enabled
- [ ] BACKEND_IMPLEMENTATION lists every file/function to touch and pseudocode for tricky bits when the `backend_implementation` module is enabled
- [ ] ORCHESTRATION_AND_UI lists frontend files and copy changes when the `orchestration_and_ui` module is enabled
- [ ] OBSERVABILITY has metric names/labels and validation dashboard calls when the `observability` module is enabled
- [ ] RUNBOOK includes flags, commands, queries, and rollback when the `runbook` module is enabled
- [ ] DATA_MODEL.sql documents schema/storage expectations when the `data_model` module is enabled
- [ ] RISKS calls out flicker/instability, drift, and back‑compat
- [ ] AGENT_PROMPT is zero‑context and explicit (file paths, flags, acceptance)
- [ ] Full AIP prompt artifacts (`AGENT_PROMPT.txt` and `IMPLEMENTATION_AUDIT_PROMPT.txt`) are present, current, and referenced by the checklist

Checklist YAML Schema (informal)
- version: integer
- feature: string (slug)
- packet_level: lite | full (optional for legacy packets; recommended for new full AIPs)
- enabled_modules: [contracts | data_model | backend_implementation | orchestration_and_ui | observability | runbook]
- omitted_modules: [{ module: <same enum>, reason: string }]
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
- Required prompt-artifact tasks for full AIPs: `agent-prompt`, `audit-prompt`
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
4) Record `packet_level`, `enabled_modules`, and `omitted_modules` in `CHECKLIST.yaml`, then fill in README.md, REVIEWS.md or README Collaboration Summary, CONTEXT.md, RISKS.md, and only the enabled capability-module docs from confirmed decisions and accepted assumptions.
5) During planning, explicitly check for reuse opportunities (shared modules/components/design system) to avoid duplicating patterns. If you identify a new reusable pattern, implement it in the repo’s shared layer/package.
6) Populate CHECKLIST.yaml with phases/tasks and keep statuses current.
7) For full AIPs, include initial `AGENT_PROMPT.txt` and `IMPLEMENTATION_AUDIT_PROMPT.txt` in the packet-creation approval bundle once the packet docs are drafted.
8) During Docs & Handoff, generate or refresh prompt artifacts from the current packet docs using `AgenticFlywheel/prompts/AGENT_PROMPT_GENERATOR.md` together with the Authoring Guide (`docs/templates/AIP/AGENT_PROMPT_AUTHORING_GUIDE.md`). Run the Agent Prompt QA Checklist (`docs/templates/AIP/AGENT_PROMPT_QA_CHECKLIST.md`) before finalizing.
9) Run `AgenticFlywheel/prompts/IMPLEMENTATION_AUDIT.md`, fix or explicitly disposition all findings, refresh prompt artifacts if audit-driven packet changes affect them, re-run targeted verification, then complete the packet-closure task and flip the top-level `status` to `completed`.

Zero‑Context Agent Prompt Guidance
- The AGENT_PROMPT.txt MUST:
  - Enumerate concrete file paths to edit and their purpose
  - List flags and defaults
  - Include step‑by‑step tasks and acceptance criteria
 - Use only accepted conclusions from REVIEWS.md; runtime logs under `.agentic-flywheel/state/` are advisory and never override packet docs
  - Instruct the agent to run the implementation audit gate before packet closure and to treat actionable audit findings as completion blockers
  - Reference packet docs by path; avoid relying on chat history
 - Be created after the core packet docs plus every enabled capability-module doc are complete

Validation
- CHECKLIST schema: docs/templates/AIP/CHECKLIST.schema.json
- `CHECKLIST_VALIDATOR.md` is required before approving a newly scaffolded packet and again before packet closure.
- Schema or local-script validation is strongly recommended when tooling is available.
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
