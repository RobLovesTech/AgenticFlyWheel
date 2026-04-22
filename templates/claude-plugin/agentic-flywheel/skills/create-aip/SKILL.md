---
name: create-aip
description: Create or update an Agent Implementation Packet for a feature in a repo that uses AgenticFlywheel. Use when the user says `new AIP`, `create AIP`, or `start AIP for this change`.
disable-model-invocation: true
argument-hint: [feature-slug]
---

Create or update an Agent Implementation Packet for `$ARGUMENTS`.

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
4. Choose lightweight vs full AIP using AFW scale guidance.
5. Ask only the minimum questions needed to define goals, scope, contracts, risks, and verification commands.
6. Before writing, show the packet path, planned files, and a concise diff preview.
7. Update or propose the related feature registry entry.
8. Do not generate `AGENT_PROMPT.txt` in this workflow. That happens last.

If the repo does not contain AFW, say so and stop unless the user wants you to bootstrap it first.
