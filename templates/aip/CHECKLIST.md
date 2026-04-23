Status: pending

Phases
- Design & Contracts — finalize contracts and plan
  - [ ] Confirm user-approved collaboration readiness and record Collaboration Summary
    - Evidence: user-confirmed summary, accepted prior planning artifacts, or explicit direct/template-only scaffold exception; inferred assumptions alone are not enough.
  - [ ] Capture discovery/review outputs in REVIEWS.md
- Backend Implementation — implement + tests
- Frontend Implementation — implement + tests
- Docs — global docs corrections/updates
- Observability & Rollout — metrics + runbook
- Docs & Handoff — finalize context, audit, remediation, and registry
  - [ ] Run verification commands (tests/build/lint) for impacted components
  - [ ] Sync REVIEWS.md accepted decisions, open risks, and final verdict
  - [ ] Update CONTEXT.md with final behavior
  - [ ] Add or update Feature Registry entry
  - [ ] Run Agent Prompt QA Checklist before generating or refreshing prompt artifacts
  - [ ] Generate or refresh AGENT_PROMPT.txt from current packet docs
  - [ ] Generate or refresh IMPLEMENTATION_AUDIT_PROMPT.txt from current packet docs
  - [ ] Run packet-local IMPLEMENTATION_AUDIT_PROMPT.txt and record verdict in REVIEWS.md
  - [ ] Fix or explicitly disposition every implementation audit finding
  - [ ] Re-run targeted verification for audit findings and update evidence
  - [ ] Confirm audit passed, findings are resolved, and packet may be marked completed

Acceptance
- List final criteria here
