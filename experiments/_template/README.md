# Experiment Path: <path-id>

> Status: OPEN · Weight: <critical path / enhancement / noise> · Opened: <date> · Attached direction: <directions/<name> or standalone>

## Hypothesis (one line)

<What claim does this experiment path test? One sentence.>

## Local conclusion (局部性结论)

<The ONE bounded judgment this path exists to produce. Per the manifesto
(experiments/README.md): this path is NOT a complete path — it stops when this
local conclusion is reached (pass / falsified / partial) and archives. State
the conclusion in a checkable form, e.g. "mechanism X works / does not work
under condition Y", "design choice Z is validated / falsified", "unknown-
unknown W became known".>

## What would falsify this

<The observable outcome that would prove the hypothesis wrong. Must be checkable from stage results.>

## Stage table

| Stage | Focus | DoD | Status | Evidence |
|---|---|---|---|---|
| 01-<name> | <what it tests> | <definition of done> | not started | — |
| 02-<name> | … | … | not started | — |

## DSH integration

- Preset id(s): `<preset-id>` (see `dsh/presets/`), one per stage or one shared
- Select: sync via `dsh/SYNC.md`, then pick the preset in the harness session picker

## Work log

- <date>: opened.
