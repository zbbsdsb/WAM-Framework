# Bridging the Agent-World Gap: Text World Models for LLM-based Agents

- **Weight**: enhancement
- **Source**: `2606.09032v1.pdf` (31 pages) — `D:\github projects\personal_clone_repo\各个论文\framework reference\`
- **Authors**: Yixia Li, Hongru Wang, Peng Lai, … (SUSTech, Edinburgh, PKU, SYSU, CUHK, SUFE, Tsinghua, HKU)
- **arXiv**: 2606.09032

## One-line summary

Text world models (TWMs): transition models over textual states that, given a state and a candidate action, predict the resulting outcome (webpage, terminal output, API response, user reply) — supporting planning, efficient learning, and principled evaluation. Argues most LLM agents are reactive: they map observations to actions without an explicit model of how the environment evolves.

## Key concepts

- **Reactive vs model-based agents** — the paper's central critique: agents observe→act without predicting.
- **State→action→outcome prediction** — a transition model over textual states.
- **Planning & principled evaluation** — TWM enables lookahead and better assessment.

## Mapping to WAM

| TWM concept | WAM counterpart |
|---|---|
| Transition model (state + action → outcome) | The **反向机** in the author's global-route sketch — "state → prompt reconstruction" is a first cousin of state transition prediction |
| Reactive-agent critique | WAM's 停 (Wait) step: understand the situation *before* acting |
| Outcome prediction | A *pre-verification* version of the 验 (Verify) step — predict the evidence before producing it |
| World model of the collaboration | The shared workspace: state.md is WAM's explicit model of "how the project evolves" |

## 利用探讨 (how to use)

1. **Legitimize the global-route component** — the author's sketch has a "reverse machine" (反向机); TWM is the academic form of this idea. If global-route's minimal resume experiment passes, a lightweight TWM-style prediction ("if I take this step, what will the workspace look like?") is a candidate second slice — with the paper as its reference.
2. **Pre-verification for the protocol** — the 验 step can borrow the TWM framing: before doing, state the predicted evidence; after doing, compare. This is cheap, and it sharpens the Verify step's honest-failure branch. Candidate improvement to the protocol spec (docs/01-foundation.md) after stage 1.
3. **Evaluation discipline** — TWM's "principled evaluation" argument supports WAM's evidence rule: a "done" claim is only meaningful against a predicted outcome.

## Next actions

- [ ] Keep on file for the global-route second slice (only if the resume experiment passes)
- [ ] Consider a "predict the evidence" line in the protocol spec after substrate stage 1 (proposal → promotion gate)

## Related directions

global-route (reverse machine component) · substrate (protocol spec evolution)
