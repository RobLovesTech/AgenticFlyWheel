<img width="2752" height="1536" alt="image" src="https://github.com/user-attachments/assets/4f14fb02-1f25-4d2c-ad7f-024173f2279e" />

Version: 1.0.0

AgenticFlyWheel Framework (Self-Sustaining AI-Human Development)

**Turn AI development chaos into a self-sustaining engine of quality**

*Version 1.0.0 | Architecture-agnostic | Prompt-first | Zero dependencies*

---

## The 30-Second Version

**Before AgenticFlyWheel:** every AI-driven feature is a snowflake. Patterns drift, docs go stale, tests get skipped, and intent disappears into chat history.

**After AgenticFlyWheel:** feature work moves through a repeatable control plane: active collaboration, packet scaffolding, checklist-driven implementation, docs sync, required audit, remediation, and clean closure.

The goal is not "more process." The goal is reliable velocity that compounds instead of rotting.

---

## What Changed In The Current Framework

This repo now reflects a stricter AFW model than the older README described:

- New packet work defaults to **active collaboration first** through `prompts/AIP_COLLAB.md`.
- A detailed request is still only **seed context** until the user confirms the Collaboration Summary.
- Full packets now use a **manifest-driven shape** in `CHECKLIST.yaml` with `packet_level`, `enabled_modules`, and `omitted_modules`.
- Full packet creation includes both `AGENT_PROMPT.txt` and `IMPLEMENTATION_AUDIT_PROMPT.txt` in the initial approval bundle.
- Packet closure now requires the full chain: **verification -> implementation audit -> remediation -> re-verification -> packet closure**.
- Runtime state under `.agentic-flywheel/state/` is advisory only. Packet docs remain canonical.

If you already installed an older AFW version into another repo, use `prompts/AFW_IMPORT_UPDATE.md` to merge these gates in without clobbering local customizations.

---

## What This Repo Contains

This repository is the **framework source**. It is not the installed downstream docs layout.

### Framework source layout

- `prompts/` - executable workflow prompts such as bootstrap, collaboration, audit, QA, ship, and import/update
- `spec/` - framework specs, especially `spec/AIP_FRAMEWORK.md` and `spec/EXECUTION_LAYER.md`
- `templates/aip/` - full AIP templates
- `templates/aip-lite/` - lightweight AIP templates
- `templates/config/` - host config templates for Claude, Codex, and Cursor
- `templates/claude-plugin/agentic-flywheel/` - Claude-native plugin scaffold
- `features/REGISTRY.schema.json` - schema for downstream feature registries
- `model-overlays/` - host-specific behavioral overlays

### Installed downstream layout

After running bootstrap in a product repo, AFW is typically copied into:

- `docs/AIP_FRAMEWORK.md`
- `docs/templates/AIP/*`
- `docs/templates/aip-lite/*`
- `docs/features/REGISTRY.yaml`
- `docs/features/REGISTRY.schema.json`
- `docs/ai/**`

That source-vs-installed distinction matters. In this repo, templates live under `templates/`. In a bootstrapped product repo, they live under `docs/templates/`.

---

## How AFW Works

### 1. Bootstrap

Run `prompts/SYSTEM_BOOTSTRAP.md` in the target repo. It is repo-discovery-first, asks only a few confirmation questions when needed, supports `Minimal Boot`, `Standard Boot`, and `Custom Boot`, installs the AIP framework, seeds the Feature Registry, and can propose host config updates.

### 2. Collaborate Before Scaffolding

For new packet-sized work, start with `prompts/AIP_COLLAB.md`.

The collaboration gate locks:

- goal and desired outcome
- personas and per-persona scope
- in-scope and out-of-scope work
- acceptance signals
- contracts or data model implications
- rollout and rollback expectations
- verification commands
- risks and non-goals

`prompts/AIP_NEW.md` is now the **direct scaffolding fast path**, not the default intake path.

The Collaboration Summary is now a structured readiness receipt. At minimum it should record:

- confirmation basis
- confirmed by
- confirmed at
- confirmed decisions
- accepted assumptions
- open questions or deferred follow-ups
- persona scope decisions

### 3. Execute Through Closure

Implementation follows `CHECKLIST.yaml`, then must complete the required closure chain:

1. run verification commands
2. run `prompts/CHECKLIST_VALIDATOR.md` when validating packet structure and closure readiness
3. sync docs and run prompt QA before refreshing prompt artifacts
4. refresh `AGENT_PROMPT.txt` and, for full AIPs, `IMPLEMENTATION_AUDIT_PROMPT.txt`
5. run the required implementation audit flow using `prompts/IMPLEMENTATION_AUDIT.md` plus the packet-local `IMPLEMENTATION_AUDIT_PROMPT.txt` for full AIPs
6. fix or explicitly disposition findings
7. re-run targeted verification
8. close the packet

---

## Quick Start

### Install AFW into another repo

```bash
# From the target repo root
cp -R /path/to/AgenticFlyWheel ./AgenticFlyWheel
```

Then run:

```text
@AgenticFlyWheel/prompts/SYSTEM_BOOTSTRAP.md
```

Recommended next steps after bootstrap:

1. Run `@AgenticFlyWheel/prompts/AGENTS_CONFIG_TAILOR.md` to wire Claude, Codex, and/or Cursor into the docs-first AFW flow.
2. Start your first packet with `@AgenticFlyWheel/prompts/AIP_COLLAB.md`.
3. Use `@AgenticFlyWheel/prompts/IMPLEMENTATION_AUDIT.md` before closing that packet.

### Use AFW inside this framework repo

If you are editing AFW itself, the source-of-truth files are the ones in this repo:

- prompts: `prompts/*.md`
- specs: `spec/*.md`
- templates: `templates/aip/**`, `templates/aip-lite/**`
- host configs: `templates/config/**`

Do not document framework-source behavior using downstream `docs/...` paths unless you are explicitly describing the installed layout in a target repo.

---

## Prompt Map

### Core workflow prompts

- `prompts/SYSTEM_BOOTSTRAP.md` - install AFW into a repo and generate the initial docs foundation
- `prompts/AGENTS_CONFIG_TAILOR.md` - propose host config updates for Claude, Codex, Cursor, and Gemini CLI
- `prompts/AIP_COLLAB.md` - collaboration-first intake for new or updated packets
- `prompts/AIP_NEW.md` - scaffold or update a packet only after collaboration readiness is satisfied
- `prompts/CHECKLIST_VALIDATOR.md` - validate packet checklist structure, readiness evidence, and closure gates
- `prompts/AGENT_PROMPT_GENERATOR.md` - generate or refresh `AGENT_PROMPT.txt`
- `prompts/IMPLEMENTATION_AUDIT.md` - required post-implementation audit before packet closure
- `prompts/AIP_RECONCILE.md` - reconcile packet truth with accepted changes or follow-on decisions
- `prompts/AFW_IMPORT_UPDATE.md` - update an existing AFW install to the latest framework gates

### Supporting prompts

- `prompts/OFFICE_HOURS.md`, `prompts/AUTOPLAN.md` - deeper planning before packet creation when risk or scope is high
- `prompts/PRELANDING_REVIEW.md`, `prompts/QA.md`, `prompts/SHIP.md` - reusable review and release prompts
- `prompts/CONTEXT_SAVE.md`, `prompts/CONTEXT_RESTORE.md`, `prompts/GUARD_MODE.md`, `prompts/LEARNINGS.md` - runtime support and operator workflows
- `prompts/FEATURES_REGISTRY_*` - bootstrap, update, validate, and retrofit registry entries

---

## Packet Types

### No AIP

Use for trivial work such as typos, tiny docs fixes, or very narrow low-risk changes.

### AIP-Lite

Use for smaller single-sided changes that still need explicit scope, verification, and closure discipline.

Required tracked artifacts:

- `README.md`
- `CHECKLIST.yaml`

Optional artifact:

- `AGENT_PROMPT.txt` when the repo wants a zero-context handoff for the change

### Full AIP

Use for larger feature work, cross-cutting changes, multi-surface implementation, contract changes, migrations, or anything that needs a stronger planning and closure surface.

Required tracked artifacts:

- `README.md`
- `REVIEWS.md`
- `CHECKLIST.yaml`
- `CHECKLIST.md`
- `CONTEXT.md`
- `RISKS.md`
- `AGENT_PROMPT.txt`
- `IMPLEMENTATION_AUDIT_PROMPT.txt`

Optional capability modules:

- `CONTRACTS.md`
- `DATA_MODEL.sql`
- `BACKEND_IMPLEMENTATION.md`
- `ORCHESTRATION_AND_UI.md`
- `OBSERVABILITY.md`
- `RUNBOOK.md`

New full packets should record their shape directly in `CHECKLIST.yaml`:

```yaml
packet_level: full
enabled_modules:
  - contracts
  - backend_implementation
omitted_modules:
  - module: observability
    reason: "No metrics or rollout changes in this packet"
```

Older full packets without the manifest remain valid. Prompts and validators should infer their shape from the packet docs already present.

---

## Collaboration And Closure Rules

These are the rules most worth internalizing:

- Generic requests like `new AIP`, `create AIP`, or `start AIP` should default to `AIP_COLLAB.md`.
- A specific feature description can shorten the collaboration round, but it does not authorize packet writes by itself.
- `collaboration-readiness` must exist before implementation work begins.
- Full packets write the Collaboration Summary into `REVIEWS.md`.
- AIP-Lite writes the Collaboration Summary into `README.md`.
- Inferred assumptions are not accepted assumptions until the user confirms them or explicitly chooses a direct/template-only scaffold exception.
- Full packet creation must include both prompt artifacts up front: `AGENT_PROMPT.txt` and `IMPLEMENTATION_AUDIT_PROMPT.txt`.
- Packet completion is not honest until the implementation audit has run and its actionable findings are resolved or explicitly dispositioned.

---

## Host Surfaces

AFW supports multiple host experiences. In this repo, the current shipped surfaces are:

| Host Surface | Path | Purpose |
|--------------|------|---------|
| Claude project config | `templates/config/.claude/CLAUDE.md` | Stable repo-level AFW guidance |
| Claude project prompt compatibility layer | `templates/config/.claude/PROJECT_PROMPT.md` | Compatibility with older Claude repo setups |
| Claude project skill | `templates/config/.claude/skills/agentic-flywheel/SKILL.md` | Repeatable AFW workflows in Claude |
| Codex config | `templates/config/.codex/agents.yml` | Docs-first Codex host configuration |
| Cursor rules | `templates/config/.cursor/rules/.cursorrules` | Lightweight Cursor routing and guardrails |
| Claude plugin scaffold | `templates/claude-plugin/agentic-flywheel/` | Focused native command surface for key AFW workflows |
| Model overlays | `model-overlays/claude.md`, `model-overlays/codex.md` | Host behavior overlays aligned with current AFW rules |

Use `AGENTS.md` as the first repo-specific source of truth after AFW is installed, regardless of host.

---

## Runtime Layer

`spec/EXECUTION_LAYER.md` defines AFW's local runtime layer.

Key ideas:

- repo-tracked packet docs are canonical
- `.agentic-flywheel/state/` is local, advisory, and gitignored
- runtime notes can inform work, but they do not change packet truth until promoted into packet docs
- accepted audit findings become closure blockers only after they are written back into packet truth

Canonical runtime paths:

- `.agentic-flywheel/state/checkpoints/`
- `.agentic-flywheel/state/learnings.jsonl`
- `.agentic-flywheel/state/reviews.jsonl`
- `.agentic-flywheel/state/timeline.jsonl`
- `.agentic-flywheel/state/question-prefs.json`

---

## Updating An Existing AFW Install

If a repo already vendors or installs AFW, run:

```text
@AgenticFlyWheel/prompts/AFW_IMPORT_UPDATE.md
```

That flow is designed to:

- preserve local customizations
- merge in the collaboration-readiness gate
- merge in the implementation-audit gate
- update templates and host configs
- flag in-progress packets that still need migration

---

## Why This Works

AFW combines four things that usually drift apart:

1. planning that captures real user intent
2. packet docs that stay self-contained and restartable
3. host routing that nudges agents into the right workflow
4. closure gates that force docs, verification, audit, and truth write-back to match reality

The result is a development loop where each finished feature makes the next one easier to reason about, safer to change, and faster to ship.

---

## Bottom Line

AgenticFlyWheel is a prompt-first control plane for systematic AI-assisted development. It helps teams replace ad hoc AI sessions with repeatable collaboration, explicit packet truth, honest audits, and low-friction handoff.

If you want the framework in another repo, start with:

```text
@AgenticFlyWheel/prompts/SYSTEM_BOOTSTRAP.md
```
