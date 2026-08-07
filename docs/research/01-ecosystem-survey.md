# Research Brief 01 — Agent Framework Ecosystem Survey

> Date: 2026-08-07 · Method: parallel research task (official docs + HN/GitHub criticism, sources verified) · Purpose: differentiation positioning for WAM

## What each framework persists / plans / verifies

| Framework | Cross-session state | Goals & planning | Verification | Criticism |
|---|---|---|---|---|
| LangGraph | Checkpoints (thread-scoped short-term) + Store (cross-thread long-term); thread_id resumes | None built-in; custom nodes | None; interrupt for human-in-the-loop | Abstraction bloat, breaking changes (HN 43468435) |
| AutoGen | Conversation history only | None (GroupChat); no goal model | None | 0.4 self-admits experimental; merged into MS Agent Framework |
| CrewAI | Short/long/entity/context memory; LLM infers importance on save | role/goal; AgentPlanner replans per round when planning=True | None | "Abstraction soup", production debugging nightmare (HN 47132187) |
| OpenAI Agents SDK | Persistable sessions (SQLite/Redis/Mongo) = message history + context vars; no project-level state | Instructions + handoffs; no planning | Guardrails validate output schema; no step-level verification | "Better to hand-write", hard to debug (HN 44353964) |
| Letta/MemGPT | Explicit memory hierarchy: memory blocks (human/persona) + archival/recall; cross-session; git-versioned MemFS + "agent dreaming" | None; model self-edits memory | None | Self-editing memory ≈ unreliable instruction execution (HN 37901902); V1 SDK deprecated |
| Claude Code | Nothing per-session; CLAUDE.md + auto-memory (model-written notes) | None; self-made todos | None — official docs admit "looks done" without runnable checks is an illusion | Unusable on complex engineering, CLAUDE.md bloat (GitHub issue #42796) |
| Aider | Git commits (every edit, rollback-able) + session history; no cross-session memory | architect mode = planner/implementer dual model | Runs tests + lint; no semantic verification | No project-level memory |

## Ceiling analysis — where they all break for multi-session complex projects

- **No human-readable shared state**: memory is kv checkpoints (LangGraph), prompt files (CLAUDE.md), or model self-written notes (Letta). Nobody offers one human-readable, human-editable, cross-session source of truth.
- **No weight judgment**: only CrewAI infers importance at save time; no critical-path/enhancement/noise tiers anywhere.
- **No verification**: industry-wide gap — Anthropic's own docs admit unverified "done" is an illusion.
- **Planning artifacts are one-shot**: CrewAI replans per round; Aider architect; no living goal object with progress.
- **Positioning implication**: do not build the 100th orchestration framework. WAM = shared state + six-step protocol.

## Open questions

- State schema that is machine-executable AND human-editable?
- Priority: human-annotated, model-inferred, or protocol-derived?
- Cost/granularity trade-off of step-level verification?
- Embed into or replace existing workflows (Claude Code / Aider)?

## Sources

LangChain persistence docs; Microsoft Agent Framework migration guide; CrewAI memory docs; OpenAI Agents SDK sessions docs; Letta concepts docs; Claude Code memory docs; Aider git docs; HN threads 43468435 / 47132187 / 44353964 / 37901902; Claude Code issue #42796.
