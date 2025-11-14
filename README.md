AgenticFlywheel Framework (Self‑Sustaining AI‑Human Development)

Version: 2.0.0

The Core Problem
When building with AI agents, development becomes **inconsistent and ad-hoc**:
- **Inconsistent patterns**: Each feature implemented differently; no standard approach to context gathering, planning, implementation, testing, or documentation.
- **Process shortcuts**: AI skips planning, testing, or docs updates because there's no enforcement mechanism — leading to fragile outcomes and technical debt.
- **Lost context**: Decisions and requirements scattered across chat histories, tickets, and PRs that can't be reconstructed or reused.
- **No traceability**: Features exist in code but aren't mapped to contracts, flags, metrics, or documentation.
- **Documentation drift**: Docs quickly become stale because updating them isn't part of the systematic workflow.

**Result**: AI development feels fast initially but creates chaos — inconsistent code quality, missing tests, broken context, unmaintainable features.

**Before AgenticFlywheel:**
```
User: "Add user authentication"
AI: [Writes code fast, skips tests, minimal docs]
User: "Add password reset"  
AI: [Different pattern, different structure, no connection to first feature]
User: "Where's the auth contract documented?"
AI: "Let me search... not sure, want me to infer from code?"
→ 6 months later: unmaintainable mess, no one knows how features work
```

**After AgenticFlywheel:**
```
User: "Add user authentication"
AI: [Runs AIP_COLLAB → creates packet with contracts, tests, observability]
AI: [Follows CHECKLIST.yaml → implements with tests, updates docs, updates registry]
User: "Add password reset"
AI: [Checks registry, finds auth AIP, follows same pattern, links in registry]
User: "Where's the auth contract?"
AI: "docs/features/REGISTRY.yaml → auth AIP → CONTRACTS.md line 23"
→ 6 months later: every feature documented, tested, traceable, maintainable
```

The Solution
**AgenticFlywheel enforces a systematic, repeatable development process** through prompt-based workflows that make AI agents follow consistent patterns:

**Context Gathering** → Tailored docs (`docs/ai/**`) generated via interview wizard
**Planning** → Structured Agent Implementation Packets (AIPs) with contracts, risks, acceptance criteria
**Development** → Phased execution enforced through `CHECKLIST.yaml` (Design → Backend → Frontend → Testing → Docs)
**Testing** → Required test tasks in every phase, no skipping
**Documentation** → "Docs & Handoff" is a mandatory final phase that updates all docs, registry, and generates restart prompts

**Key Mechanism**: Prompt-first workflows (not scripts) guide AI agents through validation gates, ensuring nothing gets skipped.

What This Is
- A **process enforcement framework** for AI-human collaboration that ensures consistent development patterns through structured Agent Implementation Packets (AIPs).
- **Prompt‑first workflows** (not scripts): Interview-style prompts guide AI agents through planning, implementation, testing, and documentation with validation at each step.
- **Architecture‑agnostic and principles‑based**: Works for any tech stack — layered, clean, hexagonal, monoliths, microservices, or event‑driven systems.
- **Flywheel effect**: Once bootstrapped, better docs → better AI results → better docs → faster, more reliable development.

Key Outcomes
**Consistency & Process Enforcement:**
- **Systematic workflow**: Every feature follows the same pattern — Context → Plan → Develop → Test → Document.
- **No skipped steps**: Validation gates ensure AI agents complete planning, testing, and documentation before moving forward.
- **Repeatable patterns**: AIPs provide templates and checklists that enforce consistent development practices across all features.

**Complete Context & Traceability:**
- **Tailored foundation**: `docs/ai/**` provides AI-specific docs (coding standards, testing, security, architecture, observability) generated from a short interview.
- **Feature Registry**: `docs/features/REGISTRY.yaml` maps every feature to its contracts, flags, metrics, owners, and AIP packets.
- **Zero-context restartability**: `AGENT_PROMPT.txt` in each AIP allows new AI sessions to continue without chat history.

**Quality & Maintainability:**
- **Contracts-first**: APIs, events, and schemas defined upfront with compatibility rules.
- **Acceptance-driven**: Every phase has explicit verification commands and acceptance criteria.
- **Self-maintaining docs**: "Docs & Handoff" phase is required, ensuring docs stay current with code.

**Safe & Practical:**
- **Idempotent workflows**: Confirm-before-write with diff previews — safe for existing repos.
- **Architecture-agnostic**: Works with any tech stack, language, or validation approach.
- **Prompt-based**: No scripts or dependencies to install; works in any AI tool (Claude, Cursor, Codex).

Included
- `spec/AIP_FRAMEWORK.md` — Portable AIP standard and framework specification.
- `templates/aip/*` — Full packet templates: `README.md`, `CHECKLIST.yaml` (+ guide + schema), `AGENT_PROMPT.txt`, `CONTEXT.md`, `CONTRACTS.md`, `DATA_MODEL.sql`, `BACKEND_IMPLEMENTATION.md`, `ORCHESTRATION_AND_UI.md`, `OBSERVABILITY.md`, `RUNBOOK.md`, `RISKS.md`.
- `templates/aip-lite/*` — Lightweight AIP templates: `README.md`, `CHECKLIST.yaml` for smaller features.
- `features/REGISTRY.schema.json` — JSON schema for Feature Registry with dependencies field.
- `prompts/` (run in your AI tool):
  - `prompts/SYSTEM_BOOTSTRAP.md` — Interviews you; discovers existing features; generates `docs/ai/**`, installs templates, bootstraps Feature Registry, proposes enhanced agent configs, and guides first AIP creation.
  - `prompts/CODEBASE_AUDIT.md` — Analyzes codebase to identify existing features for backfilling.
  - `prompts/FEATURES_RETROFIT.md` — Reverse-engineers AIPs for existing features.
  - `prompts/TUTORIAL_FIRST_AIP.md` — Interactive walkthrough creating your first real AIP.
  - `prompts/AIP_NEW.md` — Scaffolds a new AIP packet from templates with confirm‑before‑write.
  - `prompts/AIP_COLLAB.md` — Guided Q&A to design a feature, then emits a complete packet.
  - `prompts/DEPENDENCY_ANALYSIS.md` — Analyzes feature dependencies and assesses change impact.
  - `prompts/CHECKLIST_VALIDATOR.md` — Validates `CHECKLIST.yaml` structure and status coherence.
  - `prompts/AGENTS_CONFIG_TAILOR.md` — Proposes changes to agent configs with preview and consent.
  - `prompts/FEATURES_REGISTRY_BOOTSTRAP.md` — Creates `docs/features/REGISTRY.yaml` + schema.
  - `prompts/FEATURES_REGISTRY_UPDATE.md` — Adds/updates registry entries for features.
  - `prompts/FEATURES_REGISTRY_VALIDATE.md` — Validates registry schema, cross-links, and dependencies.
- `templates/config/` (enhanced agent configs with automatic search and dependency checking):
  - `.claude/PROJECT_PROMPT.md` — Claude-specific instructions
  - `.codex/agents.yml` — Codex agents configuration
  - `.cursor/rules/.cursorrules` — Cursor rules integration

When to Use Full vs Lightweight AIPs

Not every change needs the same level of documentation. Choose the right approach:

**No AIP Required** (document in commit message):
- Bug fixes and hotfixes
- Typo corrections or minor copy changes
- Small refactoring (<3 files, no behavior change)
- Documentation-only updates

**Lightweight AIP** (`templates/aip-lite/`):
- **Small features** (<2 days, <5 files touched)
- **Single-sided changes** (backend OR frontend, not both)
- **Simple additions** (basic CRUD, straightforward endpoints)
- **No complex contracts** (no external integrations or events)
- **Examples**: Add a filter to existing page, create simple report, add validation rule

**Full AIP** (`templates/aip/`):
- **Major features** (>5 days, multiple subsystems)
- **Full-stack changes** (backend + frontend + data)
- **New contracts** (APIs, events, webhooks, external integrations)
- **Database migrations** or schema changes
- **Gradual rollout** (feature flags, A/B tests, phased deployment)
- **Infrastructure changes** (new services, caching layers, architecture shifts)
- **Examples**: User authentication system, payment processing, data pipeline, dashboard redesign

**Decision Tree**:
```
Is it a bug fix or <3 files? → No AIP (commit message)
├─ No → Is it <2 days and single-sided? → Lightweight AIP
    ├─ No → Does it have complex contracts or affect multiple systems? → Full AIP
        ├─ No → Lightweight AIP
        └─ Yes → Full AIP
```

**When in doubt**: Start with lightweight. You can always expand to full AIP if complexity grows.

Principles

**Process Enforcement:**
- **Systematic workflow**: Every feature follows Context → Plan → Develop → Test → Document — no shortcuts allowed.
- **Required phases**: Backend Implementation, Frontend Implementation, and Docs & Handoff phases are mandatory in every AIP.
- **Required testing**: Test tasks (unit, integration) must exist within implementation phases and be marked complete.
- **Validation gates**: Checklist validators and registry validators ensure completeness before moving forward.
- **Zero-context continuity**: AGENT_PROMPT.txt enables AI sessions to restart without losing context or consistency.

**Quality Contracts:**
- **Docs‑first**: `docs/ai/**` and the Feature Registry are the substrate AI agents use to reason deterministically.
- **Contracts‑first**: APIs, events, and schemas defined upfront with explicit compatibility rules and error models.
- **Acceptance‑driven**: Each phase and task has explicit verification commands and acceptance criteria.
- **Observability‑ready**: Metric taxonomy and logging/tracing conventions documented to trust outcomes.

**Practical & Safe:**
- **Architecture‑agnostic**: Encode your boundaries (whatever they are) and validation method (Zod, pydantic, Go tags, Bean Validation, etc.).
- **Idempotent and safe**: Always preview planned changes; never overwrite without consent.
- **Prompt-based**: No scripts, dependencies, or build steps — works in any AI tool.

How It Works: The Systematic Process

**Phase 1: Context Gathering (One-Time Setup)**
1. Copy `AgenticFlywheel/` into your repo root
2. Run `AgenticFlywheel/prompts/SYSTEM_BOOTSTRAP.md` in your AI tool
3. Answer interview questions about your architecture, testing, security, observability
4. **Codebase audit** — AI analyzes your repo and discovers existing features:
   - Identifies features by clustering routes, components, services, database schema
   - Presents discovered features for confirmation
   - Choose: backfill all, backfill top 5 critical, or start fresh
   - Non-blocking: backfilling happens after setup if desired
5. Review and approve diffs — the wizard generates:
   - `docs/ai/**` (coding standards, testing, architecture, security, observability, error handling, config management)
   - `docs/templates/AIP/*` (full AIP templates for major features)
   - `docs/templates/AIP-Lite/*` (lightweight templates for small features)
   - `docs/features/REGISTRY.yaml` (feature tracking system)
   - Enhanced agent configs with automatic search & dependency checking
6. **Tutorial** — Create your first real AIP during setup:
   - AI guides you through planning a feature you actually want to build
   - Learn by doing with a real feature, not fictional examples
   - Choose lightweight or full AIP based on complexity
   - End setup with a complete AIP ready to implement

**Phase 2: Planning (Per Feature)**
5. Run `AgenticFlywheel/prompts/AIP_COLLAB.md` or `AIP_NEW.md` to create an AIP packet
6. AI guides you through structured Q&A covering:
   - Objectives, scope, and constraints
   - Contracts (API/events/schemas)
   - Backend and frontend implementation plans
   - Risks and mitigations
   - Observability and acceptance criteria
7. Review and approve — generates complete packet with `CHECKLIST.yaml`, `CONTRACTS.md`, `BACKEND_IMPLEMENTATION.md`, etc.

**Phase 3: Development (Enforced Phases)**
8. AI agent executes tasks from `CHECKLIST.yaml` in order:
   - **Design & Contracts**: Finalize implementation plans
   - **Backend Implementation**: Code + unit/integration tests (required)
   - **Frontend Implementation**: UI/UX + tests (required)
   - **Docs Correction**: Update global docs as needed
   - **Observability & Rollout**: Add metrics, dashboards, runbook
   - **Docs & Handoff**: Update all packet docs, Feature Registry, generate `AGENT_PROMPT.txt` (required)

**Phase 4: Validation & Maintenance**
9. Run `AgenticFlywheel/prompts/CHECKLIST_VALIDATOR.md` to verify structure and completeness
10. Run `AgenticFlywheel/prompts/FEATURES_REGISTRY_UPDATE.md` to keep registry current
11. Use `AGENT_PROMPT.txt` to restart AI sessions with zero context loss

**Result**: Every feature follows the same systematic process. No shortcuts. No skipped steps. Consistent, traceable, maintainable.

How Consistency Is Enforced

**Structural Enforcement:**
- **Required phases**: `CHECKLIST.yaml` templates include mandatory "Backend Implementation", "Frontend Implementation", "Docs & Handoff" phases
- **Required tasks**: Every phase includes explicit test tasks (tests-backend, tests-frontend) that must be marked complete
- **Validation gates**: `CHECKLIST_VALIDATOR.md` checks for required phases, status coherence, and acceptance criteria
- **Registry updates**: Feature Registry must be updated during "Docs & Handoff" — no feature is complete without traceability
- **Dependency tracking**: Features declare dependencies; AI automatically runs impact analysis before modifications

**Transparent Agent Behavior:**
- **Automatic context gathering**: AI agents automatically search Feature Registry and existing AIPs before making changes — you don't trigger this manually
- **Automatic dependency analysis**: When modifying features with dependents, AI checks for breaking changes and proposes coordination — happens transparently
- **Scale guidance baked in**: AI suggests lightweight vs full AIP based on feature complexity — no manual decision needed
- **Pattern discovery**: AI finds similar implementations across AIPs to ensure consistency — automatic, not manual search

**Prompt-Based Guidance:**
- **Structured Q&A**: AIP_COLLAB guides through contracts, risks, acceptance (can't skip sections)
- **Template scaffolding**: Every AIP starts with the same structure (README, CONTRACTS, BACKEND_IMPLEMENTATION, ORCHESTRATION_AND_UI, OBSERVABILITY, RUNBOOK, RISKS)
- **Agent prompt generation**: AGENT_PROMPT.txt created last, synthesizing all packet docs into zero-context instructions
- **Diff-driven approval**: Every change previewed before writing — you see what's enforced

**Documentation Contracts:**
- **Docs-first foundation**: `docs/ai/**` establishes coding standards, testing requirements, security policies that AI agents must follow
- **Acceptance criteria**: Every phase defines success conditions and verification commands
- **Runbook requirements**: RUNBOOK.md must include flags, validation steps, rollback procedures
- **Observability requirements**: OBSERVABILITY.md must define metrics, dashboards, and validation panels

**Result**: AI agents can't "forget" to write tests, skip docs, or deviate from patterns — the framework structure and transparent automation guide them to consistency.

Quick Start
- Copy `AgenticFlywheel/` to repo root.
- Run `AgenticFlywheel/prompts/SYSTEM_BOOTSTRAP.md` in your AI tool:
  - Answer questions about your architecture and stack
  - Review discovered existing features; choose backfill strategy
  - Approve diffs to create `docs/ai/**`, `docs/AIP_FRAMEWORK.md`, `docs/templates/AIP/*`, `docs/templates/aip-lite/*`, and `docs/features/REGISTRY.yaml`
  - Approve enhanced agent configs (automatic search & dependency checking)
  - Create your first real AIP via guided tutorial
- You're done! You have:
  - Complete documentation foundation
  - Your first feature AIP ready to implement
  - AI agent configured to work systematically

Bootstrap Wizard (Interview Topics)
- Architecture: layered/clean/hex/monolith/microservices; your real boundaries and where business logic lives.
- Languages & validation: TS/Zod, Python/pydantic, Go tags, Java Bean Validation, etc.
- Testing: frameworks, coverage targets, negative tests; CI gates and commands.
- Contracts: APIs/events/schema; compatibility and versioning strategy.
- Data: storage engines, migrations, retention; messaging/queues/streams.
- Security & privacy: authn/z model, PII policy, secrets handling, compliance regimes.
- Performance: latency/throughput budgets; perf test plan.
- Observability: metrics taxonomy, tracing, logging; dashboards and alert thresholds.
- Change management: PR standards, docs workflow, release cadence.
- Agent tool presence: Claude, Codex, Cursor — propose config updates or skip.

Generated Docs (Tailored)
- `docs/ai/INDEX.md` — Central navigation (links AIP spec, Feature Registry, packet templates).
- `docs/ai/CODING-STANDARD.md` — Your language/style and error handling norms.
- `docs/ai/TESTING-STANDARDS.md` — Pyramid, coverage, negative tests, CI commands.
- `docs/ai/SECURITY.md` — Validation approach, authz semantics, PII redaction, secrets policy.
- `docs/ai/PLATFORM-ARCHITECTURE.md` — Your architecture shape and boundaries.
- `docs/ai/DATA-ACCESS.md` — Stores, migrations, retention, data safety.
- `docs/ai/API-DOCUMENTATION.md` — Contracts with error model and versioning.
- `docs/ai/PERFORMANCE.md` — Budgets and verification.
- `docs/ai/OBSERVABILITY.md` — Metrics/logging/tracing conventions and quick checks.
- `docs/ai/ERROR-HANDLING.md` — Error classification, retry policies, circuit breakers, fallback strategies.
- `docs/ai/CONFIGURATION-MANAGEMENT.md` — Environment variables, feature flags, secrets management, configuration validation.
- Optional: `DEPLOYMENT.md` — Release processes, rollback procedures, environment management.
- Optional: `DOMAIN-MODELS.md` — Core business entities, relationships, and domain boundaries.
- Optional: `INTERACTION-PATTERNS.md`, `UI-COMPONENTS.md`, `CACHE-POLICY.md` (if applicable).

Feature Registry (First‑Class)
- Purpose: A single, searchable index of features with flags, configs, contracts, metrics, owners, rollout, and linked AIPs.
- Location: `docs/features/REGISTRY.yaml` (created/maintained via prompts).
- Schema (baseline): see `AgenticFlywheel/features/REGISTRY.schema.json`.
- Prompts:
  - Bootstrap: `prompts/FEATURES_REGISTRY_BOOTSTRAP.md`
  - Update: `prompts/FEATURES_REGISTRY_UPDATE.md`
  - Validate: `prompts/FEATURES_REGISTRY_VALIDATE.md`
- AIP tie‑in: every AIP’s “Docs & Handoff” phase must update the Feature Registry entry with flags, contracts path, metrics, compliance, AIP path(s), rollout notes, and `last_updated`.

Create a New AIP
- Run `AgenticFlywheel/prompts/AIP_NEW.md`:
  - Provide feature slug and title; optional context, scope, constraints.
  - Approve diffs to create `docs/Agent Implementation Packets/<slug>/` with standard files.
  - The prompt ensures the "Docs & Handoff" phase exists in `CHECKLIST.yaml`.

Collaborative Design (Optional)
- Run `AgenticFlywheel/prompts/AIP_COLLAB.md` for short Q&A across objectives, scope, architecture, contracts, risks, verification, observability, and phases.
- After confirmation, it emits the packet and prints acceptance and next steps (including a Feature Registry update proposal).

Checklist Validation (Prompt‑Based)
- Use `AgenticFlywheel/prompts/CHECKLIST_VALIDATOR.md`:
- Verifies presence of "Docs & Handoff".
- Checks status coherence (top‑level vs tasks).
- Flags missing acceptance or verification commands.
- Proposes concrete corrections with diffs.

Agent Config Updates (Optional, Non‑Destructive)
- Run `AgenticFlywheel/prompts/AGENTS_CONFIG_TAILOR.md` to propose changes to:
  - Claude: `.claude/PROJECT_PROMPT.md` (docs‑first norms tailored to your stack).
  - Codex: `.codex/agents.yml` context updates to include `docs/**`, packets, and registry paths.
  - Cursor: `.cursor/rules/.cursorrules` additions to prioritize docs‑first and AIP norms.
- Always shows diffs; approve per file.

Safety & Idempotency
- Prompts never write files without explicit approval.
- They detect and respect existing files; you can skip, merge, or replace.
- Link the AIP `CHECKLIST.yaml` and registry diffs in PRs for traceability.

Acceptance Criteria
- `docs/ai/**` exists and reflects your architecture, validation approach, contracts, testing, performance, observability, error handling, and configuration management.
- `docs/AIP_FRAMEWORK.md` links to the framework spec.
- `docs/templates/AIP/*` exists with unmodified templates ready for use.
- `docs/features/REGISTRY.yaml` exists and includes at least one feature linked to its AIP and contracts.
- Prompts function end‑to‑end: bootstrap, new AIP, registry update, and validations.

Maintenance & Continuous Improvement

**Enforce Consistent Patterns:**
- **Always use AIPs**: For any significant feature or change, create an AIP — this enforces the systematic workflow.
- **Follow the checklist**: Use `CHECKLIST.yaml` as the canonical task tracker; mirror status in `CHECKLIST.md` for human readability.
- **Run validators**: Use `CHECKLIST_VALIDATOR.md` and `FEATURES_REGISTRY_VALIDATE.md` before considering a feature complete.
- **Update the registry**: Feature Registry updates are required in the "Docs & Handoff" phase — no exceptions.

**Keep Context Current:**
- **Maintain `docs/ai/**`**: Treat these as normative; when coding standards or architecture change, update them immediately.
- **Generate prompts last**: `AGENT_PROMPT.txt` is synthesized after all packet docs are complete — this ensures zero-context restartability.
- **Link everything**: Ensure Feature Registry entries link to AIPs, AIPs reference contracts, and contracts are discoverable from `docs/ai/INDEX.md`.

**Flywheel Effect:**
- Each completed AIP strengthens your documentation
- Better docs enable faster, more reliable AI collaboration
- More consistent patterns reduce cognitive load and technical debt
- The framework gets more valuable with each feature you build

FAQ

**Why not just use AI normally without a framework?**
Without structure, AI development becomes inconsistent: each feature implemented differently, tests skipped, docs forgotten, context lost. AgenticFlywheel enforces a systematic process through templates and validation gates, ensuring every feature follows the same pattern. The time investment in structure pays dividends in consistency, maintainability, and velocity.

**Does this slow down development?**
Initially, yes — bootstrapping takes 15-30 minutes, and your first AIP takes longer than ad-hoc coding. But the systematic process eliminates rework, prevents technical debt, and makes every subsequent feature faster. By your third feature, you're ahead of ad-hoc AI development. By your tenth, you're 2-3x faster with higher quality.

**What if we skip the "Docs & Handoff" phase to ship faster?**
Don't. That phase is what makes the framework work. Skipping it breaks the flywheel effect: docs drift, the Feature Registry becomes stale, future AI sessions lack context, and you're back to inconsistent development. The systematic process only works if you complete all phases.

**How do you enforce that AI agents follow the process?**
- Structural enforcement: Required phases in `CHECKLIST.yaml` templates
- Validation gates: `CHECKLIST_VALIDATOR.md` checks for required phases and completeness
- Prompt-based guidance: Structured Q&A in AIP_COLLAB ensures nothing gets skipped
- Human oversight: You review and approve all changes via diffs

**Can we adapt this to our existing workflow?**
Yes. The wizard interviews you about your architecture, testing, and processes, then generates tailored docs. If you have existing docs, it proposes merges. If you can't use certain file locations, adapt them. The principles (systematic workflow, required phases, validation gates) are more important than the exact structure.

**We don't use TypeScript or Zod:**
The wizard adapts to your language and validation method (pydantic, Go tags, Bean Validation, etc.).

**We already have docs:**
The wizard proposes merges and links; you can skip any file.

**We can't store tool config files:**
Skip the config step — the framework still works fully.

**Do we need scripts or Node installed?**
No. This framework is prompt‑first and tool‑agnostic.

**What if an AIP is half-done and we stopped working on it?**
Mark it as `abandoned` in both CHECKLIST.yaml and Feature Registry. Use `AgenticFlywheel/prompts/AIP_RECONCILE.md` to document what was completed and clean up. You can always resume later by changing status to `in_progress`.

**What if code has changed but AIP hasn't been updated?**
Run `AgenticFlywheel/prompts/AIP_RECONCILE.md` to compare code vs docs. It will identify drift and help you update the AIP to match reality or flag code that violates the original contracts. This is especially useful for legacy features or after rapid changes.

**How do we handle incomplete features?**
Use status `incomplete` in both CHECKLIST.yaml and Feature Registry. This indicates partial implementation that may be resumed. Run `AIP_RECONCILE.md` to document what's done vs what's pending, update docs to reflect reality, and create a plan for completion or removal.

Troubleshooting
- Too many proposed changes: Use the diff view to reject or narrow scope; rerun with a smaller target (e.g., start with `INDEX.md`, AIP templates, and Feature Registry bootstrap).
- Mixed architecture: Encode boundaries you actually use; avoid aspirational docs — agents need current truth.
- Conflicting PR feedback: Link the AIP `CHECKLIST.yaml`, `CONTRACTS.md`, and the Feature Registry entry to anchor decisions.

