<img width="2752" height="1536" alt="image" src="https://github.com/user-attachments/assets/4f14fb02-1f25-4d2c-ad7f-024173f2279e" />

Version: 1.0.0

# AgenticFlyWheel: Prompt-First Control Plane for Systematic AI Development

**Turn AI-assisted feature work into a repeatable system of collaboration, packet truth, verification, and audit-backed closure.**

*Version 1.0.0 | Architecture-agnostic | Prompt-first | Zero dependencies*

[Why AFW](#why-afw) | [How It Works](#how-afw-works) | [Quick Start](#quick-start) | [Prompt Map](#prompt-map) | [Packet Types](#packet-types) | [Host Surfaces](#host-surfaces) | [Updating Existing Installs](#updating-an-existing-afw-install)

---

## Framework Highlights

- Collaboration-first by default: packet-sized work starts with `prompts/AIP_COLLAB.md`, not silent scaffolding.
- AIP collaboration is mode-aware: the intake can classify work as `technical`, `operating`, or `mixed` and probe non-technical requirements deeply when rollout, GTM, client transition, enablement, or approvals matter.
- Full packets are manifest-driven: `CHECKLIST.yaml` records `packet_level`, `requirements_mode`, `delivery_surfaces`, `enabled_modules`, and `omitted_modules`.
- Full packet creation includes both prompt artifacts up front: `AGENT_PROMPT.txt` and `IMPLEMENTATION_AUDIT_PROMPT.txt`.
- Packet closure requires the full chain: verification -> audit -> remediation -> re-verification -> closure.
- Runtime state under `.agentic-flywheel/state/` is advisory only. Packet docs remain canonical.

If you already installed an older AFW version into another repo, use `prompts/AFW_IMPORT_UPDATE.md` to merge the newer collaboration and audit gates without clobbering local customizations.

---

## Why AFW

Most AI development breaks in the same places:

- intent gets lost across chats and handoffs
- implementation moves faster than contracts, tests, and docs
- "done" gets claimed before the repo has trustworthy closure evidence
- every feature becomes its own one-off pattern

AFW solves that by turning feature work into a control plane:

1. active collaboration locks the real intent before packet truth is written
2. AIPs make the work self-contained and restartable
3. checklists force execution through verification and docs sync
4. implementation audit prevents paper-complete but reality-incomplete closure

This is not a generic prompt collection. It is a framework for making AI-assisted work more reliable over time.

---

## What This Repo Is

This repository is the **framework source**.

It is not the downstream installed layout used inside a product repo after bootstrap. In this repo, the source-of-truth framework assets live here:

- `prompts/`
- `spec/`
- `templates/aip/`
- `templates/aip-lite/`
- `templates/config/`
- `templates/claude-plugin/agentic-flywheel/`
- `features/REGISTRY.schema.json`
- `model-overlays/`

After bootstrap in another repo, AFW is typically installed into:

- `docs/AIP_FRAMEWORK.md`
- `docs/templates/AIP/*`
- `docs/templates/aip-lite/*`
- `docs/features/REGISTRY.yaml`
- `docs/features/REGISTRY.schema.json`
- `docs/ai/**`

That source-vs-installed distinction matters. This repo defines the framework; downstream repos consume the installed docs layout.

---

## How AFW Works

### 1. Bootstrap

Run `prompts/SYSTEM_BOOTSTRAP.md` in the target repo.

Bootstrap is repo-discovery-first. It supports `Minimal Boot`, `Standard Boot`, and `Custom Boot`, installs the framework surfaces, seeds the Feature Registry, and can propose host config updates.

### 2. Collaborate Before Scaffolding

For new packet-sized work, start with `prompts/AIP_COLLAB.md`.

The collaboration gate locks:

- requirements mode (`technical`, `operating`, or `mixed`) plus collaborating functions
- goal and desired outcome
- personas and per-persona scope
- in-scope and out-of-scope work
- acceptance signals
- contract or data-model implications
- operating process changes, ownership, and handoffs when relevant
- GTM, launch, client rollout, enablement, support, and approval requirements when relevant
- rollout and rollback expectations
- verification commands
- risks and non-goals

`prompts/AIP_NEW.md` is the direct scaffold/write fast path, not the default intake path.

The Collaboration Summary is a structured readiness receipt. At minimum it should record:

- confirmation basis
- confirmed by
- confirmed at
- confirmed decisions
- accepted assumptions
- open questions or deferred follow-ups
- persona scope decisions
- operating readiness decisions when applicable

### Requirements Modes

- `technical`: primarily code, contracts, data, UI, observability, and runbook work
- `operating`: primarily process, rollout, GTM, client-transition, enablement, support, governance, or approval work
- `mixed`: both technical and operating requirements are first-class and belong in one packet

### 3. Execute Through Closure

Implementation follows `CHECKLIST.yaml`, then must complete the required closure chain:

1. run verification commands
2. validate packet structure and readiness with `prompts/CHECKLIST_VALIDATOR.md` when appropriate
3. sync docs and run prompt QA
4. refresh `AGENT_PROMPT.txt` and, for full AIPs, `IMPLEMENTATION_AUDIT_PROMPT.txt`
5. run the implementation audit flow using `prompts/IMPLEMENTATION_AUDIT.md` and the packet-local audit wrapper for full AIPs
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

1. Run `@AgenticFlyWheel/prompts/AGENTS_CONFIG_TAILOR.md` to wire Claude, Codex, Cursor, or Gemini CLI into the docs-first AFW flow.
2. Start your first packet with `@AgenticFlyWheel/prompts/AIP_COLLAB.md`.
3. Use `@AgenticFlyWheel/prompts/IMPLEMENTATION_AUDIT.md` before closing that packet.

### Work on AFW itself

If you are editing this framework repo, the source-of-truth files are the framework-source paths in this checkout:

- prompts: `prompts/*.md`
- specs: `spec/*.md`
- templates: `templates/aip/**`, `templates/aip-lite/**`
- host configs: `templates/config/**`

Do not describe framework-source behavior using downstream `docs/...` paths unless you are explicitly documenting the installed layout in another repo.

---

## Prompt Map

### Core workflow prompts

| Prompt | Purpose |
|--------|---------|
| `prompts/SYSTEM_BOOTSTRAP.md` | Install AFW into a repo and generate the initial docs foundation |
| `prompts/AGENTS_CONFIG_TAILOR.md` | Propose host config updates for Claude, Codex, Cursor, and Gemini CLI |
| `prompts/AIP_COLLAB.md` | Collaboration-first intake for new or updated packets |
| `prompts/AIP_NEW.md` | Scaffold or update a packet only after collaboration readiness is satisfied |
| `prompts/CHECKLIST_VALIDATOR.md` | Validate checklist structure, readiness evidence, and closure gates |
| `prompts/AGENT_PROMPT_GENERATOR.md` | Generate or refresh `AGENT_PROMPT.txt` |
| `prompts/IMPLEMENTATION_AUDIT.md` | Required post-implementation audit before packet closure |
| `prompts/AIP_RECONCILE.md` | Reconcile packet truth with accepted changes or follow-on decisions |
| `prompts/AFW_IMPORT_UPDATE.md` | Update an existing AFW install to the latest framework gates |

### Supporting prompts

- `prompts/OFFICE_HOURS.md`, `prompts/AUTOPLAN.md` for deeper planning when scope, risk, or tradeoffs need more pressure-testing
- `prompts/PRELANDING_REVIEW.md`, `prompts/QA.md`, `prompts/SHIP.md` for reusable review and release flows
- `prompts/CONTEXT_SAVE.md`, `prompts/CONTEXT_RESTORE.md`, `prompts/GUARD_MODE.md`, `prompts/LEARNINGS.md` for runtime support and operator workflows
- `prompts/FEATURES_REGISTRY_*` for bootstrap, update, validate, and retrofit registry entries

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

Full AIPs may be `technical`, `operating`, or `mixed` depending on whether the packet is mostly code delivery, mostly operating/change-readiness work, or both.

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
- `OPERATING_MODEL.md`
- `GTM_AND_LAUNCH.md`
- `CLIENT_ROLLOUT.md`
- `ENABLEMENT_AND_SUPPORT.md`
- `GOVERNANCE_AND_APPROVALS.md`

New full packets should record their shape directly in `CHECKLIST.yaml`:

```yaml
packet_level: full
requirements_mode: mixed
delivery_surfaces:
  - backend
  - operations
  - client_rollout
enabled_modules:
  - contracts
  - backend_implementation
  - client_rollout
omitted_modules:
  - module: observability
    reason: "No metrics or rollout changes in this packet"
```

Older full packets without the manifest remain valid. Prompts and validators should infer their shape from the packet docs already present.

---

## What AFW Emphasizes

- Active collaboration before packet truth
- Repo-tracked docs as the canonical control plane
- Restartable implementation through packet-local prompt artifacts
- Verification commands that match the real repo
- Honest closure only after audit findings are resolved or explicitly dispositioned

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

The result is a development loop where each finished feature becomes easier to reason about, safer to change, and faster to ship.

---

## Bottom Line

AgenticFlyWheel helps teams replace ad hoc AI sessions with repeatable collaboration, explicit packet truth, repo-grounded verification, and audit-backed closure.

If you want the framework in another repo, start with:

```text
@AgenticFlyWheel/prompts/SYSTEM_BOOTSTRAP.md
```
