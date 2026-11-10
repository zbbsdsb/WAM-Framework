# Directions — Unverified Development Zones

> Established 2026-08-07. Governance rule: nothing unverified enters the official structure.
>
> **2026-11-10 annotation — a third exit was added: `parked`.** Four of the five directions have had no work since 2026-08-07 and no experiment; none was falsified. The old two-exit gate (promote / archive) forced them to sit on `OPEN` forever, and archiving them would have asserted a failure that never happened. `parked` is the honest state: *no evidence either way, not being pursued, and here is what would reopen it.* Status per folder is now recorded in each direction's own README and listed below.
>
> **2026-10-09 annotation.** All four directions remain OPEN and unverified; none has produced a vertical slice yet (see `workspace/log.md`, 2026-08-15: eight days with zero recorded execution). Ordering changed: `docs/development/mvp-plan.md` §1 places the minimal verifiable core (stage 2) ahead of the agent-plugin and weight-first slices. Two facts were checked and did not hold up — "Hermes Agent is the platform this project is developed on" (no such directory under `D:/github projects/`; DSH is the verified mechanism) and "WAM is built on Sponge" (zero occurrences in this repo, while `D:/github projects/Sponge/研发/03_架构与生态位.md` claims it). Both are recorded in `docs/decisions/register.md` X-01, X-02, OQ-09, OQ-10 and need the author's decision.

## Why

WAM's own philosophy: no bluffing, verification before commitment. To keep the project from drifting off course, all *speculative* development happens here first. A direction is a hypothesis about where WAM should go — it earns its place in the official structure only by being verified.

## Three tiers of material

| Tier | Where it lives | Trust level |
|---|---|---|
| Evidence | `research/briefs/` | Sourced facts, verifiable — permanent |
| Proposals | `directions/<name>/` | Ideas, drafts, designs, prototypes — NOT trusted |
| Decisions & constitutions | `docs/foundation.md`, `workspace/decisions.md`, `workspace/goals.md` | Verified — official |

## Lifecycle of a direction

1. **Open** — create `directions/<name>/README.md` with: a one-line hypothesis, a weight tier (critical path / enhancement / noise), and what would falsify it.
2. **Work** — free-form exploration inside the folder: notes, prototypes, drafts. Low ceremony by design. Nothing here is a commitment.
3. **Verify** — the direction's claims must be demonstrated: working code with output, a demo, test results, sources for factual claims.
4. **Three exits** — a direction ends in exactly one of them, and it must say which:
   - **PROMOTED** — requires ALL of: a decision recorded in `workspace/decisions.md` (reason, alternatives, weight judgment); evidence cited (artifact path / command output / test result); the artifact moved into its official home (`docs/`, code tree, etc.); the folder moved to `directions/archive/`.
   - **ARCHIVED** — verification failed. Archive it the same way, with the failure recorded. Archiving is not failure-shaming; it is the project's memory of what was tried and why.
   - **PARKED** — no evidence either way, and not being pursued now. Requires: one line stating **what would unpark it** (a decision, a dependency, an experiment result) and **who is waiting on what**. Parked is not a verdict — it is a schedule. A parked direction that nobody can name an unlock condition for should be archived instead.

   **Only `ARCHIVED` may claim a direction was wrong.** Parking is the default for "not now", and the four 2026-08-07 directions are parked on exactly that basis (none was tested, none was falsified).

## Current directions

Status is a field, not a folder. `ACTIVE` = being worked on now. `PARKED` = no evidence either way, not being pursued, unlock condition stated. Folders do not move on parking — the reference count (117 links into `directions/`) makes moving them pure cost, and the status line is what a reader actually needs.

| Direction | Status | What it is | Unlock condition (what would unpark it) |
|---|---|---|---|
| `shared-context/` | **ACTIVE** | (author, 2026-10-27) Layered shared context with explicit per-agent exploration boundaries; default scheduling = one Miracle Agent calling concurrent tool entities | — (next step is its one-session scope-conflict experiment; when it runs, the run lives in `experiments/shared-context-scope-conflict/`) |
| `global-route/` | **PARKED** | WAM as a single global orchestration entity; cross-session resume (the "reverse machine") | Absorbed: resume → `docs/development/mvp-plan.md` §3.2 (MVP capability 8); "single global entity" → `shared-context/` §5. Unpark if the resume capability proves insufficient **or** the shared-context experiment contradicts the single-judgment-source claim |
| `substrate/` | **PARKED** | State substrate: library + CLI for the state model, no agent of its own | Its first cut **is** `docs/development/roadmap.md` W1 (skeleton + StateRepository). Unpark as a direction only if the CLI outgrows the loop (e.g. dashboard `state check` returns) |
| `agent-plugin/` | **PARKED — conflict unresolved** | WAM embedded in a host agent (skill / MCP) implementing the protocol | Blocked by an unresolved design conflict: `shared-context/` §8 says WAM keeps assigning scope, the host agent only executes — if that cannot hold, the two are mutually exclusive. Unpark on the author's decision about who assigns `scope` |
| `weight-first/` | **PARKED — rejected for the MVP, not falsified** | Lead with the original contribution: goal DAG + critical-path computation + unknown registry | Rejected for the MVP by `docs/decisions/register.md` H-04 (`dependency structure ≠ importance`) and excluded in `docs/development/roadmap.md` §7. Unpark when flat `goals.md` demonstrably fails at retrieval/priority — i.e. when the §7 reopen condition is met |

## Deferred (not yet opened as directions)

- `verify-gate/` — evidence checker for the Verify step — merged into the substrate slice (stage 1); reconsider as its own direction if it outgrows the CLI.
- `state-v2/` — state model evolution from memory research (CoALA layering, reflection triggers) — deferred until substrate exposes real problems.

## Archived

- `architecture/` — superseded 2026-08-07 by the four competing directions above.
