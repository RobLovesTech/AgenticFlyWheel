Agent Prompt Authoring Guide (Generate Late in Handoff)

Purpose
- Produce a zero‑context, execution‑ready AGENT_PROMPT.txt that synthesizes the entire AIP into a single, precise instruction set.

Sequence (must follow)
1) Read `CHECKLIST.yaml` first and note `packet_level`, `requirements_mode`, `delivery_surfaces`, `enabled_modules`, and `omitted_modules`. Ensure the always-present docs are complete: README.md, REVIEWS.md, RISKS.md, CONTEXT.md, CHECKLIST.yaml. Then ensure every enabled module doc is complete.
2) Read README.md → extract: Executive Summary, Requirements Mode, Goals, Non‑Goals, Signals & Flags (Summary), Acceptance, Rollout, Operating Requirements.
3) Read REVIEWS.md → extract the Collaboration Summary plus only the Accepted Decisions, Open Risks, and Final Verdict. Ignore advisory notes that were not accepted.
4) If `contracts` is enabled, read CONTRACTS.md → extract: signal formulas, thresholds/buckets, events, fallbacks, Acceptance Rules.
5) If `backend_implementation` is enabled, read BACKEND_IMPLEMENTATION.md → extract: file paths + functions to edit; flags; pseudocode.
6) If `orchestration_and_ui` is enabled, read ORCHESTRATION_AND_UI.md → extract: FE files + copy/threshold changes.
7) If `runbook` is enabled, read RUNBOOK.md → extract: flags/defaults; commands; flip/rollback; queries.
8) If `observability` is enabled, read OBSERVABILITY.md → extract: metrics names/labels; dashboards and validation panels.
9) If `data_model` is enabled, read DATA_MODEL.sql → extract schema/storage expectations and any DDL or retention notes.
10) If `operating_model` is enabled, read OPERATING_MODEL.md → extract future-state workflow, owners, handoffs, and exception handling.
11) If `gtm_and_launch` is enabled, read GTM_AND_LAUNCH.md → extract launch audience, sequencing, messaging constraints, assets, success metrics, and stop/go criteria.
12) If `client_rollout` is enabled, read CLIENT_ROLLOUT.md → extract cohorts, transition rules, customer communications, and rollback/cutover criteria.
13) If `enablement_and_support` is enabled, read ENABLEMENT_AND_SUPPORT.md → extract training, support ownership, coverage, escalation, and FAQ expectations.
14) If `governance_and_approvals` is enabled, read GOVERNANCE_AND_APPROVALS.md → extract sign-offs, policy/compliance gates, required evidence, and readiness checkpoints.
15) Read CHECKLIST.yaml → list phases/tasks in order (summarize as step‑by‑step tasks).
16) Draft AGENT_PROMPT.txt using the structure below; include exact paths, flags, acceptance, and readiness evidence. Keep concise and precise.

AGENT_PROMPT Structure (must include)
- Title line: “You are the implementation agent for: <TITLE> (<FEATURE_SLUG>)”
- Context directory path
- Intake steps (read docs list)
- Primary goals (bullets)
- Non‑Goals (bullets)
- Review Inputs (Accepted Decisions from REVIEWS.md only)
- Collaboration Inputs (confirmed decisions and accepted assumptions from Collaboration Summary)
- Operating Readiness Inputs (launch, rollout, enablement, support, approval, and client-transition decisions when applicable)
- Signals & Flags (summary of formulas, flags, readiness gates)
- Runtime Flags (from RUNBOOK when enabled, otherwise from CHECKLIST/CONTEXT if packet-level defaults exist)
- Touch points (Backend files, Frontend files, Docs, and non-code artifact surfaces) — exact paths
- Step-by-step tasks (from CHECKLIST.yaml) — summarize concisely
- Verify & Accept (Acceptance from README + Acceptance Rules from CONTRACTS when enabled + required readiness evidence when applicable)
- Validation & Observability (metrics/dashboards from OBSERVABILITY when enabled, plus launch/adoption evidence when applicable)
- Implementation Audit Gate (run IMPLEMENTATION_AUDIT after implementation/docs/verification, fix findings, re-verify, then close)
- Ground rules (minimize scope; update docs; compliance; no unrelated changes)

Rubric (self‑check before finalizing)
- Does it list concrete file paths and the intent for each?
- Are all flags and defaults included?
- Are readiness gates, approvals, and non-technical requirements included when the packet needs them?
- Are formulas/thresholds summarized correctly?
- Are tasks in execution order (phases) and concise?
- Are acceptance conditions explicit and verifiable?
- Are validation commands/queries mentioned?
- Does the prompt reference only the module docs that the packet actually enables?
- Does it state that IMPLEMENTATION_AUDIT is required before packet closure and that findings block completion until fixed or explicitly dispositioned?
- Does it preserve the Collaboration Summary so implementation does not depend on prior chat or unconfirmed assumptions?
- Is it free of implementation detail that belongs in packet docs (keep it an instruction, not a design doc)?

Anti‑patterns
- Do not hand‑wave: “update code accordingly.” Specify files/sections.
- Do not assume prior chat context.
- Do not duplicate entire packet content; synthesize what’s necessary to execute.
- Do not treat raw runtime logs or unaccepted review notes as canonical.
- Do not omit flags, acceptance, or file paths.

Handoff
- Save AGENT_PROMPT.txt at the root of the packet.
- Update CHECKLIST to mark the task complete.
- Do not mark packet closure complete until the implementation audit, remediation, and targeted re-verification tasks are complete.
