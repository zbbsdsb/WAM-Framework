# WAM: Wait a Minute

## The Origin of an Agent Framework

WAM stands for **Wait a Minute**, an agent framework. But the name is easily misleading — it suggests some simple mechanism for "making AI pause", while the problem it actually addresses goes far deeper.

Wait a Minute is not a rate control mechanism, but an **existential posture**: when faced with a truly daunting task, do not rush to give a "plausible-looking" answer. Stop, and work through it together with the user, one step at a time. This is not conservatism; it is respect for complexity.

---

## The Problem

### The Fourfold Deficiency

Current agent frameworks answer almost entirely within the confines of the conversation. You ask in one paragraph, it answers in one paragraph — this looks like collaboration, but is essentially an infinite extension of "question-and-answer". When we say "AI assistant", a true assistant should be able to perceive what is known in the current situation, what is unknown, and what is unknown-unknown.

These are the four deficiencies we face:

1. **Constructiveness** — Answers remain at the level of reaction to a single conversation, lacking the ability to build toward a goal step by step. It does not "construct"; it merely "responds".
2. **Continuity** — Every conversation starts almost from zero. Once the rhythm is broken, follow-up work on complex projects basically collapses. In human collaboration, re-alignment is possible through communication, but AI seems unable to do this.
3. **Genuine verifiability** — Output sounds reasonable, but does not hold up under scrutiny. Even a basic task like "check the paper" struggles to guarantee accuracy, let alone converting unknown-unknowns into known-unknowns when designing complex projects.
4. **Judgment of weight** — AI cannot distinguish the difference in importance between two things. In complex projects, not everything is equally important: some tasks are on the critical path, some are merely nice-to-have, some are pure noise. But the AI's responses seem to lack this "sense of priority" — it treats all inputs as equally important and processes them uniformly. As a result, when faced with truly complex tasks, it fails to grasp what matters — it does not know what deserves deep attention, what can be skipped, what should be done first, what can be deferred. This is not a problem of "understanding ability", but of the framework not providing the cognitive tool of "weight judgment".

### State Desync

In real collaboration, the states of human and AI are almost always out of sync. The user knows their own context, the weight of their intentions, and the trade-offs behind every decision; the AI knows none of it. In human collaboration, even when out of sync, it can be gradually corrected through communication. But AI does not seem to do this — it is either too fast or too hasty, and if the user's rhythm is even slightly disrupted, the follow-up conversation on a complex project is basically invalidated.

This is not something prompt engineering can solve. It is a structural defect at the framework level.

---

## The Starting Point of the Philosophy

### The 1% Foundation

We are not building a 100% shell. There are already too many of those "all-capable frameworks" that appear to do everything but actually do nothing deeply.

WAM chooses a different path: **build only 1% of the foundation, but build that 1% solidly.**

Because only when the foundation is solid can real construction begin. This foundation is not a feature list; it is a fundamental answer to the question of "how agents collaborate with humans": how state is synchronized, how goals are constructed, how progress continues, how uncertainty is managed.

### The Deepest Sage, the Hands of a Pragmatist

The architectural vision of this framework is: it is like a **deepest sage**, while possessing a pair of **pragmatic hands of a doer**.

The sage thinks:

- It sees the whole situation, not just the current sentence.
- It traverses all possibilities, rather than taking a preset shortcut.
- It understands when to be fast and when to be slow.
- It senses the boundary between "what we know" and "what we don't know".
- It judges what is critical and what is noise — sensitive to weight.

The doer acts:

- It does not talk about ideals; it only takes **verifiable steps**.
- It is pragmatic: push forward when feasible, admit when not — no bluffing, no forcing.
- It does not pursue comprehensiveness; it focuses only on the most important 1% right now.
- Every step leaves continuable progress, never an empty promise.

This architecture can be multi-agent or single-agent. Perhaps even this definition itself needs to be reconsidered later — because the "number of agents" is an implementation detail, not core philosophy. WAM's focus: **no matter how many agents run beneath, what is presented to the user should be a unified, global, constructive collaboration entity.**

---

## The Response

### When Everyone Expects AI to Be Faster, We Say Wait a Minute

This is not counter-trend. It is a judgment based on observation:

As general capability improves, people will only pursue increasingly complex projects. When a user wants to develop something truly remarkable together with AI, no existing framework can truly do the job. Not because the technology is not strong enough, but because the collaboration model of frameworks is fundamentally wrong — it assumes the answer can be completed within one conversational turn, or at least within one continuous conversation stream.

But reality is not like that. Users do not expect AI to complete all the work within one conversation, but **there must be a constructive beginning**. Every conversation must be directional and progressive, even if the progress is only 1%.

WAM's response:

- **Slow down to speed up.** Establish the state first, then take the next step.
- **No bluffing.** When facing genuinely difficult problems, acknowledge the difficulty, then work through it together with the user.
- **A directional 1%.** Every step moves toward the goal, even if the step is small.
- **Weight-sensitive.** Hold the critical path, ignore the noise, do not do the useless work of covering everything.
- **Pragmatic and honest.** Push forward when feasible, admit when not. Honesty matters more than perfection.
- **Stay in sync.** One of the framework's core duties is to keep the states of AI and user aligned, or at least aligned to a communicable degree.

---

## On the Name

"Wait a Minute" is a reminder, a posture, a design philosophy.

It is not a module in the technical architecture diagram, but a comment written before every line of code. When the model tends to quickly generate a plausible-looking output, WAM says: wait — do we really understand what the user wants? Do we really understand the current situation? Do we really know what the next step should be?

If we don't, don't rush to answer.

Go figure it out first.

---

*This document records the core ideas of the WAM framework. It is not the final definition. As the architecture design progresses, these ideas may be revised, extended, or even overturned. This is exactly part of the WAM spirit — stay open, stay constructive, stay in awe of the unknown.*
