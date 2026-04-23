Agent Prompt QA Checklist

Use this checklist before finalizing AGENT_PROMPT.txt. The prompt must be zero‑context and execution‑ready.

Structure & Context
- [ ] Title contains AIP title and feature slug
- [ ] Context directory path is included
- [ ] Intake steps instruct reading: README, REVIEWS, CONTRACTS, BACKEND_IMPLEMENTATION, ORCHESTRATION_AND_UI, OBSERVABILITY, RUNBOOK, RISKS, CONTEXT, DATA_MODEL, CHECKLIST

Goals & Non‑Goals
- [ ] Primary goals listed as bullets
- [ ] Non‑Goals listed to prevent scope creep
- [ ] Collaboration Summary is reflected as confirmed user intent and accepted assumptions
- [ ] Review Inputs use only the Accepted Decisions section of REVIEWS.md

Signals & Flags
- [ ] Summarizes core signals (formulas/algorithms) in one place
- [ ] Runtime flags listed with defaults (from RUNBOOK)

Touch Points (Files)
- [ ] Backend file paths explicitly listed (with purpose)
- [ ] Frontend file paths explicitly listed (with purpose)
- [ ] Docs paths for global corrections listed (with purpose)

Tasks (Step‑by‑Step)
- [ ] Derived from CHECKLIST.yaml phases in execution order
- [ ] Concise and actionable (edit file X, do Y)

Verification & Acceptance
- [ ] Acceptance from README “Acceptance” is included
- [ ] Acceptance Rules from CONTRACTS are included or referenced
- [ ] Validation & Observability panels/metrics named (from OBSERVABILITY)
- [ ] Required IMPLEMENTATION_AUDIT gate is included before packet closure
- [ ] Audit findings are described as blockers until fixed or explicitly dispositioned with rationale
- [ ] Targeted re-verification after audit remediation is required

Guardrails & Constraints
- [ ] Privacy/PII constraints restated (e.g., redaction, no names)
- [ ] Back‑compat notes (e.g., no new event names) if applicable
- [ ] No DB schema changes unless DATA_MODEL.sql states otherwise

Anti‑patterns to avoid
- [ ] No vague instructions like “update code accordingly”
- [ ] Do not assume chat history
- [ ] Do not treat raw runtime logs or unaccepted review notes as canonical
- [ ] Do not omit flags, acceptance, or file paths
