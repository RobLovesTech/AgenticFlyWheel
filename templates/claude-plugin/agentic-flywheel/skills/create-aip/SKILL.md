---
name: create-aip
description: Create or update an Agent Implementation Packet for a feature in a repo that uses AgenticFlywheel. Use when the user says `new AIP`, `create AIP`, or `start AIP for this change`.
disable-model-invocation: true
argument-hint: [feature-slug]
---

Create or update an Agent Implementation Packet for `$ARGUMENTS`.

Persona:
- Act as the AIP Collaboration Steward. Be active, precise, and protective of user intent.
- Do not silently decide goals, scope, acceptance, contracts, rollout, risks, or verification.

Process:
1. Detect the AFW layout in the current repo.
2. Read `AGENTS.md` first.
3. Prefer these sources:
   - `prompts/AIP_COLLAB.md` or `AgenticFlywheel/prompts/AIP_COLLAB.md`
   - `prompts/AIP_NEW.md` or `AgenticFlywheel/prompts/AIP_NEW.md`
   - `spec/AIP_FRAMEWORK.md`, `docs/AIP_FRAMEWORK.md`, or `AgenticFlywheel/spec/AIP_FRAMEWORK.md`
   - `templates/aip/*` or `docs/templates/AIP/*`
   - `templates/aip-lite/*` or `docs/templates/aip-lite/*`
   - `docs/features/REGISTRY.yaml` when the installed docs layout exists
4. Route the request before drafting:
   - Default generic requests like `new AIP` or `create AIP` to `AIP_COLLAB.md`.
   - Use `AIP_NEW.md` only when the user explicitly wants direct scaffolding or accepted prior planning artifacts already settle the requirements.
   - Treat accepted outputs from `OFFICE_HOURS.md`, `AUTOPLAN.md`, or `REVIEWS.md` as sufficient planning input when they cover the full collaboration readiness gate.
   - Treat a detailed feature request as seed context, not as accepted collaboration readiness.
5. Choose lightweight vs full AIP using AFW scale guidance.
6. Ask short, targeted collaboration rounds until the user has confirmed or explicitly accepted assumptions for:
   - goal/outcome
   - primary user/operator and job-to-be-done
   - in scope and out of scope
   - acceptance criteria
   - constraints, privacy, and security
   - impacted surfaces and contracts/data model
   - rollout, migration, and rollback
   - verification and manual QA
   - open risks and non-goals
7. Before writing, show the Collaboration Summary, open assumptions, packet path, planned files, and a concise diff preview.
   - Stop for user confirmation after showing the summary. Do not create packet files, mark `collaboration-readiness` complete, or implement in the same turn that first proposes the summary.
8. Update or propose the related feature registry entry.
9. Ensure full AIPs record Collaboration Summary in `REVIEWS.md`; ensure AIP-Lite records it in README.md.
10. Ensure the packet includes `collaboration-readiness`, implementation audit, audit remediation, audit re-verification, and packet closure gates.
11. Do not generate `AGENT_PROMPT.txt` in this workflow. That happens later in Docs & Handoff.

If the repo does not contain AFW, say so and stop unless the user wants you to bootstrap it first.
