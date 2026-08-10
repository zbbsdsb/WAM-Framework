# Reference — 借鉴库

> Established 2026-08-07. A weighted library of papers and ideas borrowed into WAM's development. Every entry is classified by weight tier and carries a "how to use it" exploration (利用探讨).

## Weight tiers (consistent with workspace/goals.md)

| Tier | Meaning | What happens to the paper's ideas |
|---|---|---|
| **critical** | Directly shapes current M1 architecture decisions | Must be read thoroughly; mechanisms enter direction proposals |
| **enhancement** | Does not change current decisions, but offers portable mechanisms | Indexed for later design (state-v2, substrate read layer, etc.) |
| **noise** | Good to know; not worth deep work | Skimmed; cited only when relevant |

## Lifecycle of an entry

1. **Ingest** — extract title/abstract/contribution, write the entry file with a weight judgment.
2. **Map** — connect the paper's concepts to WAM's concrete parts (state model, six-step protocol, directions).
3. **Use** — the exploration says exactly how: transplant directly / adapt / name a phenomenon / trigger a design decision.
4. **Promote or rest** — mechanisms that survive verification move into direction proposals (per the promotion gate); the entry records what was adopted.

## Index

| Paper | Tier | WAM hook | Entry status |
|---|---|---|---|
| Memory in the Age of AI Agents (survey, 107p) | critical | Memory-form taxonomy → state-v2 / substrate layering | Ingestion done; deep-read scheduled |
| BMAM: Brain-inspired Multi-Agent Memory | critical | Subsystem memory ↔ four state files; "soul erosion" names the continuity gap | Ingestion done; deep-read scheduled |
| ADAMEM: Test-Time Adaptive Memory | enhancement | Long-term trajectory + on-the-fly strategy memory → Read step | Ingestion done |
| Text World Models for LLM-based Agents | enhancement | State→action→outcome prediction → "reverse machine" / pre-verification | Ingestion done |
| World-Action Model (WAM) — CALVIN | noise | Name collision only; robotics RL, unrelated | Ingestion done |

## Source material

PDFs live in `D:\github projects\personal_clone_repo\各个论文\framework reference\` (not copied into this repo to keep it light). Entries reference them by filename.
