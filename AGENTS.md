# Repository Guidelines

## Project Structure & Module Organization
- Root docs such as `README.md`, `spec/AIP_FRAMEWORK.md`, and `spec/EXECUTION_LAYER.md` define the AgenticFlywheel control plane and runtime layer.
- `prompts/` contains the prompt workflows (e.g. `SYSTEM_BOOTSTRAP.md`, `AIP_NEW.md`, `IMPLEMENTATION_AUDIT.md`, `OFFICE_HOURS.md`, `SHIP.md`) that agents run inside AI tools.
- `templates/` holds reusable AIP and AIP‑Lite packet templates (`templates/aip/**`, `templates/aip-lite/**`) plus config templates under `templates/config/**`.
- `features/REGISTRY.schema.json` defines the schema for downstream feature registries; keep it backward compatible.

## Build, Test, and Development Flow
- This repository is docs‑ and schema‑only; there is no compile or build step.
- To exercise flows, run the prompts in `prompts/` against a sample repo (start with `SYSTEM_BOOTSTRAP.md`, then `OFFICE_HOURS.md`/`AUTOPLAN.md`, then `TUTORIAL_FIRST_AIP.md`, then `IMPLEMENTATION_AUDIT.md` before packet closure).
- When editing schemas, validate them with your preferred JSON Schema tool (e.g. `ajv`, `spectral`) before opening a PR.

## Coding Style & Naming Conventions
- Use Markdown with ATX headings (`#`, `##`) and concise, instructional language.
- Use 2‑space indentation for YAML; format JSON schemas with 2‑space indentation and sorted keys where practical.
- Prompt files in `prompts/` use UPPER_SNAKE_CASE names (e.g. `AIP_COLLAB.md`); new prompts must follow this pattern.
- Template and spec paths in docs should be explicit (e.g. `docs/Agent Implementation Packets/<feature-slug>/CHECKLIST.yaml`).

## Testing Guidelines
- For prompt changes, manually walk through at least one end‑to‑end flow (bootstrap → AIP creation → checklist validation) and note results in the PR.
- For schema updates (`features/REGISTRY.schema.json`, `templates/aip/CHECKLIST.schema.json`), add or update example payloads and validate them.
- Avoid breaking existing downstream contracts; prefer additive changes and document any deprecations in `spec/AIP_FRAMEWORK.md`.

## Commit & Pull Request Guidelines
- Write clear, imperative commit messages (e.g. `prompts: refine SYSTEM_BOOTSTRAP wizard`, `templates: add AIP-Lite checklist example`).
- PR descriptions should summarize intent, list touched prompts/templates/schemas, and describe how you manually tested flows.
- Link any tracking issues and, when UX or agent behavior changes, include a brief transcript or summary of a representative run.

## Agent-Specific Instructions
- Agents working in downstream repos should treat the local `AGENTS.md` as the source of truth for process, paths, and validation steps.
- When bootstrapping a repo with AgenticFlywheel, ensure `AGENTS.md` is updated to reflect the installed prompt set, docs layout, and testing commands.
