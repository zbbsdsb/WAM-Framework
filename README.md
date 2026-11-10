# WAM — Wait a Minute

An agent framework built on a single conviction: **before answering, understand the situation.**

## Why "Wait a Minute"

The name is not about rate-limiting an AI's responses. It is an existential posture.

When faced with a genuinely daunting task, WAM does not rush to produce a plausible-sounding answer. It stops — and works through the problem together with you, one step at a time. This is not caution for its own sake; it is respect for complexity.

## The Problem

Today's agent frameworks reduce collaboration to an endless one-question-one-answer loop. They answer *within* the conversation, but never *beyond* it. This leaves four structural gaps:

1. **Constructiveness** — Responses react to the latest message; they do not build toward a goal. The agent responds; it does not construct.
2. **Continuity** — Every conversation starts from zero. The moment a rhythm is broken, complex projects collapse. Humans re-align through communication; agents simply lose the thread.
3. **Verifiability** — Output sounds reasonable but does not hold up under scrutiny. Even a task as basic as "check the paper" cannot be trusted, let alone the work of turning unknown-unknowns into known-unknowns during complex design.
4. **Weight judgment** — The agent cannot tell what matters. In a complex project, some work is on the critical path, some is nice-to-have, some is noise — yet the framework offers no tool for judging importance, so the agent treats everything as equally important and grasps at everything.

Beneath all four lies a deeper failure: **state desync**. The human carries context, intent, and the weight of every decision; the AI carries none of it. In human teams, misalignment is repaired by talking it out. In AI collaboration, a single interruption is enough to invalidate the rest of the project.

This is not a prompt-engineering problem. It is a structural defect of the framework.

## The Philosophy

### The 1% Foundation

We are not building a 100% shell — one of those all-capable frameworks that does nothing deeply. WAM builds only the bottom 1% of the foundation, and builds it solidly. That foundation is not a feature list; it is a fundamental answer to how an agent collaborates with a human: how state stays synchronized, how goals are constructed, how progress survives, how uncertainty is managed.

### The Sage and the Doer

WAM's architecture vision is a **sage** with the hands of a **doer**.

- The **sage** sees the whole situation, not the current sentence. It traverses possibilities instead of taking preset shortcuts. It knows when to be fast and when to be slow. It senses the boundary between what we know and what we don't. It is sensitive to weight.
- The **doer** takes only verifiable steps. It is pragmatic: push forward when possible, admit when not — no bluffing, no forcing. It focuses on the most important 1% and leaves continuable progress behind, never an empty promise.

Whether the underlying system is one agent or many is an implementation detail. However many agents run beneath, the user should face a single, unified, constructive collaborator.

### Principles

- **Slow down to speed up.** Establish the state before taking the next step.
- **No bluffing.** Face real difficulty by acknowledging it — then work through it together.
- **A directional 1%.** Every step moves toward the goal, however small.
- **Weight-sensitive.** Hold the critical path; ignore the noise.
- **Honest.** If it works, push. If it doesn't, say so. Honesty beats polish.
- **Stay in sync.** Keeping the agent and the human aligned — to the extent that communication allows — is the framework's core duty.

## Status

**Current stage: M1 — design convergence, zero implementation code.**

As of 2026-10-09 this repository contains **no executable implementation** — 29 tracked files, all Markdown / HTML / CSS / YAML. What exists is a converged design baseline, a governance mechanism, and a set of explicitly-marked open questions.

**As of 2026-10-28** the implementation count is still zero, and that is now the project's main risk rather than a state to be described. Four things were added: a **goal taxonomy** ([`docs/09`](docs/09-goal-taxonomy.md), which derives the MVP scope from typed cells instead of discussion), a **nine-week roadmap to 2027-01-01** ([`docs/10`](docs/10-rd-roadmap-2027.md), with per-week exit conditions and a fixed cut order), an **external-assets review** ([`docs/11`](docs/11-external-assets.md), every claim graded A/B/C by how much of the source was actually read), and a fifth direction ([`directions/shared-context/`](directions/shared-context/README.md), the author's layered-shared-context / single-global-agent thesis). One previously load-bearing technical choice was **falsified by probing**: codex-cli is logged in but `api.openai.com` is geo-blocked from this network, so it cannot be the first executor (`docs/07` X-10 → B-15).

| Stage | What exists | Evidence |
|---|---|---|
| **M0 — Foundation** (complete) | Shared state model + collaboration protocol | [docs/01-foundation.md](docs/01-foundation.md) · [`workspace/`](workspace/) |
| **M1 — Design convergence** (current) | Five core concepts, core loop, MVP plan, decision register, acceptance criteria | [docs/03](docs/03-vision-and-concepts.md) · [docs/04](docs/04-architecture.md) · [docs/05](docs/05-state-move-evidence.md) · [docs/06](docs/06-development-plan.md) · [docs/07](docs/07-decision-register.md) · [docs/08](docs/08-scenarios-and-acceptance.md) |
| **Implementation** | Not started. The MVP's verifiable core is defined but not built. | [docs/06-development-plan.md](docs/06-development-plan.md) |

**Nothing in `docs/` describes a working system.** Those documents state design intent and are explicit about which parts have no carrier yet.

## Documentation map

| Document | Answers | Read it when |
|---|---|---|
| [`idea.md`](idea.md) | Why this project exists (philosophy, original wording) | You want the source of truth on intent |
| [`docs/01-foundation.md`](docs/01-foundation.md) | The M0 state model + six-step protocol + governance tiers | You need the currently-in-force rules |
| [`docs/02-dashboard-plan.md`](docs/02-dashboard-plan.md) | The dashboard effort's plan (staged P1–P4) | You're touching dashboard work |
| [`docs/03-vision-and-concepts.md`](docs/03-vision-and-concepts.md) | What problem WAM solves; Intent / Situation / Judgment / Move / Evidence; the seven principles | You're new to WAM, or need the vocabulary |
| [`docs/04-architecture.md`](docs/04-architecture.md) | The core loop, component responsibilities, persistent record, execution boundary, Human Absent Mode | You want the shape of the system |
| [`docs/05-state-move-evidence.md`](docs/05-state-move-evidence.md) | What Situation must express; fact vs assumption vs unknown; Move lifecycle; evidence ladder | You're designing data structures or validation |
| [`docs/06-development-plan.md`](docs/06-development-plan.md) | **The engineering plan** — MVP scope (must / minimal / deferred), the three implementation choices with their evidence, 6 interfaces, `.wam/state.json` schema, Move lifecycle, 15 tasks, **7 execution batches with exit conditions**, 12 acceptance cases, and the decisions awaiting your review | You're about to write code — **start here** |
| [`docs/07-decision-register.md`](docs/07-decision-register.md) | Which decisions are established / baseline / hypothesis / open | You need to know how settled something is |
| [`docs/08-scenarios-and-acceptance.md`](docs/08-scenarios-and-acceptance.md) | Four design-validation scenarios + 10 acceptance criteria | You want to test whether WAM holds up |
| [`docs/09-goal-taxonomy.md`](docs/09-goal-taxonomy.md) | **What we promise vs what we hope** — three axes (responsibility layer × commitment type × evidence form), 35 cells, the MVP cut derived from cells | You are about to add, defer, or argue about a scope item |
| [`docs/10-rd-roadmap-2027.md`](docs/10-rd-roadmap-2027.md) | **The nine weeks to 2027-01-01** — per-week exit conditions, three blocking decisions, a fixed cut order, and what counts as success | You want to know what to do this week |
| [`docs/11-external-assets.md`](docs/11-external-assets.md) | Outside work that may help, graded A/B/C by how much was actually read, each with an adopt/adapt/defer/reject verdict and its cost | You are considering borrowing an idea |
| [`directions/`](directions/) | Five competing directions (unverified proposals) | You want to know what's being considered |
| [`experiments/`](experiments/) | Executable verification tracks, staged via DSH agent presets | You're running a verification |
| [`reference/`](reference/) | Weighted library of borrowed papers + the borrow-to-R&D workflow | You're considering adopting an idea from outside |

**Start here if you are a new contributor:** `docs/03` → `docs/07` → `docs/06`.

**Start here if you are about to implement:** `docs/06` + `docs/10`. `docs/06` is self-contained — it carries the interface contracts, the data schema, the task list with dependencies, and the phase gates. `docs/10` turns it into nine weeks with exit conditions and a fixed cut order. Read `docs/03` §3 for why the design is shaped this way, and `docs/09` §4 before adding anything to the scope.

**Public site** (bilingual, atompunk): <https://zbbsdsb.github.io/WAM-Framework/> · source: [`site/`](site/)

---

*The design documents in `docs/` record the current thinking. They are not a final definition, and they are explicit about which parts have no implementation. That openness is part of WAM itself.*

## Author

**ceaserzhao (zbbsdsb)**
