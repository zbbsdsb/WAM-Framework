# Research Brief 03 — Unknown-Unknowns & Weight Judgment

> Date: 2026-08-07 · Method: parallel research task; arXiv IDs verified via arXiv API, literature via Crossref · Purpose: feed the "unknown registry" and "weight judgment" features

## Theme A: unknown-unknowns & calibration

**Findings**

- Ignorance quadrant taxonomy: known / known-unknown / unknown-unknown (Smithson 1989) — the exact vocabulary WAM's state.md three sections already uses.
- Three-channel confidence: token probability, semantic entropy (Kuhn 2023, arXiv:2302.09664), verbalized confidence (Lin 2022, arXiv:2205.14334; Tian 2023, arXiv:2305.14975). Cross-checking channels catches overconfidence.
- Question gates before acting: Ask Me Anything (arXiv:2210.02441); FLARE triggers retrieval on low confidence (arXiv:2305.06983).
- Structured Ignorance Certificates (arXiv:2606.08571): the model outputs a JSON "ignorance certificate" declaring its knowledge boundary — the closest existing mechanism to WAM's explicit unknown registry.
- ADVICE (arXiv:2510.10913): verbalized confidence is systematically overconfident.

**Portable to WAM**: quadrant labels on state items; confidence cross-check; the "question gate" (WAM's 停/判 steps already embody it); ignorance certificates as a machine-readable unknown registry.

**Open**: unsupervised detection of unknown-unknowns is essentially unsolved → WAM's contribution is the explicit registry + human-in-the-loop, not automatic detection.

## Theme B: weight / priority judgment

**Findings**

- Generative Agents retrieval: recency × importance × relevance (arXiv:2304.03442).
- Self-RAG: reflection tokens adjudicate relevance (arXiv:2310.11511).
- ToT value scoring & pruning (arXiv:2305.10601); HuggingGPT task DAGs (arXiv:2303.17580).
- Counter-evidence: "What Deserves Memory" (arXiv:2508.03341) criticizes heuristic importance scoring as designer intuition.

**Portable to WAM**: importance score on goals/log entries (human-annotated first, model-assisted later); DAG/tree goal structure with an explicit critical path.

**Open**: **critical path method (CPM) in LLM agent planning has no dedicated literature** (nearest: Vote-Tree-Planner arXiv:2502.09749, DART-LLM arXiv:2411.09022 — neither uses CPM) → WAM's clearest original contribution; no cross-task benchmark for importance scoring.

## Caveats

- Ramírez & Burrage "unknown unknowns" literature: not found in Crossref / arXiv / Semantic Scholar — flagged, not fabricated.
