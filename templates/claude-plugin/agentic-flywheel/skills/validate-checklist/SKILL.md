---
name: validate-checklist
description: Validate an AgenticFlywheel `CHECKLIST.yaml` for collaboration readiness, required phases, status coherence, verification coverage, implementation audit gates, and registry updates.
disable-model-invocation: true
argument-hint: [path-or-feature-slug]
---

Validate the target AFW `CHECKLIST.yaml`.

Process:
1. Resolve `$ARGUMENTS` to either:
   - a direct checklist path, or
   - `docs/Agent Implementation Packets/<feature-slug>/CHECKLIST.yaml`
2. Read `AGENTS.md` first.
3. Prefer these sources:
   - `prompts/CHECKLIST_VALIDATOR.md` or `AgenticFlywheel/prompts/CHECKLIST_VALIDATOR.md`
   - `templates/aip/CHECKLIST.schema.json`, `docs/templates/AIP/CHECKLIST.schema.json`, or `AgenticFlywheel/templates/aip/CHECKLIST.schema.json`
   - the target `CHECKLIST.yaml`
4. Check:
   - required top-level fields
   - `packet_level`, `enabled_modules`, and `omitted_modules` when present, plus legacy fallback behavior when they are absent
   - collaboration readiness task and Collaboration Summary write-back
   - final `Docs & Handoff` phase
   - verification commands and acceptance
   - implementation audit, remediation, re-verification, and packet closure tasks
   - status coherence
   - registry update coverage
   - top-level `in_progress` or `completed` packets do not omit completed collaboration readiness unless explicitly legacy with rationale
5. Return pass or fail with findings and a minimal proposed patch.

If the target file cannot be found, explain the missing path and stop.
