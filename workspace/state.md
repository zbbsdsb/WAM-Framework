# Situation

> A snapshot of the current situation shared between human and AI. Read here at the start of every session; update here at the end.

## Known

- WAM (Wait a Minute): an agent framework, philosophy recorded in idea.md.
- Core diagnosis: fourfold deficiency (constructiveness, continuity, verifiability, weight judgment) + state desync; the response is the 1% foundation, the sage and the doer, and six response principles.
- Project stage: founded 2026-08-06, M0 foundation complete (state model + collaboration protocol, see docs/foundation.md).
- Development governance: unverified work lives in directions/, promoted only after verification (three tiers: evidence / proposals / decisions).
- M1 in progress: four competing directions open (global-route / substrate / agent-plugin / weight-first); convergence = first verified vertical slice.
- Experiment track space: experiments/ established 2026-08-15 — executable verification tracks run in stages via DeepSeek Harness agent presets; first experiment path design pending (see workspace/goals.md).
- **Implementation status 2026-10-09: zero executable code.** 29 tracked files, all Markdown/HTML/CSS/YAML. No direction has produced a vertical slice.
- **Design baseline established 2026-10-09** (docs/vision.md–docs/specifications/acceptance.md): five core concepts (Intent / Situation / Judgment / Move / Evidence & Update), core loop, MVP plan with stage gates, decision register, 4 validation scenarios + 10 acceptance criteria. All marked as design intent, none as implemented.
- **The most important premise is now recorded** (docs/vision.md §3): WAM has no desire of its own. Numerical scores are evidence within a scenario, not a universal objective function. User intent is the anchor of judgment; WAM may interpret and suggest but must not silently rewrite the user's goal.
- **Two structural gaps identified** (docs/specifications/state-and-evidence.md §6.2): of 10 questions needed for cross-session recovery, 6 are answerable, 2 are not (assumptions with validation paths; failure paths / disconfirmed hypotheses), 2 are marginal (session-level intent; why the next step is worth it).
- **Judgment as process has no carrier**: decisions.md records what was decided, not how the judgment was reached — so judgment traceability cannot be checked today.
- **Tech stack undecided, and not needed yet — the foundation is collaboration state, not code.**
- **Engineering baseline fixed 2026-10-09 (docs/development/mvp-plan.md §1)**: Python 3.13.12 + zero third-party deps (stdlib verified 17/17); codex-cli 0.138.0 as first Judgment provider and Move executor (`--output-schema` / `--json` / `-s read-only|workspace-write` / `exec resume` all verified present); single-file `.wam/state.json` written atomically via `tempfile` + `os.replace`. DeepSeek Harness kept as a future executor option (npm has 0.2.0-rc.2, but node_modules absent and runnability unverified).
- **The environment's `OPENAI_BASE_URL` endpoint is unusable** — `/models` and `/chat/completions` both return HTTP 403 (gateway replies "该接口未接入公益站独立网关"). Do not write code that assumes it works (X-07).
- **MVP interface set fixed at 6** (docs/specifications/execution-contract.md §5): IntentProvider / SituationBuilder / JudgmentProvider / MoveExecutor / EvidenceVerifier / StateRepository. Each has a stated replacement reason; DirectionProvider, WeightCalculator, CandidateRanker, EventBus, ReflectionService are deliberately NOT interfaces. Interfaces get extracted at T-14, i.e. after the vertical slice runs — not before.
- **One recorded deviation from the M0 constitution** (B-13 / OQ-18): the MVP treats `workspace/*.md` as read-only evidence input and `.wam/state.json` as the loop's authority, so the MVP runs against a dedicated fixture project rather than the WAM repo itself. Dogfooding WAM with WAM would create two writers of state.
- **2026-10-28: the executor choice in docs/development/mvp-plan.md §1.2 is falsified.** codex-cli 0.138.0 exists and is **logged in**, but `codex exec` against `api.openai.com` returns **403 `Country, region, or territory not supported`** (cf-ray HKG, after 7 reconnects). Authentication is not the problem; the region is. Replaced by B-15: `dsh --profile headless` first (help text verified, profile **not installed**), human executor as the always-available fallback. **The six interfaces and the loop are unaffected — this is the first real payoff of "interfaces before implementation".**
- **2026-10-28: goal taxonomy established** (`docs/development/scope.md`). Three axes: responsibility layer L0–L5 (belief / commitment / judgment / action / presentation / substrate) × commitment G1–G5 (committed / exploratory / conditional / deferred / rejected) × evidence E1–E4 (executable / observable / external judgement / argument). 35 cells. **The MVP is now derived from cells, not discussed**: 20 in, 3 minimal, 12 out.
- **2026-10-28: the L4 presentation layer was the empty layer.** Of the four deficiencies plus state desync, L4 (what the user sees) is the only layer that directly serves state desync — and it had no goal in docs/vision.md–08. That gap is now filled by the attention state machine (`docs/architecture.md` §12): **10 machine states / 6 presentation modes**, orthogonal to the Move lifecycle, with six E1-testable invariants.
- **2026-10-28: the MVP's type claim is now explicit and narrow** (`docs/development/scope.md` §3.2): **T1 (convergent) only, plus T2 at levels L1–L2.** T3 (open-ended construction) and T4 (inquiry with no metric) are Phase 4 test cases, not MVP promises. Without this sentence the four-scenario document reads as "the MVP supports all four".
- **2026-10-28: fifth direction opened** — `directions/shared-context/` carries the author's three claims (no conversational multi-agent; a layered shared context with explicit per-agent boundaries living in the "information source" responsibility space; default scheduling = one Miracle Agent with concurrent tool-registry calls). Its nearest precedents were identified but **not read** (SE-Blackboard IEEE 11527206; an LLM blackboard paper), so **originality is not claimed**.
- **2026-10-28: schedule is 9 weeks 2 days** (10-29 → 12-31), not 12. Roadmap in `docs/development/roadmap.md`; the only non-negotiable gate is **W4 (vertical slice)**.


## Unknown

- Whether the four state files suffice in real collaboration and whether the format needs to evolve.
- Single-agent or multi-agent presentation (idea.md explicitly states this is an implementation detail).
- Whether the three weight tiers (critical path/enhancement/noise) need finer granularity.
- **Intent's minimum data expression (OQ-01)** — blocks MVP stage 2a entirely.
- **How to express an authorization boundary** (OQ-05 / B3) — blocks Human Absent Mode.
- **Whether WAM should bind any execution platform** (OQ-10): DSH's preset mechanism was verified against source; "Hermes" could not be found on this machine; the dashboard plan implies Python while DSH is TypeScript.
- **What WAM's relationship to Sponge is** (OQ-09): the Sponge repo positions WAM as an application-layer derivative built on Sponge and puts it in its convergence acceptance criteria, while this repo contains zero mentions of Sponge and defers tech stack entirely. Author decision needed; also note Sponge's description of WAM's six-step loop is now outdated relative to docs/architecture.md §2.
- **Whether codex is authenticated in the target environment** (OQ-19): the CLI version (0.138.0) and every flag docs/development/mvp-plan.md relies on were verified, but the auth state itself could not be checked — the sandbox blocks `~/.codex`. Blocks T-06/T-08 only; T-01–T-05 are unaffected.
- **How the codex sandbox tier maps from `authorization`** (OQ-20): the three tiers exist, the mapping rule is ours and unverified. MVP starts at the most conservative setting (default `read-only`, upgrade only on approval) and widens in Phase 2.
- **Whether the Judgment schema is stable** (OQ-21): if it needs three revisions, the I3 boundary is wrong — go back to design rather than keep tuning the prompt.
- **What "done" means for an open-source acceptance project** (OQ-22): scenario C has no single metric, so completion needs external judgment. Blocks Phase 4 case design, not the MVP.
- **Operational tasks (T5, "keep it from breaking") have no Intent form** (OQ-23): is doing nothing a success? Not modelled this version.
- **Whether scope write-set overlap should block or serialise** (OQ-24): blocking exposes the design error, serialising hides it.
- **Whether 10 user-visible states is too many** (OQ-25): community products converge on 3; our justification (cross-session, cross-day re-sync needs WAITING vs ASKING) is untested.
- **Whether `dsh --profile headless` output can be reliably constrained to JSON** (OQ-26): capability seen only in help text; profile not installed. **Blocks W3's JudgmentProvider.**
- **Whether J6's stagnation criterion is valid** (OQ-27): a paper discussing "agent loops mistaking stagnation for progress + self-evaluation bias" was located but not read (429). If not read before W2, do not implement J6 in W6.

## Unknown-Unknowns

Product-level:
- When collaboration scales: multi-project support? state partitioning? how do concurrent sessions write to the same log?
- How "weight judgment" transitions from manual human annotation to framework-assisted judgment.
- Whether a state update can leave a half-written state (consistency, B5) — the MVP answers this with a single write point plus atomic replace (docs/development/mvp-plan.md §4.2), which is a design rather than a mechanism, so it still needs proving under real interruption.
- Whether 8 weeks of repository inactivity (2026-08-15 → 2026-10-09) is itself a signal about the project's operating conditions.
- **Added 2026-10-09 (PM)**: whether a fixture project small enough to be reliable is also small enough to be misleading. Phase 4 exists to answer this, and it must include a no-numeric-metric case (docs/development/mvp-plan.md §9.2 A10).

Development-process (listed 2026-08-15 — per hard rule 4, explicit, never feigned):
- Whether the convergence gate actually converges, or the four directions stall in permanent competition.
- Whether the wam CLI has real leverage or degrades into a markdown formatter (substrate falsification condition).
- Whether host agents actually follow the six-step protocol once embedded (agent-plugin falsification condition).
- Whether a computed critical path beats a flat todo list in practice (weight-first falsification condition).
- The semantics of the author's sketch 反向机 (pending author confirmation).
- When real usage will force the four-file format to evolve (state-v2 trigger).
- **Added 2026-10-09**: whether documenting the design without running anything is itself a repetition of the 2026-08-15 failure mode (planning instead of executing). docs/development/mvp-plan.md §8.1 lists this as a live risk — this session produced documents, not execution.
- **Added 2026-10-09**: whether the four validation scenarios are actually runnable against the current design, or whether some of them need capability that the MVP will not have (docs/specifications/acceptance.md §5.1 deliberately defers this).
- **Added 2026-10-28**: whether the author can sustain 12–16 hours/week for 9 consecutive weeks with no interruption week. The roadmap has no calendar buffer on purpose; if this assumption is wrong, the plan breaks at **W4**, not at W9.
- **Added 2026-10-28**: whether "zero executable code after 3 months, with 4 documentation-only sessions" is a *scheduling* observation or already the **conclusion** about this project's operating conditions. The 2026-08-15 diagnosis said the same thing and was followed by a 8-week gap. This is the one unknown that determines whether the roadmap matters.
