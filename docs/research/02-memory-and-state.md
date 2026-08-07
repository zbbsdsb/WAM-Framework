# Research Brief 02 — Memory & State Architectures for LLM Agents

> Date: 2026-08-07 · Method: parallel research task; arXiv IDs verified via arXiv API, repos via GitHub API · Purpose: feed state model v2 design

## Key findings

1. **CoALA** (arXiv:2309.02427): memory = working / episodic / semantic / procedural; actions = internal reasoning / external tools; decision loop = plan → act → observe. A conceptual framework, but now the standard vocabulary.
2. **MemGPT/Letta** (arXiv:2310.08560): "LLM as OS" — main memory (resident JSON) + external storage (recall + vector archive); the LLM pages memory itself; memory pressure triggers write / retrieve / summarize. Beats fixed context on long-document QA and multi-session chat.
3. **Generative Agents** (arXiv:2304.03442): memory stream + reflection (periodic synthesis of higher-level conclusions) + weighted retrieval (recency × importance × relevance). Ablations show each component contributes to believable behavior; evidence is simulated believability, not task metrics.
4. **A-MEM** (arXiv:2502.12110): zettelkasten-style notes + dynamic links + memory evolution (new memories trigger updates of old ones). Beats SOTA across 6 base models.
5. **Products**: Mem0 (arXiv:2504.19413; LLM extraction + vector/graph dual storage + add/update/conflict ops), Zep Graphiti (time-aware knowledge graph, incremental timestamped edges), LangMem (core/episodic/semantic/procedural memory API + background auto-extraction). All self-reported; no independent third-party evaluation.

## Design implications for WAM (inference, not verified fact)

- **Layering is consensus**: working vs long-term separation; CoALA's four classes map naturally onto state / goals / log / decisions; explicit read/write permissions needed per class.
- **Reflection/compression paths are validated**: periodic review triggers (log → decisions) are worth building.
- **Authoritative state read-direct + vector retrieval only as auxiliary** (avoids retrieval misses; apply time-decay to retrieval).
- **Updates must leave traces**: overwrite chains, not silent rewrites.

## Unresolved problems

- Memory fidelity: LLM-generated reflections/summaries have no correctness guarantee; drift and hallucinated memory have no evaluation method.
- Retrieval misses & staleness: no unified timestamp/invalidation mechanism.
- No standard benchmark for multi-session long projects.
- **Human-shared state is unresearched**: all memory systems are agent-internal. Human-readable, human-editable shared state is WAM's blank space.

## Sources

arXiv:2309.02427, 2310.08560, 2304.03442, 2502.12110, 2504.19413; docs.letta.com; github.com/getzep/graphiti; github.com/langchain-ai/langmem.
