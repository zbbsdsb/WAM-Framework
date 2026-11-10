# WAM — Wait a Minute

An agent framework built on a single conviction: **before answering, understand the situation.**

## Why "Wait a Minute"

The name is not about rate-limiting an AI's responses. It is an existential posture.

When faced with a genuinely daunting task, WAM does not rush to produce a plausible-sounding answer. It stops — and works through the problem together with you, one step at a time. This is not caution for its own sake; it is respect for complexity.

## The Problem

Today's agent frameworks reduce collaboration to an endless one-question-one-answer loop. They answer *within* the conversation, but never *beyond* it. This leaves four structural gaps:

1. **Constructiveness** — responses react to the latest message; they do not build toward a goal.
2. **Continuity** — every conversation starts from zero; the moment a rhythm is broken, complex projects collapse.
3. **Verifiability** — output sounds reasonable but does not hold up under scrutiny.
4. **Weight judgment** — the agent cannot tell what matters, so it treats everything as equally important.

Beneath all four lies a deeper failure: **state desync**. The human carries context, intent, and the weight of every decision; the AI carries none of it. In human teams, misalignment is repaired by talking it out. In AI collaboration, a single interruption is enough to invalidate the rest of the project.

This is not a prompt-engineering problem. It is a structural defect of the framework.

## The Philosophy

**The 1% foundation.** We are not building a 100% shell — one of those all-capable frameworks that does nothing deeply. WAM builds only the bottom 1% of the foundation, and builds it solidly: how state stays synchronized, how goals are constructed, how progress survives, how uncertainty is managed.

**The sage and the doer.** The *sage* sees the whole situation, not the current sentence; it traverses possibilities, senses the boundary between what we know and what we don't, and is sensitive to weight. The *doer* takes only verifiable steps: push forward when possible, admit when not — no bluffing, no forcing.

Whether the underlying system is one agent or many is an implementation detail. However many agents run beneath, the user should face a single, unified, constructive collaborator.

**Principles.** Slow down to speed up · No bluffing · A directional 1% · Weight-sensitive · Honest · Stay in sync.

## Status

**Zero executable code.** What exists is a design baseline, a governance mechanism, and an explicit list of open questions — every design document states which parts have no carrier yet.

Two places hold the current truth, and this file will not duplicate them:

| You want | Go to |
|---|---|
| Where the project stands right now (known / unknown / unknown-unknowns) | [`workspace/state.md`](workspace/state.md) |
| What happens this week, and what has to be true by when | [`docs/development/roadmap.md`](docs/development/roadmap.md) |

> This README used to carry its own status section. By 2026-11-10 there were four copies of "where the project stands" and two of them were wrong. The fix was structural: one home each, everything else points there.

## Start here

| You are | Read |
|---|---|
| New to WAM | [`docs/vision.md`](docs/vision.md) → [`docs/decisions/register.md`](docs/decisions/register.md) (only the C and OQ sections) → [`docs/development/scope.md`](docs/development/scope.md) §4 |
| About to write code | [`docs/development/roadmap.md`](docs/development/roadmap.md) → [`docs/specifications/execution-contract.md`](docs/specifications/execution-contract.md) → [`docs/development/mvp-plan.md`](docs/development/mvp-plan.md) |
| Judging whether a claim holds | [`docs/decisions/register.md`](docs/decisions/register.md) → [`docs/specifications/acceptance.md`](docs/specifications/acceptance.md) |
| Contributing material | [`CONTRIBUTING.md`](CONTRIBUTING.md) — where each kind of content belongs |
| Exploring a *different* overall architecture | [`paths/`](paths/) — the path registry; rules in [`PATH_GOVERNANCE.md`](PATH_GOVERNANCE.md) |

**A note on what `docs/` means here.** `docs/` holds only what has been *adopted*. Explorations of a different overall architecture live in `paths/` — including `octsix`, the path the author is currently working in. **No path is canonical by default**, and the concepts of one path do not become WAM's concepts because they are in the current one.

The full documentation map lives in **[`docs/README.md`](docs/README.md)**. Everything outside `docs/` — research, proposals, experiments, the paper library, project state, the public site — is described there too; this file intentionally does not repeat it.

**Public site** (bilingual, atompunk): <https://zbbsdsb.github.io/WAM-Framework/> · source: [`site/`](site/)

---

*The documents in `docs/` record the current thinking. They are not a final definition, and they are explicit about which parts have no implementation. That openness is part of WAM itself.*

## Author

**ceaserzhao (zbbsdsb)**
