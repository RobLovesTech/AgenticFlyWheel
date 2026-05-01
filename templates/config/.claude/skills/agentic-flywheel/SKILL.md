---
name: agentic-flywheel
description: Use AgenticFlywheel for bootstrap, AIP creation, implementation audit, AIP reconciliation, checklist validation, and zero-context AGENT_PROMPT generation. Trigger when the user asks to bootstrap AFW, create or update an AIP, run the implementation audit, validate `CHECKLIST.yaml`, reconcile packet docs, or generate `AGENT_PROMPT.txt`.
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

### Import or Update AFW

Use when the user asks to update AFW, import AFW updates, or upgrade AgenticFlywheel in a repo that already vendors or installs it.

Read:
- `prompts/AFW_IMPORT_UPDATE.md` or `AgenticFlywheel/prompts/AFW_IMPORT_UPDATE.md`
- The repo's `AGENTS.md`
- Existing AFW source, vendored, or installed docs/templates layout

Execution rules:
- Preserve local customizations and show diffs before writing.
- Add or update the active collaboration/readiness gate across prompts, templates, specs, validators, and host configs.
- Add or update the implementation audit gate across prompts, templates, specs, validators, and host configs.
- Propose separate migration diffs for in-progress AIPs.
- Do not modify completed AIPs unless the user explicitly approves.

### Create or Update an AIP

Use when the user says `new AIP`, `create AIP`, `start AIP for this change`, or asks to plan a feature with AFW.

Read, in order:
- `prompts/AIP_COLLAB.md` or `AgenticFlywheel/prompts/AIP_COLLAB.md` for guided Q&A
- `prompts/AIP_NEW.md` or `AgenticFlywheel/prompts/AIP_NEW.md` for direct scaffolding
- `spec/AIP_FRAMEWORK.md`, `docs/AIP_FRAMEWORK.md`, or `AgenticFlywheel/spec/AIP_FRAMEWORK.md`
- `templates/aip/*`, `docs/templates/AIP/*`, or vendored template sources
- `templates/aip-lite/*`, `docs/templates/aip-lite/*`, or vendored lite template sources

Execution rules:
- Act as the AIP Collaboration Steward: active, precise, and protective of user intent.
- Treat generic requests like `new AIP` or `create AIP` as entry into the AIP flow, with `AIP_COLLAB.md` as the default route.
- Use `AIP_NEW.md` only when the user explicitly wants direct/template-only scaffolding or when accepted prior planning artifacts already settle the feature well enough to draft safely.
- Accepted outputs from `OFFICE_HOURS.md`, `AUTOPLAN.md`, existing `REVIEWS.md`, or equivalent review summaries can satisfy the preflight and avoid redundant questioning.
- Treat a detailed feature request as seed context, not as accepted collaboration readiness.
- Choose lightweight vs full AIP using AFW scale guidance.
- Ask short, targeted rounds until goals, user/operator impact, all personas (with per-persona scope confirmation), scope, non-goals, priority tiers (for large features with 3+ capability areas), acceptance, contracts/data model, reference data completeness, cross-cutting behaviors (lifecycle, grandfathering, evaluation semantics, defaults, audit scope), interaction surfaces (user journey walkthrough), rollout, risks, and verification are confirmed or explicitly accepted as assumptions.
- Reflect a Collaboration Summary and open assumptions before writing packet files.
- Stop for user confirmation after the first Collaboration Summary. Do not create or update packet files, mark `collaboration-readiness` complete, or implement in the same turn that first proposes the summary.
- Update the feature registry as part of the proposal.
- Ensure full AIPs write the Collaboration Summary to `REVIEWS.md`; ensure AIP-Lite writes it to README.md.
- Ensure the generated checklist includes `collaboration-readiness` before implementation tasks.
- Ensure the generated checklist includes `implementation-audit`, `audit-remediation`, `audit-reverify`, and `packet-closure`.
- For full AIPs, generate initial `AGENT_PROMPT.txt` and `IMPLEMENTATION_AUDIT_PROMPT.txt` during packet creation, then refresh prompt artifacts again during Docs & Handoff before the required implementation audit.

### Run Implementation Audit

Use when the user says `implementation audit`, `audit this AIP`, `run AIP audit`, or when an AIP is ready for closure.

Read:
- `prompts/IMPLEMENTATION_AUDIT.md` or `AgenticFlywheel/prompts/IMPLEMENTATION_AUDIT.md`
- The target packet docs, especially `CHECKLIST.yaml`
- Changed implementation files and verification evidence named by the packet

Execution rules:
- Run after implementation, verification, docs sync, and prompt-artifact refresh, before packet closure.
- Treat packet docs as canonical; runtime state is advisory only.
- Promote accepted findings into `REVIEWS.md` for full AIPs or README.md for AIP-Lite.
- Add remediation tasks for actionable findings.
- Block top-level `completed` until findings are fixed or explicitly dispositioned and targeted re-verification passes.
- Refresh prompt artifacts if audit-driven packet changes affect execution or handoff instructions.

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
- Check collaboration readiness, required phases, status coherence, verification commands, registry update coverage, implementation audit, audit remediation, audit re-verification, and packet closure coverage.
- Fail if a non-legacy in-progress or completed packet lacks `collaboration-readiness` or the expected Collaboration Summary write-back.
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
- Generate the prompt late in Docs & Handoff, and include the required implementation audit gate before packet closure.
- Show the full draft or a concise diff before writing.

## Output Expectations

- Report which AFW layout you detected.
- Name the files or packet you used as sources.
- Keep user questions short and targeted.
- Before writing, show a plan and a diff preview.
- After writing, summarize changed paths and the next AFW step.
