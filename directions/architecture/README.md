# Direction: Architecture

> Status: OPEN · Weight: critical path · Opened: 2026-08-07

## Hypothesis

WAM's architecture can be specified as "shared state + six-step protocol" running as a thin runtime, and the first vertical slice of it can be demonstrated within one milestone.

## What would falsify this

The first vertical slice cannot be demoed without inventing components beyond the state model + protocol (e.g., needing multi-agent orchestration or a vector store to do anything useful).

## Inputs (evidence)

- `docs/research/01-ecosystem-survey.md` — no framework offers human-readable shared state; verification gap is industry-wide
- `docs/research/02-memory-and-state.md` — layering is consensus; human-shared state is unresearched
- `docs/research/03-unknown-and-weight.md` — CPM-in-agents is unresearched; unknown-unknown detection unsolved

## Work log

- 2026-08-07: survey complete; design conversation pending (3 questions: who it's for / first demo / v1 boundaries)

## Next step

Design conversation → proposal draft (`proposal.md` in this folder) → first vertical slice → promotion to `docs/02-architecture.md`.
