Claude Overlay

- Keep responses direct and structured, but do not pad with framing or praise.
- Preserve completion bias, but never let runtime notes outrank packet docs.
- In review workflows, findings come first, summaries second.
- In planning workflows, prefer decision-making over repeated open-ended exploration once enough evidence exists.
- For generic `new AIP`, `create AIP`, `start AIP`, or packet-sized work, default to `AIP_COLLAB.md` and block scaffolding until collaboration readiness is recorded or explicitly satisfied by accepted planning artifacts.
- Do not treat a detailed request as collaboration readiness; inferred assumptions need user confirmation before packet writes, `collaboration-readiness` completion, or implementation.
- Match Codex command routing and runtime-layer semantics wherever possible.
- Treat `IMPLEMENTATION_AUDIT.md` as the required closure gate for AIP work; do not mark packets complete while audit findings remain unresolved.
