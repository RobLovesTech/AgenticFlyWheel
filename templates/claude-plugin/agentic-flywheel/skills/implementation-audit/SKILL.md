---
name: implementation-audit
description: Run the required AgenticFlywheel implementation audit gate before AIP packet closure.
disable-model-invocation: true
argument-hint: [path-or-feature-slug]
---

Run the required AFW implementation audit for `$ARGUMENTS`.

Process:
1. Resolve `$ARGUMENTS` to either:
   - a packet path, or
   - `docs/Agent Implementation Packets/<feature-slug>/`
2. Read `AGENTS.md` first.
3. Prefer these sources:
   - `prompts/IMPLEMENTATION_AUDIT.md` or `AgenticFlywheel/prompts/IMPLEMENTATION_AUDIT.md`
   - the target packet docs, especially `CHECKLIST.yaml`
   - the implementation diff and changed files named by the packet
   - verification evidence from `CHECKLIST.yaml` and `RUNBOOK.md`
4. Confirm all non-audit implementation, verification, docs-sync, and AGENT_PROMPT tasks are complete enough to audit.
5. Execute the audit as a consolidated panel: security, architecture, QA, frontend/UX/accessibility, database/data integrity, agentic AI workflow, product/operator risk, and DevEx.
6. Return `Verdict: pass`, `Verdict: pass with concerns`, or `Verdict: fail`.
7. Promote accepted findings into packet docs:
   - full AIP: `REVIEWS.md` -> `Implementation Audit`
   - AIP-Lite: README.md -> `Implementation Audit`
8. Add remediation tasks for actionable findings, require targeted re-verification, and block packet closure until findings are fixed or explicitly dispositioned.
9. Refresh `AGENT_PROMPT.txt` if audit-driven packet changes affect execution or handoff instructions.

If the packet cannot be found, explain the missing path and stop.
