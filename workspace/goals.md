# Goals

> Goal tree. Each item: `- [ ] Title — Weight: critical path/enhancement/noise — Progress — Next step`
> Weight tiers: critical path (blocked without it) > enhancement (better with it) > noise (not done, not scheduled)

## M0 Foundation (current milestone)

- [x] Define the state model and collaboration protocol — Weight: critical path — Progress: done — Evidence: docs/01-foundation.md
- [x] Set up the four workspace/ state files and record the project founding — Weight: critical path — Progress: done — Evidence: this directory
- [x] Run a real session through the full six-step protocol (Read→Wait→Judge→Do→Verify→Write) — Weight: critical path — Progress: done — Evidence: all sessions 2026-08-06/07 followed the loop (bootstrap, README, translation, survey); this session: read→wait→judge→do(dispatch)→verify(results)→write

## M1 方向竞争与第一个切片（current next milestone）

- [x] Targeted survey: ecosystem / memory & state / unknown & weight — Weight: critical path — Progress: done — Evidence: docs/research/*
- [x] Establish directions/ folders + promotion gate (three tiers: evidence / proposals / decisions) — Weight: critical path — Progress: done — Evidence: directions/README.md, docs/01-foundation.md §Development Governance
- [x] Open 4 competing directions: global-route (author) / substrate / agent-plugin / weight-first — Weight: critical path — Progress: done — Evidence: directions/*/README.md
- [x] Public site: site/index.html (bilingual EN/中文, atompunk) — Weight: enhancement — Progress: done — Evidence: site/index.html, https://zbbsdsb.github.io/WAM-Framework/
- [x] M1 execution plan confirmed: substrate (stage 1, +verify-gate) / agent-plugin (stage 2) / weight-first (stage 3) slices; global-route minimal resume experiment; state-v2 deferred — Weight: critical path — Progress: done — Evidence: workspace/decisions.md
- [x] Reference library (reference/): 5 papers ingested, tiered critical/enhancement/noise with utilization explorations — Weight: enhancement — Progress: done — Evidence: reference/*
- [ ] Stage 1: substrate vertical slice — wam CLI (state check / goal next / log append) + evidence checker — Weight: critical path — Progress: not started — Next step: next session; DoD: catches a real format error in WAM's own workspace, answers "what's next" without reading files by hand, checker flags an evidence-less "done"
- [ ] Stage 2: agent-plugin vertical slice — Hermes skill implementing the six-step protocol, used on the WAM repo for a week — Weight: critical path — Progress: not started — Next step: after stage 1; DoD: skill's state check catches something the host agent would have missed in 3 consecutive sessions
- [ ] Stage 3: weight-first vertical slice — goal DAG + critical-path computation on goals.md — Weight: critical path — Progress: not started — Next step: after stage 2; DoD: within two weeks the computed critical path changed or prevented a priority decision
- [ ] Stage 1 parallel: global-route minimal resume experiment (cross-session "continue" from workspace/) — Weight: critical path — Progress: not started — Next step: with stage 1; no full engine
- [ ] Convergence: first direction to pass the promotion gate defines M1 architecture; others archive or merge — Weight: critical path — Progress: not started

## Scheduled follow-ups (not expanded before M1)

- Tooling for state files: format validation, quick queries
- Assistance mechanism for weight judgment
- Runtime and agent layer (language/architecture TBD)
