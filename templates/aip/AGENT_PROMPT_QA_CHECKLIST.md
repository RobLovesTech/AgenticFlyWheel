Agent Prompt QA Checklist

Use this checklist before finalizing AGENT_PROMPT.txt. The prompt must be zero‑context and execution‑ready.

Structure & Context
- [ ] Title contains AIP title and feature slug
- [ ] Context directory path is included
- [ ] Intake steps instruct reading CHECKLIST first, then the always-present packet docs plus only the enabled module docs

Goals & Non‑Goals
- [ ] Primary goals listed as bullets
- [ ] Non‑Goals listed to prevent scope creep
- [ ] Collaboration Summary is reflected as confirmed user intent and accepted assumptions
- [ ] Review Inputs use only the Accepted Decisions section of REVIEWS.md

Signals & Flags
- [ ] Summarizes core signals (formulas/algorithms) in one place
- [ ] Runtime flags listed with defaults (from RUNBOOK)
- [ ] Readiness gates, approvals, or operating constraints are included when the packet is `operating` or `mixed`

Touch Points (Files)
- [ ] Backend file paths explicitly listed (with purpose)
- [ ] Frontend file paths explicitly listed (with purpose)
- [ ] Docs paths for global corrections listed (with purpose)
- [ ] Non-code artifact paths or packet surfaces are listed when launch, rollout, enablement, support, or approvals are in scope

Tasks (Step‑by‑Step)
- [ ] Derived from CHECKLIST.yaml phases in execution order
- [ ] Concise and actionable (edit file X, do Y)

Verification & Acceptance
- [ ] Acceptance from README “Acceptance” is included
- [ ] Acceptance Rules from CONTRACTS are included or referenced when the `contracts` module is enabled
- [ ] Validation & Observability panels/metrics named when the `observability` module is enabled
- [ ] Required readiness evidence is included when launch, client rollout, enablement, support, or approvals are in scope
- [ ] Required IMPLEMENTATION_AUDIT gate is included before packet closure
- [ ] Audit findings are described as blockers until fixed or explicitly dispositioned with rationale
- [ ] Targeted re-verification after audit remediation is required

Guardrails & Constraints
- [ ] Privacy/PII constraints restated (e.g., redaction, no names)
- [ ] Back‑compat notes (e.g., no new event names) if applicable
- [ ] No DB/schema claims assume `DATA_MODEL.sql` exists unless the `data_model` module is enabled
- [ ] Do not omit packet-defined GTM, client-transition, enablement, support, or approval constraints

Anti‑patterns to avoid
- [ ] No vague instructions like “update code accordingly”
- [ ] Do not assume chat history
- [ ] Do not treat raw runtime logs or unaccepted review notes as canonical
- [ ] Do not tell the implementation agent to read omitted module docs
- [ ] Do not omit flags, acceptance, or file paths
