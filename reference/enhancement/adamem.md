# ADAMEM: Test-Time Adaptive Memory for Language Agents

- **Weight**: enhancement
- **Source**: `2606.05684v1.pdf` (18 pages) — `D:\github projects\personal_clone_repo\各个论文\framework reference\`
- **Authors**: Yunxiang Zhang, Yiheng Li, Ali Payani, Lu Wang (UMich; Cisco)
- **arXiv**: 2606.05684

## One-line summary

A hybrid memory architecture for test-time adaptation: a **long-term trajectory memory** of raw offline experiences plus an **on-the-fly dynamic short-term strategy memory** that guides decisions as long-horizon tasks unfold. No parameter updates. Trade-off between token efficiency and adaptability.

## Key concepts

- **Static-guidance misalignment** — guidance fixed at episode start becomes increasingly wrong as a long task unfolds. This is the academic statement of WAM's state desync.
- **Hybrid memory** — raw experience store (long-term) + generated strategy summary (short-term, refreshed on the fly).
- **Token efficiency vs adaptability** — an explicit cost trade-off for how much state to carry into each step.

## Mapping to WAM

| ADAMEM | WAM counterpart |
|---|---|
| Long-term trajectory memory | `workspace/log.md` (raw, append-only) |
| Dynamic short-term strategy memory | The **Read step**: session-start situation summary + "what's next" (state.md read + goals.md judgment) |
| Static-guidance misalignment | Why the protocol mandates reading state at every session start, not "once configured" |
| Token efficiency trade-off | Substrate CLI's value: answer "what's next" cheaply without dumping the whole log |

## 利用探讨 (how to use)

1. **Evidence for the Read step** — ADAMEM's misalignment result is citable evidence for why the six-step protocol's step 1 exists; the strategy-memory idea maps to the *session briefing* a WAM agent should generate at session start (a derived projection, never the source of truth).
2. **Cost model for state reads** — the token-efficiency framing gives substrate a design criterion: `wam goal next` should answer in one line, not one page. Add this to the stage-1 slice's DoD thinking.
3. **Deferred state-v2 input** — on-the-fly strategy generation is a candidate for state-v2's "derived projection" layer (the working-set idea from idea.md), not for v1.

## Next actions

- [ ] Adopt the one-line-answer criterion in substrate stage 1 (CLI output should be < 3 lines per query)
- [ ] Index the misalignment result in docs/research/02 as supporting evidence
- [ ] No deep-read needed unless state-v2 opens

## Related directions

substrate (stage 1 CLI) · state-v2 (deferred) · global-route (interaction flow continuation)
