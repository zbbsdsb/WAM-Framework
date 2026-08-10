# ADAMEM: Test-Time Adaptive Memory for Language Agents

- **Weight**: enhancement
- **Source**: `2606.05684v1.pdf` (18 pages) — `D:\github projects\personal_clone_repo\各个论文\framework reference\`
- **Authors**: Yunxiang Zhang, Yiheng Li, Ali Payani, Lu Wang — UMich / Cisco
- **arXiv**: 2606.05684 · **Benchmarks**: ALFWorld (embodied navigation), WebShop (web shopping)
- **Read status**: method + experiments read (2026-08-07)

## Problem & motivation

Most agentic memory systems **restrict retrieval to episode initiation**: they front-load a retrieved trajectory or distilled strategy into the system prompt once, then rely on it as *static guidance* that becomes increasingly misaligned as long-horizon tasks unfold (intermediate failures, shifting sub-goals). Research questions: (1) how to make memory adapt continuously during inference without parameter updates; (2) how to train agents to synthesize strategies that explicitly optimize this test-time adaptation.

## Core method

**Hybrid memory architecture** (decouples storage from abstraction):

- **Long-term trajectory memory M** — scalable store of raw experiences collected offline; furnishes *verified demonstrations* of successful decision-making in similar historical states.
- **Short-term strategy memory z_t** — a concise natural-language strategy generated **on-the-fly**, conditioned on the current state s_t (unlike ReasoningBank's pre-generated offline strategies). This is the control point for adaptation.

**Two inference modes**: AdaMEM-low (refresh strategy at agent-decided steps) and AdaMEM-high (generate strategy at agent-decided steps) — a token-efficiency vs adaptability knob.

**STEP-MFT fine-tuning framework** — dual-filter rejection sampling to curate SFT data: keep only successful trajectories where the strategy actually *changed the action* (a_t ≠ a′_t vs memory-free baseline); discard redundant instances. Data record: (s_t, E_ret, z_t, a_t, a′_t, r). One unified fine-tuned model handles both strategy and action generation (no separate inference models).

## Experiments & results

- ALFWorld: No Memory 45.2±1.8 (seen) / 46.8±2.5 (unseen); ReasoningBank 49.3/51.2; Synapse 52.1/52.2; **ADAMEM 54.0±2.9 / 58.2±3.9** (training-free, on-policy LTM, Qwen3-4B).
- WebShop: No Memory 71.4±1.4; ReasoningBank 68.6; Synapse 65.4; **ADAMEM 74.2±0.3**.
- Off-policy LTM (Gemma-3-27b): ADAMEM also ahead.
- STEP-MFT beats outcome-only MFT and training-free baselines (ALFWorld seen ≈60+, WebShop ≈76+).
- **Verbosity pathology**: with raw-trajectory retrieval (Synapse-style), increasing retrieved trajectories k degrades performance (52.1% → 47.8%) — concatenating full trajectories overflows context with redundant content. ADAMEM's strategy compression avoids this. *This is the strongest quantitative argument for state-v2's derived projections and against dumping raw logs.*

## Limitations

- Task domains are *decisional* (navigation/shopping), not conversational collaboration — transfer to human-AI project work is inferred, not demonstrated.
- Strategy generation cost at test time (AdaMEM-high) vs token budget is a real trade-off, not free.
- Single fine-tuned model simplification means strategy quality depends on the base model's instruction following.

## Mapping to WAM (detailed)

| ADAMEM element | WAM counterpart | Adoptability now |
|---|---|---|
| Static-initialization critique | The exact failure WAM's Read step (step 1 of the six-step protocol) is designed against | Adopt now: citable evidence for the protocol |
| Long-term trajectory memory | `workspace/log.md` | Aligned |
| Short-term strategy memory z_t | The session briefing a WAM agent should generate at session start (a *derived projection*, never the source of truth) | Later (substrate stage 2 / agent-plugin skill) |
| Verbosity pathology | Risk for log.md at scale: raw log dumps into context degrade | **Adopt now as a design criterion**: `wam goal next` answers in one line, not one page |
| Token-efficiency vs adaptability knob | Protocol's 读 step cost model: how much state to read per session | Later (measure after stage 1) |

## 评估标准 (evaluation criteria — later assessment phase)

1. **One-line-answer criterion**: substrate CLI output < 3 lines per query (already folded into stage-1 DoD).
2. **Briefing quality**: when a session-start briefing (strategy-memory analog) is prototyped, compare task outcomes vs raw log reading over 2 weeks of real sessions.
3. **Adaptability check**: does the briefing get *refreshed* mid-session when state changes, or does it rot like static guidance? (The protocol's 停/判 steps are the refresh trigger.)

## 研发路线 (R&D path — later phases)

1. **Stage 1 (substrate)**: adopt the one-line criterion; no code from this paper yet.
2. **Stage 2 (agent-plugin skill)**: the skill's Read step should emit a compact briefing (state.md + goals.md distilled), not paste files — ADAMEM's strategy-memory is the direct reference.
3. **state-v2**: derived projection layer ("working-set" from idea.md) = short-term strategy memory; log summarization = its long-term trajectory compression; verbosity pathology is the quantitative justification.

## Related directions

substrate (stage 1 CLI) · agent-plugin (stage 2 skill) · state-v2 (deferred) · reference/critical/bmam.md (retrieval fusion)
