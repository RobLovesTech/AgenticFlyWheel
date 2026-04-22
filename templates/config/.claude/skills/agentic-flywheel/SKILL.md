---
name: agentic-flywheel
description: Use AgenticFlywheel for bootstrap, AIP creation, AIP reconciliation, checklist validation, and zero-context AGENT_PROMPT generation. Trigger when the user asks to bootstrap AFW, create or update an AIP, validate `CHECKLIST.yaml`, reconcile packet docs, or generate `AGENT_PROMPT.txt`.
---

# AgenticFlywheel

Use this skill only for explicit AFW workflow requests or when a repo already uses AFW and the task clearly requires its packet workflow.

## Detect the Layout First

Prefer one of these layouts:

1. Framework source repo:
   - `prompts/`
   - `templates/`
   - `spec/AIP_FRAMEWORK.md`
2. Vendored framework:
   - `AgenticFlywheel/prompts/`
   - `AgenticFlywheel/templates/`
   - `AgenticFlywheel/spec/AIP_FRAMEWORK.md`
3. Installed framework:
   - `docs/AIP_FRAMEWORK.md`
   - `docs/templates/AIP/`
   - `docs/templates/aip-lite/`
   - `docs/features/REGISTRY.yaml`

If neither layout exists, say that AFW is not installed in the repo and stop unless the user is explicitly asking you to install/bootstrap it.

Always read `AGENTS.md` before applying the workflow.

## Workflow Selection

### Bootstrap AFW

Use when the user asks to install or bootstrap the framework.

Read, in order:
- `prompts/SYSTEM_BOOTSTRAP.md` when working in the AFW source repo
- `AgenticFlywheel/prompts/SYSTEM_BOOTSTRAP.md` when the vendored framework exists
- `prompts/AGENTS_CONFIG_TAILOR.md` or `AgenticFlywheel/prompts/AGENTS_CONFIG_TAILOR.md` when Claude/Codex/Cursor config updates are in scope
- `spec/AIP_FRAMEWORK.md` or `AgenticFlywheel/spec/AIP_FRAMEWORK.md`

Execution rules:
- Inspect the repo first and infer as much as possible before asking questions.
- Propose a file plan before writing.
- Show concise diffs before writing.
- For Claude Code, prefer `.claude/CLAUDE.md` plus `.claude/skills/agentic-flywheel/` over the legacy `.claude/PROJECT_PROMPT.md` pattern.
- If `.claude/CLAUDE.md` already exists, preserve it. Add only the minimum AFW-specific facts and routing rules needed for Claude to use AFW correctly. Do not rewrite unrelated content or restructure the file unless the user explicitly asks for that.

### Create or Update an AIP

Use when the user says `new AIP`, `create AIP`, `start AIP for this change`, or asks to plan a feature with AFW.

Read, in order:
- `prompts/AIP_COLLAB.md` or `AgenticFlywheel/prompts/AIP_COLLAB.md` for guided Q&A
- `prompts/AIP_NEW.md` or `AgenticFlywheel/prompts/AIP_NEW.md` for direct scaffolding
- `spec/AIP_FRAMEWORK.md`, `docs/AIP_FRAMEWORK.md`, or `AgenticFlywheel/spec/AIP_FRAMEWORK.md`
- `templates/aip/*`, `docs/templates/AIP/*`, or vendored template sources
- `templates/aip-lite/*`, `docs/templates/aip-lite/*`, or vendored lite template sources

Execution rules:
- Choose lightweight vs full AIP using AFW scale guidance.
- Ask only the minimum questions required to define scope, contracts, risks, and verification.
- Update the feature registry as part of the proposal.
- Do not generate `AGENT_PROMPT.txt` during AIP creation.

### Reconcile an Existing Packet

Use when the user asks to repair, realign, or update an AIP after the implementation changed.

Read:
- `prompts/AIP_RECONCILE.md` or `AgenticFlywheel/prompts/AIP_RECONCILE.md`
- The packet’s `CHECKLIST.yaml`
- The packet docs that drifted from reality

### Validate a Checklist

Use when the user asks whether a packet is structurally complete or shippable.

Read:
- `prompts/CHECKLIST_VALIDATOR.md` or `AgenticFlywheel/prompts/CHECKLIST_VALIDATOR.md`
- `templates/aip/CHECKLIST.schema.json`, `docs/templates/AIP/CHECKLIST.schema.json`, or `AgenticFlywheel/templates/aip/CHECKLIST.schema.json`
- The target `CHECKLIST.yaml`

Execution rules:
- Check required phases, status coherence, verification commands, and registry update coverage.
- Propose a minimal patch when the checklist is invalid.

### Generate `AGENT_PROMPT.txt`

Use only after the packet docs are complete.

Read:
- `prompts/AGENT_PROMPT_GENERATOR.md` or `AgenticFlywheel/prompts/AGENT_PROMPT_GENERATOR.md`
- `templates/aip/AGENT_PROMPT_AUTHORING_GUIDE.md`, `docs/templates/AIP/AGENT_PROMPT_AUTHORING_GUIDE.md`, or the vendored template path
- `templates/aip/AGENT_PROMPT_QA_CHECKLIST.md`, `docs/templates/AIP/AGENT_PROMPT_QA_CHECKLIST.md`, or the vendored template path
- The packet docs, especially `CHECKLIST.yaml`

Execution rules:
- Treat `CHECKLIST.yaml` as canonical.
- Generate the prompt last.
- Show the full draft or a concise diff before writing.

## Output Expectations

- Report which AFW layout you detected.
- Name the files or packet you used as sources.
- Keep user questions short and targeted.
- Before writing, show a plan and a diff preview.
- After writing, summarize changed paths and the next AFW step.
