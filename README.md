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

**M0 — Foundation.** A shared state model and collaboration protocol. See [docs/01-foundation.md](docs/01-foundation.md).

The collaboration state — read at the start of every session, written at the end — lives in [`workspace/`](workspace/).

**Public site** (bilingual, atompunk): <https://zbbsdsb.github.io/WAM-Framework/> · source: [`site/`](site/)

---

*This document records the core ideas of WAM. It is not the final definition; the ideas may be revised, extended, or overturned as the architecture progresses. That openness is part of WAM itself.*

## Author

**ceaserzhao (zbbsdsb)**
