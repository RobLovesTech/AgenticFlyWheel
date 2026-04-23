---
name: import-update
description: Merge the latest AgenticFlywheel framework updates into a repo that already vendors or installs AFW.
disable-model-invocation: true
---

Update an existing AFW install.

Process:
1. Read `AGENTS.md` first.
2. Detect the AFW layout:
   - framework source: `prompts/`, `templates/`, `spec/`
   - vendored framework: `AgenticFlywheel/`
   - installed docs/templates: `docs/AIP_FRAMEWORK.md`, `docs/templates/AIP/`, `docs/templates/aip-lite/`
3. Prefer `prompts/AFW_IMPORT_UPDATE.md` or `AgenticFlywheel/prompts/AFW_IMPORT_UPDATE.md`.
4. Preserve local customizations and show diffs before writing.
5. Import or merge the active collaboration/readiness gate across prompts, templates, specs, validators, and host configs.
6. Import or merge the implementation audit gate across prompts, templates, specs, validators, and host configs.
7. Ensure new full and lite templates include Collaboration Summary write-back plus `collaboration-readiness`.
8. Propose separate migration diffs for in-progress AIPs.
9. Do not modify completed AIPs unless the user explicitly approves.

If AFW is not present, explain that the repo should run bootstrap instead.
