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
- Implementation audit findings are not authoritative until promoted into packet docs, but once accepted and promoted they are hard closure blockers until fixed or explicitly dispositioned with rationale.

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

Packet Manifest Contract
- Full AIPs may use a capability-driven packet manifest recorded directly in `CHECKLIST.yaml`.
- Recommended manifest fields for new full AIPs:
  - `packet_level: full`
  - `enabled_modules: [contracts, data_model, backend_implementation, orchestration_and_ui, observability, runbook]` with only relevant modules present
  - `omitted_modules:` entries with `module` plus `reason`
- The manifest is canonical packet truth. Prompts should read it before assuming which docs exist.
- Legacy full AIPs without these fields remain valid. Prompts and validators should treat them as older full packets and infer module coverage from the packet docs and checklist references instead of failing on the missing manifest.
- AIP-Lite stays on the existing lighter surface unless a repo explicitly chooses to extend it.

Collaboration Receipt Contract
- The Collaboration Summary is the evidence-bearing collaboration receipt that authorizes packet creation or update.
- The receipt must capture:
  - `Confirmation Basis`
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
- If accepted prior planning artifacts or a direct/template-only scaffold exception satisfied readiness, record the exact source artifacts or exception rationale in the receipt.

Collaboration Intake Flow
1) For generic `new AIP`, `create AIP`, `start AIP`, or packet-sized work, route to `AIP_COLLAB.md` by default.
2) Use runtime notes, prior chat, and review logs only as advisory inputs while clarifying the request.
3) Confirm or explicitly accept assumptions for:
   - goals and desired outcome
   - primary user/operator and job-to-be-done
   - all impacted personas with per-persona scope decisions
   - in-scope and out-of-scope work
   - priority tier assignments for large features
   - success criteria and acceptance signals
   - constraints and compliance requirements
   - impacted surfaces
   - contracts and data-model implications
   - reference data completeness when relevant
   - cross-cutting behaviors when relevant
   - interaction-surface decisions when relevant
   - rollout, migration, rollback, and verification expectations
   - risks and non-goals
   - packet level plus which optional capability modules are required or intentionally omitted
4) Promote the accepted collaboration result into packet docs before scaffolding implementation truth:
   - Full AIP: `REVIEWS.md` -> `Collaboration Summary`
   - AIP-Lite: README.md -> `Collaboration Summary`
5) Record packet level and enabled/omitted modules in `CHECKLIST.yaml`, then mark or create `collaboration-readiness` before implementation tasks begin.
6) `AIP_NEW.md` may scaffold directly only when the user explicitly asks for direct/template-only scaffolding or accepted prior planning artifacts already satisfy collaboration readiness.
7) A detailed request does not satisfy collaboration readiness by itself. Agent-inferred assumptions must stay proposed until the user confirms the Collaboration Summary.
8) For explicit `new AIP` requests, do not scaffold packet files, complete `collaboration-readiness`, or start implementation in the same response that first proposes the collaboration receipt.

Prompt Artifact Flow
1) Full AIP packet creation generates an initial `AGENT_PROMPT.txt` and `IMPLEMENTATION_AUDIT_PROMPT.txt` in the same approval bundle as the packet docs.
2) Docs & Handoff later generates or refreshes prompt artifacts again from the current packet docs before the required implementation audit.
3) AIP-Lite does not require a packet-local `IMPLEMENTATION_AUDIT_PROMPT.txt`; `AGENT_PROMPT.txt` is optional unless the repo wants a zero-context handoff artifact for the change.
4) Prompt-generation and audit flows must read the packet manifest first and only require enabled module docs. Legacy full AIPs without a manifest should be handled by inferring module coverage from the packet docs already present.

Implementation Audit Flow
1) After implementation, verification, docs sync, and prompt-artifact refresh, run `IMPLEMENTATION_AUDIT.md`.
2) Append the advisory runtime entry to `.agentic-flywheel/state/reviews.jsonl` when runtime logging is enabled.
3) Promote accepted audit findings into `REVIEWS.md` for full AIPs or the `Implementation Audit` section of README.md for AIP-Lite.
4) Create remediation checklist tasks for actionable findings in `CHECKLIST.yaml` and `CHECKLIST.md`.
5) Fix or explicitly disposition findings, refresh prompt artifacts if audit-driven packet changes affect them, re-run targeted verification, then mark audit remediation, re-verification, and packet closure tasks complete.
6) Only after this flow may top-level `CHECKLIST.yaml.status` be set to `completed`.
- Acceptance and disposition authority:
  - A finding becomes a closure blocker only after it is explicitly accepted into packet truth by the user or by a follow-on prompt acting under the user's accepted workflow.
  - Hosts must not silently self-approve severity downgrades or dismiss findings without recording rationale.
  - Any non-blocking or not-applicable disposition must record the rationale, the deciding party, and the targeted verification evidence or explicit reason no additional verification is required.

Host Strategy
- Codex is the primary host in v1.
- Claude and Cursor should receive compatible, smaller overlays after the Codex path is stable.
- Host configs should route natural-language commands for planning, AIP collaboration, reviews, implementation audit, checkpointing, QA, shipping, and guard mode to the matching AFW prompt.
- Host configs must treat active collaboration as the default for new AIP requests and packet-sized work; direct scaffolding is a narrow fast path after collaboration readiness is satisfied.

Privacy and Retention
- First cut is local-only. No hosted telemetry.
- Runtime state may include implementation notes and branch names; treat it as private project state.
- Store only what improves recovery and review quality.
- Delete stale or misleading runtime artifacts when they no longer reflect current packet truth.

Non-Goals
- No browser binary, Chrome extension, or hidden home-directory dependency.
- No requirement to sync runtime state across machines.
- No hosted analytics or community telemetry in v1.
