# Memory in the Age of AI Agents: A Survey — Forms, Functions and Dynamics

- **Weight**: critical
- **Source**: `47372_Memory_in_the_Age_of_AI_.pdf` (107 pages) — `D:\github projects\personal_clone_repo\各个论文\framework reference\`
- **Authors**: Hu, Liu, Yue, Zhang, et al. — NUS, Renmin, Fudan, PKU, NTU, Tongji, UCSD, HKUST, Georgia Tech, OPPO, Oxford
- **arXiv**: n/a (survey PDF)
- **Read status**: TOC + selected sections read (2026-08-07): 3.1 (token-level memory incl. Flat/Planar/Hierarchical discussion), 3.4 (adaptation), 7.3–7.6 (RL, multimodal, world-model memory), 7.7 (trustworthy memory); **NOT yet read**: 4 (Functions) and 5 (Dynamics) in full, 6.1 benchmark details, 7.1–7.2, 7.5 (Shared Memory — heading not located in extracted text; needs a targeted re-read)

## Scope & organization

A landscape survey organized around three axes:
- **Form** — what carries memory: token-level (Flat 1D / Planar 2D / Hierarchical 3D), parametric (internal/external), latent (generate/reuse/transform), plus Adaptation.
- **Function** — why agents need memory: factual (user/environment), experiential (case-based, …), and further categories (chapters 4.x).
- **Dynamics** — how memory changes over time (chapter 5; not yet read).
- Plus: benchmarks/frameworks inventory (6) and position statements on frontiers (7).

## Key content read so far

**3.1.1 Flat Memory discussion** — flat collections are simple/scalable (append/prune cheap; similarity search without predefined structure) and suit broad recall, episodic accumulation, rapidly changing histories. But: no explicit relational organization → coherence depends on retrieval quality; redundancy/noise accumulate; retrieved units are understood without relations → limited compositional reasoning, long-horizon planning, abstraction. *This is the textbook statement of the ceiling WAM's four-file model will eventually hit — and the argument for state-v2.* Notably, WAM's files are flat AND human-curated; the survey's critique of pure flat memory assumes machine retrieval, not human+AI joint curation.

**3.1.2 Planar / 3.1.3 Hierarchical** — planar links nodes (knowledge graphs, traversal trees: Optimus-1, D-SMART); hybrid architectures segregate cognitive functions over a shared substrate. Hierarchical memory (3D) organizes memory into levels with different access speeds/lifetimes (MemGPT-style paging as one instance).

**7.2 Automated memory management** — the field is moving from hand-crafted structures toward automatically constructed/managed memory systems (RL-assisted: Context Folding, Memory-as-Action, MemSearcher, IterResearch). The survey's future perspective argues memory architectures should minimize human-engineered priors (cortical/hippocampal analogies, predefined taxonomies).

**7.3 RL meets agent memory** — RL increasingly internalizes memory-management abilities; expected to be the next major stage.

**7.5 Shared memory in multi-agent systems** — heading not located in extracted text (likely a short section); **needs a targeted re-read** before any multi-agent claims are made.

**7.6 Memory for world models** — world models (state+action→next state) depend on memory as the cornerstone for iterative prediction; connects to reference/enhancement/text-world-model.md.

**7.7 Trustworthy memory** — memory stores user-specific, persistent, potentially sensitive content: privacy, interpretability, safety challenges beyond RAG hallucination grounding; memory modules can leak private data through indirect channels. *Directly relevant to WAM's workspace/ holding the author's project state.*

## Mapping to WAM (detailed)

| Survey element | WAM counterpart | Meaning |
|---|---|---|
| Form taxonomy (Flat/Planar/Hierarchical) | `workspace/` four files = **flat, human-readable** form | state-v2's design space; the survey documents what the field builds instead |
| "Agent Memory vs. Context Engineering" (2.3.3) | WAM's core bet: state as shared artifact, not per-session context trick | The precise question WAM answers differently |
| Flat-memory critique | The ceiling of four Markdown files | Argument FOR state-v2 — but only after substrate exposes the actual pain (1% principle) |
| Automated memory management (7.2) | state-v2's eventual goal: framework-assisted curation | The survey itself warns against human-engineered priors; WAM's human-curated files are a deliberate counter-position worth defending |
| Trustworthy memory (7.7) | workspace/ privacy/interpretability | Design constraint: keep state human-readable (auditable by construction) |
| Benchmark inventory (6.1) | Evaluation targets for a runnable WAM | LoCoMo, LongMemEval, PrefEval, PersonaMem; WAM's human-in-the-loop setup likely needs adaptation |

## 评估标准 (evaluation criteria — later assessment phase)

1. When state-v2 opens: use 3.1's taxonomy to position the proposal explicitly ("we choose Flat + human curation, and here is the documented trade-off") — do not silently inherit the survey's bias toward hierarchical/automated designs.
2. Benchmark harvesting: extract the 6.1 table into docs/research/02 as an addendum; then decide which (if any) benchmark fits a human-shared-state evaluation.
3. Trust checklist from 7.7 applied to workspace/: who can read it (public repo!), what sensitive data should never enter it (author's credentials, tokens).

## 研发路线 (R&D path — later phases)

1. **state-v2 kickoff**: this survey + reference/critical/bmam.md are the two primary inputs; extract the benchmark table first.
2. **Substrate read layer**: consult 4 (Functions) before designing `goal next` semantics — retrieval is salience over time, not lookup.
3. **Positioning**: write the "what we deliberately do NOT adopt" section of the state-v2 proposal using 7.2/7.3 (no RL-managed memory, no hidden hierarchical stores — human-readable wins until evidence says otherwise).

## Next actions

- [ ] Deep-read 4 (Functions) + 5 (Dynamics) — scheduled for the state-v2 kickoff
- [ ] Locate and read 7.5 (Shared Memory in MAS) — target: does it cover human-shared memory at all? (If not, that absence itself is evidence for WAM's blank space.)
- [ ] Extract 6.1 benchmark table → docs/research/02 addendum

## Related directions

state-v2 (deferred) · substrate (Read layer) · reference/critical/bmam.md
