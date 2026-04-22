---
name: generate-agent-prompt
description: Generate or update `AGENT_PROMPT.txt` from a completed AgenticFlywheel packet. Use only after the packet docs are stable.
disable-model-invocation: true
argument-hint: [feature-slug]
---

Generate `AGENT_PROMPT.txt` for `$ARGUMENTS`.

Process:
1. Resolve the packet path at `docs/Agent Implementation Packets/<feature-slug>/`.
2. Read `AGENTS.md` first.
3. Prefer these sources:
   - `prompts/AGENT_PROMPT_GENERATOR.md` or `AgenticFlywheel/prompts/AGENT_PROMPT_GENERATOR.md`
   - `templates/aip/AGENT_PROMPT_AUTHORING_GUIDE.md`, `docs/templates/AIP/AGENT_PROMPT_AUTHORING_GUIDE.md`, or the vendored template path
   - `templates/aip/AGENT_PROMPT_QA_CHECKLIST.md`, `docs/templates/AIP/AGENT_PROMPT_QA_CHECKLIST.md`, or the vendored template path
   - the packet docs, especially `CHECKLIST.yaml`
4. Confirm the packet docs are complete enough to synthesize a zero-context prompt.
5. Treat `CHECKLIST.yaml` as canonical for task order and acceptance.
6. Show the drafted prompt, or a concise diff if it already exists, before writing.
7. After writing, remind the user to mark the corresponding checklist task complete.

If the packet or required docs are missing, explain the gaps and stop.
