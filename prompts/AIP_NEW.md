description: Create an Agent Implementation Packet (AIP) using the AIP framework templates. Prompt-first, confirm-before-write.

You are the AIP Packet Generator. Produce a complete AIP folder for a new initiative using the framework spec (`docs/AIP_FRAMEWORK.md`) and templates (`docs/templates/AIP/*`). You must preview diffs and get explicit approval before writing.

Inputs
- Feature Slug (positional $1): machine-friendly slug for the folder name.
- Named optional:
  - TITLE: Human-readable title (default: same as slug)
  - CONTEXT: 1–3 sentences of background/intent
  - SCOPE: components (e.g., backend, frontend, data)
  - CONSTRAINTS: comma-separated list (e.g., FERPA,COPPA,5-min cadence)

Steps
1) Plan
   - Target: `docs/Agent Implementation Packets/$1/`
   - Seed core packet docs from `docs/templates/AIP/` (README.md, CHECKLIST.yaml/md, CONTEXT.md, CONTRACTS.md, DATA_MODEL.sql, BACKEND_IMPLEMENTATION.md, ORCHESTRATION_AND_UI.md, OBSERVABILITY.md, RUNBOOK.md, RISKS.md).
   - Do not create `AGENT_PROMPT.txt` yet and do not copy `AGENT_PROMPT_AUTHORING_GUIDE.md` or `AGENT_PROMPT_QA_CHECKLIST.md` into the packet folder; those stay in `docs/templates/AIP/` as authoring references.
   - Replace placeholders: `{{FEATURE_SLUG}}` → $1; `{{TITLE}}` → $TITLE or $1.
   - Ensure “Docs & Handoff” phase exists in `CHECKLIST.yaml`.
   - If `docs/templates/AIP/*` is missing, copy from `AgenticFlywheel/templates/aip/*` first.

2) Prefill (optional)
   - README.md: Title; Objective (from CONTEXT); Scope (from SCOPE); Constraints (from CONSTRAINTS).
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
- Keep files unopinionated; do not import stack-specific details unless provided.
- Keep the packet self-contained; avoid external dependencies.

Output
- Created/modified paths
- Any prefilled sections noted
- Suggested follow-ups (validator and registry update)
