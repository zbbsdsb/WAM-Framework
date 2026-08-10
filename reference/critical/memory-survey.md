# Memory in the Age of AI Agents: A Survey — Forms, Functions and Dynamics

- **Weight**: critical
- **Source**: `47372_Memory_in_the_Age_of_AI_.pdf` (107 pages) — `D:\github projects\personal_clone_repo\各个论文\framework reference\`
- **Authors**: Hu, Liu, Yue, Zhang, … (NUS, Renmin, Fudan, PKU, NTU, Tongji, UCSD, HKUST, Georgia Tech, OPPO, Oxford)
- **arXiv**: n/a (survey PDF)

## One-line summary

A 107-page landscape survey of agent memory organized around three axes: **Form** (what carries memory: token-level Flat/Planar/Hierarchical 1D/2D/3D, parametric, latent), **Function** (what memory is used for), and **Dynamics** (how memory changes over time).

## Mapping to WAM

- The Form taxonomy (Flat → Planar → Hierarchical) is the design space WAM's four-file state model occupies: our Markdown files are a *flat, human-readable* form. The survey documents what the rest of the field builds instead — this is the evidence base for state-v2's evolution.
- "Agent Memory vs. Context Engineering" (2.3.3) is precisely the question WAM answers differently: we make the state a *shared artifact*, not a per-session context trick.

## 利用探讨 (how to use)

1. **Dictionary for state-v2** — use the survey's taxonomy as the vocabulary when designing the state model's evolution (deferred until substrate exposes problems). When state-v2 opens, this paper is its primary input alongside docs/research/02-memory-and-state.md.
2. **Substrate read-layer design** — the survey's Function/Dynamics chapters inform what `wam goal next` / `wam state check` should expose: retrieval is not just lookup, it is *salience over time*. BMAM's hybrid retrieval (next entry) is the concrete mechanism; this survey is the context.
3. **Benchmark harvesting** — the survey lists long-horizon agent benchmarks; LoCoMo (used by BMAM) is a candidate evaluation target when WAM has a runnable runtime.
4. **Avoidance list** — memory drift / hallucinated memory / staleness failure modes (already flagged in docs/research/02) get their full treatment here; the state-v2 design must cite these as explicit non-goals.

## Next actions

- [ ] Deep-read sections 3 (Form) and 5-6 (Function/Dynamics) when state-v2 opens
- [ ] Extract the benchmark table into docs/research/02 as an addendum
- [ ] Record "what we deliberately do NOT adopt" (e.g., vector retrieval as primary store) in state-v2 proposal

## Related directions

substrate (read layer) · state-v2 (deferred) · docs/research/02-memory-and-state.md
