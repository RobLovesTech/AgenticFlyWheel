Discovery Reframe
- Summarize the reframed problem statement and user/job-to-be-done.

Collaboration Summary
- Required before packet scaffolding or update.
- Capture confirmed user decisions, accepted assumptions, unresolved questions, and the confirmation that allowed packet generation.
- Do not let implementation agents treat unconfirmed guesses as packet truth.

Product Review
- Capture product-level findings, scope expansions, and tradeoffs.

Engineering Review
- Capture architecture, data flow, failure modes, and test strategy decisions.

Design Review
- Capture user-facing UX, state, copy, accessibility, and interaction decisions.

DevEx Review
- Capture developer experience findings for APIs, CLIs, SDKs, docs, or internal tooling.

Outside Voice
- Optional. Record any secondary-model or external review input.
- Mark clearly whether it was accepted, rejected, or left advisory.

Accepted Decisions
- List only the conclusions that are approved to drive implementation.

Implementation Audit
- Required after implementation, verification, docs sync, and AGENT_PROMPT generation, but before packet closure.
- Record the `IMPLEMENTATION_AUDIT.md` verdict here: `pass`, `pass with concerns`, or `fail`.
- Summarize blocking findings, accepted remediation decisions, verification evidence, and any explicitly non-blocking concerns.
- Packet closure is not allowed until actionable findings are fixed or explicitly marked not applicable with rationale and targeted re-verification is recorded.

Open Risks
- List unresolved risks, assumptions, and follow-up questions.

Final Verdict
- State whether the packet is ready to implement, blocked, needs more review, or passed implementation audit and may close.
