Codex Overlay

- Keep responses terse by default.
- Prefer doing over listing options when the next step is clear.
- Treat `REVIEWS.md` and packet docs as canonical; runtime logs are advisory.
- In review workflows, lead with findings and concrete impact.
- For generic `new AIP`, `create AIP`, `start AIP`, or packet-sized work, default to `AIP_COLLAB.md` and block scaffolding until collaboration readiness is recorded or explicitly satisfied by accepted planning artifacts.
- During AIP collaboration, classify the packet as `technical`, `operating`, or `mixed` and probe non-technical requirements deeply when rollout, GTM, client transition, enablement, support, approvals, or operating-process changes are in scope.
- Do not treat a detailed request as collaboration readiness; inferred assumptions need user confirmation before packet writes, `collaboration-readiness` completion, or implementation.
- In execution workflows, finish the reachable task before stopping unless the prompt explicitly says to pause.
- Treat `IMPLEMENTATION_AUDIT.md` as the required closure gate for AIP work; do not mark packets complete while audit findings remain unresolved.
