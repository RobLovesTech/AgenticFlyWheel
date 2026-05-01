Title: {{TITLE}}

Objective
- What you're building and why (1-2 sentences).

Changes
Backend:
- List files and functions to modify.

Frontend:
- List components and UI changes.

Data:
- Database or API contract changes.

Testing
- Unit tests to add/modify.
- Integration tests to add/modify.
- How to verify it works.

Acceptance
- Checklist of conditions that must be true when complete.

Collaboration Summary
- This section is the structured collaboration receipt that authorizes packet creation or update.
- Required before packet scaffolding or update.
- `Confirmation Basis`: `user-confirmed summary` | `accepted prior planning artifacts` | `direct/template-only scaffold exception`
- `Confirmed By`:
- `Confirmed At`:
- `Source Artifacts / Exception Rationale`:
- `Confirmed Decisions`:
- `Accepted Assumptions`:
- `Open Questions / Deferred Follow-Ups`:
- `Persona Scope Decisions`:
- `Priority Tier Assignments` (when applicable):
- `Reference Data Completeness` (when applicable):
- `Cross-Cutting Behavior Decisions` (when applicable):
- `Interaction Surface Decisions` (when applicable):
- Do not let implementation agents treat unconfirmed guesses as packet truth.
- Agent-inferred assumptions are proposed assumptions until the user confirms them or approves a direct/template-only scaffold exception.

Accepted Review Inputs (Optional)
- If planning/review prompts ran first, summarize the accepted conclusions here instead of creating REVIEWS.md.

Implementation Audit
- Required after implementation, verification, and docs updates, but before packet closure.
- Record the scaled `IMPLEMENTATION_AUDIT.md` verdict here.
- List any accepted findings, fixes, targeted re-verification evidence, and explicitly non-blocking concerns.
- Packet closure is not allowed until actionable findings are fixed or explicitly marked not applicable with rationale.

Rollout
- How to deploy (flags, gradual rollout, or all-at-once).
- Rollback plan if issues arise.
