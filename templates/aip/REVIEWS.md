Discovery Reframe
- Summarize the reframed problem statement and user/job-to-be-done.

Collaboration Summary
- This section is the structured collaboration receipt that authorizes packet creation or update.
- Required before packet scaffolding or update.
- `Confirmation Basis`: `user-confirmed summary` | `accepted prior planning artifacts` | `direct/template-only scaffold exception`
- `Confirmed By`:
- `Confirmed At`:
- `Source Artifacts / Exception Rationale`:
- `Confirmed Decisions`:
  - Goal / desired outcome
  - Persona scope decisions
  - In-scope / out-of-scope boundaries
  - Success criteria / acceptance
  - Contracts / data model
  - Rollout / migration / rollback
  - Verification expectations
- `Accepted Assumptions`:
- `Open Questions / Deferred Follow-Ups`:
- `Priority Tier Assignments` (when applicable):
- `Reference Data Completeness` (when applicable):
- `Cross-Cutting Behavior Decisions` (when applicable):
- `Interaction Surface Decisions` (when applicable):
- `Operating Readiness Decisions` (when applicable):
- Do not let implementation agents treat unconfirmed guesses as packet truth.
- Agent-inferred assumptions are proposed assumptions until the user confirms them or approves a direct/template-only scaffold exception.

Product Review
- Capture product-level findings, scope expansions, and tradeoffs.

Engineering Review
- Capture architecture, data flow, failure modes, and test strategy decisions.

Design Review
- Capture user-facing UX, state, copy, accessibility, and interaction decisions.

Operations Review
- Capture future-state workflow, operating model, ownership, support, and launch-readiness findings.

Change Management Review
- Capture GTM, client rollout, enablement, communications, approvals, and adoption-risk findings.

DevEx Review
- Capture developer experience findings for APIs, CLIs, SDKs, docs, or internal tooling.

Compliance Review
- Optional. Capture policy, legal, privacy, security, or governance review input when it materially affects the packet.

Outside Voice
- Optional. Record any secondary-model or external review input.
- Mark clearly whether it was accepted, rejected, or left advisory.

Accepted Decisions
- List only the conclusions that are approved to drive implementation.

Implementation Audit
- Required after implementation, verification, docs sync, and prompt-artifact refresh, but before packet closure.
- Record the `IMPLEMENTATION_AUDIT.md` verdict here: `pass`, `pass with concerns`, or `fail`.
- Summarize blocking findings, accepted remediation decisions, verification evidence, and any explicitly non-blocking concerns.
- Packet closure is not allowed until actionable findings are fixed or explicitly marked not applicable with rationale and targeted re-verification is recorded.

Open Risks
- List unresolved risks, assumptions, and follow-up questions.

Final Verdict
- State whether the packet is ready to implement, blocked, needs more review, or passed implementation audit and may close.
