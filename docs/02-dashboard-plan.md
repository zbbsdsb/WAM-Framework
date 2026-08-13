# R&D Dashboard Plan — 研发看板计划

> Status: **approved for planning** (2026-08-07, author direction "专门写进一个计划里"). The team-facing dashboard that makes WAM's shared state visible. This plan is the single source of truth for the dashboard effort; execution is staged P1–P4 with DoD, hard gates, and time boxes.

## Background & motivation

The WAM team (author + AI agents) runs on a shared-state protocol: `workspace/` four files, six-step protocol, directions/ + promotion gates. But the state lives in Markdown files — human-readable, yet not *visible at a glance*. The team needs a dashboard that renders the state model, so that:

- **Orient meetings** (定向会) start from a shared picture, not from reading five files.
- **Verification culture** is visible: every progress entry shows its evidence badge; failures are shown, not hidden.
- **Weight judgment** is front and center: critical-path work is visually distinct from enhancement and noise.
- **Agents and humans see the same board**: the dashboard is the human interface; the md files remain the agent interface — one data source, no drift.

Dogfooding: WAM claims state sync as its core contribution — its own team should be the first visible beneficiary.

## Positioning & principles

1. **Data is the files.** The dashboard stores nothing; it renders `workspace/`, `directions/`, `reference/`, and git. Changing a md file changes the board. No separate state to go stale.
2. **Deterministic generation.** One command, one output. No build chain, auditable, reproducible (same philosophy as the site's single-file HTML).
3. **Science over decoration.** The board shows pre-registered hypotheses, verification status, evidence chains, and failure records — not just pretty progress bars.
4. **Human interface = HTML, agent interface = md.** Work agents do not read the board; they read and write the files. The board is for the author and the coordinator agent.

## Data sources (zero new maintenance burden)

| View data | Source |
|---|---|
| Milestone / goal status | `workspace/goals.md` (weights, status marks, DoD, evidence refs) |
| Current situation / unknowns | `workspace/state.md` (Known / Unknown / Unknown-unknowns) |
| Progress timeline | `workspace/log.md` (dated entries with evidence refs) |
| Decision records | `workspace/decisions.md` (reason / alternatives / weight judgment) |
| Direction competition | `directions/*/README.md` (hypothesis / falsification / promotion gate / status field) |
| Reference library | `reference/README.md` (paper statuses) |
| Release / change history | `git log` (commit history) |

## View structure (6 panels)

**① Mission Control (指挥台)** — default view
- Current milestone + critical-path goal highlighted (weight colors: critical red / enhancement teal / noise gray)
- Gate traffic lights (预注册门 / 证据门 / 决策门 / 晋升门) — mechanically derived from files
- Known / Unknown / **Unknown-unknowns** counters

**② Goals Board (目标看板)** — goals.md rendered as a Kanban by weight tier
- Three columns: critical / enhancement / noise
- Per item: status, DoD, evidence link, time box

**③ Direction Races (方向赛马)** — the 4 competing directions
- Per direction: hypothesis, falsification condition, slice progress (not-started / slicing / verified / promoted / archived)
- Convergence gate visibility (first promoter defines M1)

**④ Evidence Trail (证据链)** — log.md timeline
- Per entry: date, content, evidence ref (commit / command / path, clickable)
- Verification badges: ✅ verified / ⏳ pending / ❌ failed (failures shown — publication-bias control)

**⑤ Decision Ledger (决策簿)** — decisions.md rendered
- Decision, reason, alternatives (collapsible), weight judgment

**⑥ Reference Status (借鉴状态)** — paper status table
- Tier badges (critical/enhancement/noise) + status (ingested/assessing/adopted/deferred/hold)
- Reuses reference/README index

## Technology choice

**Generator approach**: `scripts/dashboard.py` (future `wam dashboard`)
- Parses md (goals `- [x]` marks, log dated entries, direction front-matter) → emits single-file `dashboard.html` reusing the site's design system (atompunk + constructivism + age layer, bilingual)
- Local: `python scripts/dashboard.py` → open in browser
- Deploy: gh-pages page `dashboard.html` (same sync flow as details.html)
- **The generator's parse/validate logic is the embryo of substrate's `state check` CLI** — dogfooding ×2

## Relationship to the team R&D workflow

| Workflow stage | Dashboard use |
|---|---|
| Orient (定向会) | Mission Control: align weights, confirm critical path, read gate lights |
| Execute | agent edits md → regenerate → Evidence Trail updates (natural progress broadcast) |
| Verify | Evidence Trail: check every step carries an evidence badge |
| Retro (复盘会) | Goals Board vs Evidence Trail: did we do what we said? Where are the failures? |
| Release | Mission Control shows recent commits + live site status |

## Staged implementation plan

### P1 — Skeleton (1 session, time-boxed)
- **Scope**: generator + Mission Control + Goals Board + Evidence Trail
- **DoD**: `python scripts/dashboard.py` renders from real workspace data; opens in browser with zero console errors; three views cross-checked against source files (sampled)
- **Hard gate**: weight/status parsing correct on 10 sampled goals items; evidence-ref extraction correct on sampled log entries
- **Overrun**: split — Mission Control first, then Goals, then Evidence Trail

### P2 — Complete (1 session)
- **Prerequisite**: add `Status:` field to the 4 direction READMEs (not-started/slicing/verified/promoted/archived)
- **Scope**: Direction Races + Decision Ledger + Reference Status + gate traffic lights (initial rules: overdue goals items, evidence-less log entries, pending decisions)
- **DoD**: all 6 panels open; traffic-light judgments match manual review on 5 sampled checks
- **Hard gate**: every panel traces its data to a file path (auditable)

### P3 — Deploy (1 session)
- **Scope**: gh-pages `dashboard.html` + nav entry from the site (index/details topbar or REFERENCE-style link)
- **DoD**: live URL works; gh-pages copy byte-identical to local (EOL-normalized); verification script green
- **Hard gate**: site i18n integrity preserved (no new unpaired data-en/data-zh)

### P4 — Evolution (triggered with substrate stage 1)
- **Scope**: extract the parse/validate logic into the substrate CLI's `state check`
- **DoD**: `wam state check` reproduces the dashboard's integrity checks from the same parsing module
- **Hard gate**: same inputs → same verdicts (dashboard vs CLI)

## Risks & mitigations

| Risk | Mitigation |
|---|---|
| Generator judgment drifts from human judgment | Sampled cross-checks at each P stage; generator output is auditable (deterministic) |
| Dashboard becomes decoration nobody uses | Fixed usage in Orient/Retro meetings; author is the primary user |
| md format evolution breaks parsing | Tolerant parser + format conventions documented in docs/01-foundation.md if needed |
| Dashboard duplicates the site's look or drifts from it | Reuse site/style.css; generation shares the design tokens |

## Open decisions (defaults in brackets — author may override)

1. **Traffic-light rules**: start with three coarse rules — (a) any `[ ]` goal item past its time box → yellow; (b) any log entry without an evidence ref → red; (c) any decision without alternatives section → yellow. Refine later.
2. **Direction `Status:` field**: add to all 4 direction READMEs (default: yes, needed by P2).
3. **Public deployment**: yes — goals/decisions are already public in the repo; the dashboard adds no new exposure.
4. **P1 timing**: start immediately (default) — the generator is the CLI's precursor, so early work is not wasted.
