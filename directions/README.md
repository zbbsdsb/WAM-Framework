# Directions — Unverified Development Zones

> Established 2026-08-07. Governance rule: nothing unverified enters the official structure.

## Why

WAM's own philosophy: no bluffing, verification before commitment. To keep the project from drifting off course, all *speculative* development happens here first. A direction is a hypothesis about where WAM should go — it earns its place in the official structure only by being verified.

## Three tiers of material

| Tier | Where it lives | Trust level |
|---|---|---|
| Evidence | `docs/research/` | Sourced facts, verifiable — permanent |
| Proposals | `directions/<name>/` | Ideas, drafts, designs, prototypes — NOT trusted |
| Decisions & constitutions | `docs/01-foundation.md`, `workspace/decisions.md`, `workspace/goals.md` | Verified — official |

## Lifecycle of a direction

1. **Open** — create `directions/<name>/README.md` with: a one-line hypothesis, a weight tier (critical path / enhancement / noise), and what would falsify it.
2. **Work** — free-form exploration inside the folder: notes, prototypes, drafts. Low ceremony by design. Nothing here is a commitment.
3. **Verify** — the direction's claims must be demonstrated: working code with output, a demo, test results, sources for factual claims.
4. **Promote or archive** — promotion requires ALL of:
   - a decision recorded in `workspace/decisions.md` (reason, alternatives, weight judgment);
   - evidence cited (artifact path / command output / test result);
   - the artifact moved into its official home (`docs/`, code tree, etc.);
   - the direction folder moved to `directions/archive/`.

   A direction that fails verification is archived the same way — with the failure recorded. Archiving is not failure-shaming; it is the project's memory of what was tried and why.

## Current directions

- `global-route/` — (author) WAM as a global orchestration entity, inspired by Hermes Agent. Critical path.
- `substrate/` — WAM as a state substrate: library + CLI for the state model, no agent of its own. Critical path.
- `agent-plugin/` — WAM embedded in an existing agent (skill / MCP) implementing the six-step protocol. Critical path.
- `weight-first/` — lead with the original contribution: goal DAG + critical-path computation + unknown registry. Critical path.

## Archived

- `architecture/` — superseded 2026-08-07 by the four competing directions above.
