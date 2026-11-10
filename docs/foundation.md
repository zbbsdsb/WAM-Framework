# Foundation: The State Model and Collaboration Protocol

> Version: M0 · 2026-08-06 · Status: In effect (subject to revision through practice)
>
> **2026-10-09 note.** This document remains the currently-in-force constitution: the four-file state model and the six-step protocol are M0's delivered output and are still in effect. The design baseline in `docs/vision.md`–`docs/specifications/acceptance.md` **refines** it in three places — (1) Intent must be read, not just goals and progress; (2) "Judge" means choosing what *type* of step to take, including waiting or stopping; (3) "Verify" separates *obtaining evidence* from *evidence meeting the acceptance condition*. See [`docs/architecture.md` §2](architecture.md) for the mapping table. Everything else in this document stands unchanged.

## Thesis

The foundation of WAM is not code, but the **state shared between human and AI**.

The four fundamental questions raised in idea.md — how state is synchronized, how goals are constructed, how progress continues, how uncertainty is managed — must be answered before any runtime, any language, any number of agents. This document is the minimal version of that answer.

## The State Model: Four Files

All collaboration state lives under `workspace/` at the repository root, versioned as Markdown + git (both human and AI can read and write directly; every step can be diffed and rolled back):

| File | Question it answers | Deficiency in idea.md |
|---|---|---|
| `workspace/state.md` | How is state synchronized? What is the current situation? | State desync |
| `workspace/goals.md` | How are goals constructed? What matters? | Constructiveness + weight judgment |
| `workspace/log.md` | How does progress continue? | Continuity |
| `workspace/decisions.md` | How are judgments recorded? | Weight judgment + pragmatism |

Hard rules:

1. **Read state.md and goals.md at the start of every session; write log.md at the end** (even one line).
2. **Every "done" must carry evidence**: artifact path, command output, test result. No evidence = not done.
3. **Every goal must carry one of three weight tiers**: critical path / enhancement / noise. Noise is not elaborated, not scheduled.
4. **Unknown-unknowns must be explicitly listed**, never feigned knowledge.

## The Collaboration Protocol: A Six-Step Loop

Every collaboration (whether initiated by human or AI) follows:

1. **Read** — Load state.md (situation), goals.md (goals and weights), and the tail of log.md (progress).
2. **Wait** — Wait a Minute: is the goal clear? Is the situation understood? Should this step really be taken?
3. **Judge** — What is the highest-weight step right now? (Critical path first; never do noise.)
4. **Do** — Take exactly one verifiable step.
5. **Verify** — Provide evidence; if infeasible, say so honestly.
6. **Write** — Update state / goals / log / decisions.

## Development Governance: Directions and the Promotion Gate

Established 2026-08-07. To keep the project from drifting off course, the project's own development follows a three-tier structure:

| Tier | Where it lives | Trust level |
|---|---|---|
| Evidence | `research/briefs/` | Sourced facts, verifiable — permanent |
| Proposals | `directions/<name>/` | Ideas, drafts, prototypes — NOT trusted |
| Decisions & constitutions | `docs/` (this file), `workspace/` (decisions.md, goals.md) | Verified — official |

Hard rule: **nothing moves from `directions/` into the official structure without passing the promotion gate** — a decision recorded in `workspace/decisions.md`, evidence cited (artifact path / command output / test result), and the artifact relocated, with the direction folder archived to `directions/archive/`.

See `directions/README.md` for the full lifecycle.

## Boundaries

- This document is not the final definition. When practice exposes problems, revise the protocol here first, then the implementation.
- Tech stack, number of agents, runtime architecture: implementation details, all deferred.

## Design baseline (added 2026-10-09)

The M0 foundation above answers *how state is shared*. It does not answer *what judgment means, how a Move is bounded, or what evidence is worth*. Those are now specified separately:

| Question | Answered in |
|---|---|
| What problem WAM solves; the five core concepts; the seven principles | [`docs/vision.md`](vision.md) |
| The core loop; component responsibilities; persistent record; Human Absent Mode; concept-vs-module boundaries | [`docs/architecture.md`](architecture.md) |
| What Situation must express; fact / assumption / unknown; Move lifecycle; the five-level evidence ladder | [`docs/specifications/state-and-evidence.md`](specifications/state-and-evidence.md) |
| The minimal verifiable core, stage gates, what is deferred, what blocks development | [`docs/development/mvp-plan.md`](development/mvp-plan.md) |
| Which decisions are established / baseline / hypothesis / open | [`docs/decisions/register.md`](decisions/register.md) |
| Four design-validation scenarios + 10 acceptance criteria | [`docs/specifications/acceptance.md`](specifications/acceptance.md) |

Two things the M0 foundation does **not** provide, and which the MVP must build:

1. **A carrier for Intent.** `goals.md` holds a goal tree, not the user's intent or authorization boundary. This is the largest open gap (`docs/decisions/register.md` OQ-01).
2. **A carrier for the Judgment process.** `decisions.md` records what was decided; it does not record how the judgment was reached, so judgment traceability cannot be checked.

**Implementation status: zero.** This repository currently contains no executable code. The four Markdown files under `workspace/` are maintained by hand and carry the protocol, but nothing validates them yet.
