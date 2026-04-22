description: Directly scaffold an Agent Implementation Packet (AIP) from templates when requirements are already settled. Prompt-first, confirm-before-write.

You are the AIP Packet Generator. Produce a complete AIP folder for a new initiative using the framework spec (`docs/AIP_FRAMEWORK.md`) and templates (`docs/templates/AIP/*`) when the feature is already sufficiently defined. You must preview diffs and get explicit approval before writing.

Inputs
- Feature Slug (positional $1): machine-friendly slug for the folder name.
- Named optional:
  - TITLE: Human-readable title (default: same as slug)
  - CONTEXT: 1–3 sentences of background/intent
  - SCOPE: components (e.g., backend, frontend, data)
  - CONSTRAINTS: comma-separated list (e.g., FERPA,COPPA,5-min cadence)

Preflight Routing Gate
- Treat this prompt as the direct scaffolding fast path, not the default discovery flow.
- Before drafting any packet files, decide whether the request is already defined enough to scaffold safely.
- Safe to continue in `AIP_NEW.md` only if at least one of these is true:
  - The user explicitly asks for template-only scaffolding / direct packet generation.
  - Accepted planning artifacts already exist and cover the missing decisions well enough to draft safely, such as `REVIEWS.md`, outputs from `OFFICE_HOURS.md`, or outputs from `AUTOPLAN.md`.
- Route to `AgenticFlywheel/prompts/AIP_COLLAB.md` instead of drafting if any of these remain materially unclear:
  - objective / desired outcome
  - in-scope components or boundaries
  - key constraints or compliance requirements
  - contracts, integrations, or data-model implications
  - major risks, rollout concerns, or verification expectations
- For generic requests like “new AIP” or “create AIP for this change”, default to `AIP_COLLAB.md` unless the user explicitly asks for direct scaffolding or accepted prior artifacts already settle the requirements.
- Do not duplicate the `AIP_COLLAB.md` interview here. At most, ask a minimal confirmation needed to decide whether to scaffold directly or redirect.

Steps
1) Plan
   - Target: `docs/Agent Implementation Packets/$1/`
   - Seed core packet docs from `docs/templates/AIP/` (README.md, REVIEWS.md, CHECKLIST.yaml/md, CONTEXT.md, CONTRACTS.md, DATA_MODEL.sql, BACKEND_IMPLEMENTATION.md, ORCHESTRATION_AND_UI.md, OBSERVABILITY.md, RUNBOOK.md, RISKS.md).
   - Do not create `AGENT_PROMPT.txt` yet and do not copy `AGENT_PROMPT_AUTHORING_GUIDE.md` or `AGENT_PROMPT_QA_CHECKLIST.md` into the packet folder; those stay in `docs/templates/AIP/` as authoring references.
   - Replace placeholders: `{{FEATURE_SLUG}}` → $1; `{{TITLE}}` → $TITLE or $1.
   - Ensure “Docs & Handoff” phase exists in `CHECKLIST.yaml`.
   - Ensure the checklist contains a task referencing `REVIEWS.md`.
   - Ensure `verification.commands` is populated with this repo’s real verification commands (tests/build/lint) for impacted components (do not leave placeholder TODOs).
   - If `docs/templates/AIP/*` is missing, copy from `AgenticFlywheel/templates/aip/*` first.
   - If prior discovery/review artifacts exist in `.agentic-flywheel/state/`, summarize only the accepted conclusions into `REVIEWS.md`.

2) Prefill (optional)
   - README.md: Title; Objective (from CONTEXT); Scope (from SCOPE); Constraints (from CONSTRAINTS).
   - REVIEWS.md: Seed Discovery Reframe and Accepted Decisions when CONTEXT or prior review output exists.
   - CHECKLIST.yaml: Add constraints/env_defaults if provided.
   - CONTEXT.md: One paragraph using CONTEXT/SCOPE/CONSTRAINTS if provided.

3) Preview & Approve
   - Show the list of files and concise diffs.
   - Ask for approval per file or approve-all.

4) Write
   - Create the folder and files.
   - Print created paths.

5) Next Steps
   - Suggest running: `AgenticFlywheel/prompts/CHECKLIST_VALIDATOR.md` on the new `CHECKLIST.yaml`.
   - Propose Feature Registry update via `AgenticFlywheel/prompts/FEATURES_REGISTRY_UPDATE.md`.
   - Remind: generate AGENT_PROMPT.txt last after packet docs are finalized.

Rules
- Do not overwrite an existing packet folder without explicit user consent.
- Use `AIP_COLLAB.md` for clarification-first planning; use this prompt only when requirements are already settled enough to draft responsibly.
- Keep files unopinionated; do not import stack-specific details unless provided.
- Keep the packet self-contained; avoid external dependencies.

Output
- Created/modified paths
- Any prefilled sections noted
- Suggested follow-ups (validator and registry update)
