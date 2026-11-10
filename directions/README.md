# Directions — Unverified Development Zones

> Established 2026-08-07. Governance rule: nothing unverified enters the official structure.
>
> **2026-10-09 annotation.** All four directions remain OPEN and unverified; none has produced a vertical slice yet (see `workspace/log.md`, 2026-08-15: eight days with zero recorded execution). Ordering changed: `docs/06-development-plan.md` §1 places the minimal verifiable core (stage 2) ahead of the agent-plugin and weight-first slices. Two facts were checked and did not hold up — "Hermes Agent is the platform this project is developed on" (no such directory under `D:/github projects/`; DSH is the verified mechanism) and "WAM is built on Sponge" (zero occurrences in this repo, while `D:/github projects/Sponge/研发/03_架构与生态位.md` claims it). Both are recorded in `docs/07-decision-register.md` X-01, X-02, OQ-09, OQ-10 and need the author's decision.

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

- `global-route/` — (author) WAM as a global orchestration entity, inspired by Hermes Agent. Critical path. **Slicing: minimal resume experiment (no full engine).**
- `substrate/` — WAM as a state substrate: library + CLI for the state model, no agent of its own. Critical path. **Slicing: stage 1 — wam CLI + evidence checker (verify-gate merged in).**
- `agent-plugin/` — WAM embedded in an existing agent (skill / MCP) implementing the six-step protocol. Critical path. **Slicing: stage 2 — Hermes skill, one week on the WAM repo.**
- `weight-first/` — lead with the original contribution: goal DAG + critical-path computation + unknown registry. Critical path. **Slicing: stage 3 — goal DAG + critical-path prototype.**
- `shared-context/` — (author, 2026-10-27) WAM's collaboration substrate is a **layered shared context with explicit per-agent exploration boundaries**, not inter-agent messages; default scheduling runs a single global agent (Miracle Agent) that may call several tool-registry entities at once. Critical path (for the architecture after the MVP). **Slicing: a one-session, three-stage scope-conflict experiment — not a service.** Nearest neighbours to read first: SE-Blackboard (IEEE 11527206), LLM blackboard (NeurIPS 2026).

## Deferred (not yet opened as directions)

- `verify-gate/` — evidence checker for the Verify step — merged into the substrate slice (stage 1); reconsider as its own direction if it outgrows the CLI.
- `state-v2/` — state model evolution from memory research (CoALA layering, reflection triggers) — deferred until substrate exposes real problems.

## Archived

- `architecture/` — superseded 2026-08-07 by the four competing directions above.
