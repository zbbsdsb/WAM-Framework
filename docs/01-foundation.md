# Foundation: The State Model and Collaboration Protocol

> Version: M0 · 2026-08-06 · Status: In effect (subject to revision through practice)

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

## Boundaries

- This document is not the final definition. When practice exposes problems, revise the protocol here first, then the implementation.
- Tech stack, number of agents, runtime architecture: implementation details, all deferred.
