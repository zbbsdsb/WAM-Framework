# Reference — 借鉴库

> Established 2026-08-07. A weighted library of papers and ideas borrowed into WAM's development. Every entry is classified by weight tier and carries a "how to use it" exploration (利用探讨).
>
> **The pipeline is defined in [WORKFLOW.md](WORKFLOW.md)**: Ingest → Assess (no code, assessment matrix) → Propose (directions/) → Verify (vertical slice) → Integrate (promotion gate + write-back) → Revisit. Assessment and development happen AFTER ingestion — the library is a storage repository until a paper passes its matrix.

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

Status: `ingested` (awaiting assessment) / `assessing` / `adopted` / `adapted` / `deferred` / `rejected`. Assessment priority: critical → enhancement → noise (never).

| Paper | Tier | WAM hook | Status |
|---|---|---|---|
| Memory in the Age of AI Agents (survey, 107p) | critical | Memory-form taxonomy → state-v2 / substrate layering | ingested — assessment scheduled (next) |
| BMAM: Brain-inspired Multi-Agent Memory | critical | Subsystem memory ↔ four state files; "soul erosion" names the continuity gap | ingested — assessment scheduled |
| ADAMEM: Test-Time Adaptive Memory | enhancement | Long-term trajectory + on-the-fly strategy memory → Read step | ingested — assessment scheduled |
| Text World Models for LLM-based Agents | enhancement | State→action→outcome prediction → "reverse machine" / pre-verification | ingested — assessment scheduled |
| World-Action Model (WAM) — CALVIN | noise | Name collision only; robotics RL, unrelated | ingested — noise tier, never assessed |

Every entry now carries: problem & motivation, core method, experiments & results, limitations, detailed WAM mapping, **evaluation criteria (评估标准, for the later assessment phase)**, and an **R&D path (研发路线, for the later development phase)**. The library is a *storage repository* — assessment and development happen later, gated by the normal promotion process.

## Source material

PDFs live in `D:\github projects\personal_clone_repo\各个论文\framework reference\` (not copied into this repo to keep it light). Entries reference them by filename.
