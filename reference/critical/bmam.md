# BMAM: Brain-inspired Multi-Agent Memory Framework

- **Weight**: critical
- **Source**: `2601.20465v1.pdf` (22 pages) — `D:\github projects\personal_clone_repo\各个论文\framework reference\`
- **Authors**: Yang Li, Jiaxiang Liu, Yusong Wang, Yujie Wu, Mingkun Xu (Guangdong Institute of Intelligence Science; Science Tokyo; HK PolyU)
- **arXiv**: 2601.20465

## One-line summary

A brain-inspired memory architecture that decomposes agent memory into specialized subsystems (episodic, semantic, salience-aware, control-oriented) at complementary time scales, organizes episodic memories on explicit timelines, and retrieves by fusing lexical + semantic + temporal signals. 78.45% on LoCoMo; ablations confirm the hippocampus-inspired subsystem is critical for temporal reasoning.

## Key concepts

- **Soul erosion** — the failure mode of long-horizon agents where fragmented or misaligned memory degrades behavioral continuity and identity across sessions. This is a *name* for WAM's continuity deficiency, with a diagnostic lens.
- **Subsystem decomposition** — episodic / semantic / salience / control memory as functionally specialized stores, not one unstructured blob.
- **Timeline-indexed organization** — episodic memories along explicit timelines.
- **Hybrid retrieval** — lexical + semantic + temporal signal fusion for robust grounding (fast context-level access + slower consolidated retrieval).

## Mapping to WAM

| BMAM subsystem | WAM counterpart |
|---|---|
| Episodic memory | `workspace/log.md` (timeline-indexed already — append-only with dates!) |
| Semantic memory | `workspace/decisions.md` + `docs/` (consolidated knowledge) |
| Salience-aware memory | `workspace/goals.md` weight tiers (critical path / enhancement / noise) |
| Control-oriented memory | `docs/01-foundation.md` protocol (how to act) |
| Hybrid retrieval | substrate's future Read layer (`wam state check` / `goal next`) |

## 利用探讨 (how to use)

1. **Name the enemy** — "soul erosion" gives WAM's core problem a citable, diagnosable name. Use it in the site, README, and pitches: WAM exists because agents suffer soul erosion; the shared workspace is the antidote.
2. **Validation of M0's bet** — BMAM's subsystem decomposition independently converges on WAM's four-file split (log/decisions/goals/protocol). This is external evidence that M0's structure was not arbitrary.
3. **Timeline as first-class** — BMAM's timeline-indexed episodic memory validates log.md's append-only dated design; substrate's `goal next` should weight recent log entries like BMAM's temporal signal.
4. **Retrieval fusion for state-v2** — when the state model outgrows direct reading, BMAM's lexical+semantic+temporal fusion is the concrete mechanism to adapt (with the docs/research/02 caveat: authoritative state reads direct, retrieval is auxiliary).
5. **LoCoMo as a future benchmark** — a runnable WAM runtime could be evaluated against LoCoMo's long-horizon accuracy to produce the first external evidence.

## Next actions

- [ ] Deep-read the retrieval fusion details (method section) before substrate's Read layer design
- [ ] Cite "soul erosion" in idea.md's continuity section (one line, with source)
- [ ] Track whether LoCoMo fits a human-in-the-loop shared-state evaluation (unusual setup — likely needs adaptation)

## Related directions

substrate (read layer) · state-v2 (deferred) · global-route (continuity demo)
