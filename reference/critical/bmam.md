# BMAM: Brain-inspired Multi-Agent Memory Framework

- **Weight**: critical
- **Source**: `2601.20465v1.pdf` (22 pages) — `D:\github projects\personal_clone_repo\各个论文\framework reference\`
- **Authors**: Yang Li, Jiaxiang Liu, Yusong Wang, Yujie Wu, Mingkun Xu — Guangdong Institute of Intelligence Science and Technology / Institute of Science Tokyo / HK PolyU
- **arXiv**: 2601.20465 · **Benchmarks**: LoCoMo, LongMemEval, PrefEval, PersonaMem
- **Read status**: method + experiments + ablations read (2026-08-07); appendix diagrams skimmed

## Problem & motivation

Language agents operating over extended horizons lose temporally grounded information and behavioral consistency across sessions. The paper names this **soul erosion** and decomposes it into three distinct mechanisms, each requiring a specialized defense:

| Erosion type | What happens | BMAM defense | Brain analog |
|---|---|---|---|
| **Temporal erosion** | Fragmented episodic memories → loss of order/duration/temporal relations | **StoryArc** timeline indexing (per-entity timelines, normalized timestamps) | Hippocampus |
| **Semantic erosion** | Frequently accessed episodes fail to consolidate into stable knowledge | Selective consolidation: episodic → semantic | Hippocampus → neocortex (temporal lobe) |
| **Identity erosion** | User preferences/persona overwritten by transient context | **Amygdala-inspired salience tagging** — identity-relevant info protected | Amygdala |

Benchmarks that capture these: LoCoMo (temporal reasoning), LongMemEval, PrefEval (preference consistency), PersonaMem (persona recall).

## Core method

**Coordinator-centered multi-agent architecture**: a central coordinator routes information among functionally specialized subsystems (storage, retrieval, consolidation, control) that share a **unified memory substrate** — episodic timelines + knowledge graph + vector storage. Modular specialization without fragmenting memory state.

**Memory lifecycle loop** (six stages, hippocampus–neocortex inspired):
1. **Perception** — extract entities, temporal expressions, intent cues
2. **Shaping / active learning** — encode episodes; detect uncertainty
3. **Consolidation** — promote high-value episodic memories into semantic form
4. **Reflection** — detect contradictions; calibrate confidence
5. **Reconsolidation** — update memories when new evidence arrives
6. **Forgetting** — prune low-salience items (capacity budgets; low-priority pruned first)

**Hybrid retrieval**: fast path (context-level) + slower path (consolidated memory); evidence fused across episodic/semantic/knowledge-graph sources via **weighted reciprocal rank fusion** (RRF): `score(d|q) = Σ_s w_s / (k + rank_s(d|q))`, k=60, source weights w_s adaptive. Uncertainty and salience signals can trigger additional retrieval rounds or reweight sources. Time-dependent questions extract relative orderings/durations from the timeline structure.

**Background optimization**: reconsolidation on re-access (stability or content update), gradual pruning of low-value/outdated memories, prioritized consolidation of salient episodes.

## Experiments & results

- **LoCoMo**: 78.45% accuracy (standard long-horizon setting), beats baselines including MemOS (re-run by the authors with the same GPT-4o-mini backend for fairness).
- **LongMemEval** per category: single-session-preference 100.0%, single-session-user 87.1%, single-session-assistant 76.8%, knowledge-update 70.5%, **temporal-reasoning 59.4%**, **multi-session 52.6%** — the two hardest categories are precisely WAM's core territory.
- **Ablations** (LoCoMo subset): removing hippocampus-inspired episodic memory → **−24.62%** (central role confirmed). Removing Prefrontal (+5.03%) and Temporal Lobe (+4.02%) *improves* overall accuracy on the subset — the paper interprets this as an efficiency–robustness trade-off: the subset is 67% single-hop factual queries where direct episodic retrieval suffices ("System 1" tasks; higher-order routing is overhead). But on temporal queries specifically, removing the Temporal Lobe causes **−12.3%** — components are critical for their intended function, just not everywhere.

## Limitations

- Evaluation limited to four conversational long-term-memory benchmarks; broader domains are future work.
- Some baselines reported from original papers; only the primary baseline (MemOS) was re-evaluated in the same setting.
- Multi-agent coordination cost not deeply analyzed (see the Prefrontal ablation).
- Ethics section notes consent/data-retention concerns for persistent memory — relevant to any shared-state system.

## Mapping to WAM (detailed)

| BMAM element | WAM counterpart | Adoptability now |
|---|---|---|
| Soul erosion (3 types) | Continuity deficiency (idea.md) — **gives it a name and a diagnostic lens** | Adopt now: terminology + framing (site, docs) |
| Episodic subsystem | `workspace/log.md` — already append-only dated timeline | Aligned by design (M0 validation) |
| Semantic subsystem | `workspace/decisions.md` + `docs/` | Aligned |
| Salience tagging | `workspace/goals.md` weight tiers (critical/enhancement/noise) | WAM already has this; BMAM's version is retrieval-side, WAM's is planning-side |
| StoryArc timeline indexing | log.md evolution candidate for state-v2 | Later (state-v2) |
| Hybrid retrieval (RRF, uncertainty-driven) | substrate's future Read layer (`wam goal next` weighting recent/important log entries) | Later (after stage 1 exposes the need) |
| Memory lifecycle (consolidate/reflect/forget) | state-v2's derived projections + periodic review triggers | Later (state-v2) |
| Coordinator-centered MAS | idea.md: "agent count is an implementation detail" — BMAM shows one concrete way | Informational (does NOT force multi-agent) |

## 评估标准 (evaluation criteria — for the later assessment phase)

When deciding whether to adopt BMAM mechanisms into WAM, check:
1. **Does the CLI/Read layer actually benefit from RRF-style fusion over simple recency?** Measure `goal next` answer quality with vs without temporal weighting on WAM's own log.
2. **Does periodic consolidation (log → decisions digest) reduce session-start reading cost without losing fidelity?** (ADAMEM's verbosity result suggests raw trajectories degrade at scale — same risk for log.md.)
3. **Is the efficiency–robustness trade-off real for WAM?** BMAM's Prefrontal ablation warns: added machinery can *hurt* on simple cases. WAM's 1% principle demands the same caution — a mechanism must earn its place on real queries, not ablations on curated subsets.

## 研发路线 (R&D path — later phases)

1. **Now (stage 1, no code)**: adopt "soul erosion" terminology in idea.md and the site (one line, cited).
2. **After substrate stage 1**: if `wam goal next` struggles to surface recent-but-important log entries, prototype a temporal weighting (BMAM's temporal signal, simplified).
3. **state-v2**: story-arc-style timeline queries (when did X happen / what changed since Y), consolidation triggers, salience-protected identity data (author preferences live in workspace/state.md Known — protect them from being overwritten by transient context).
4. **Long-term**: LoCoMo-style evaluation of a runnable WAM runtime — with the honest caveat that human-in-the-loop shared-state evaluation is not the standard LoCoMo setup.

## Related directions

substrate (Read layer) · state-v2 (deferred) · global-route (continuity demo) · reference/critical/memory-survey.md
