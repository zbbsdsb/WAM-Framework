# DSH preset sync — how a stage gets its agent

## What a preset is (verified against DSH source)

A preset is a **directory**; the directory name is the preset id. It contains:

- `agent.cordis.yml` — the composition: a list of plugin rows that decide which
  tools, prompt sections, and skills this agent gets. (Required.)
- `preset.yml` — display metadata: `name`, `description`, `order`. (Optional.)
- `skills/<skill-name>/SKILL.md` — skills shipped with the preset. (Optional.)

One session composes its agent from **one** preset. So each experiment stage
selects the preset that gives it the right agent shape.

## Sync to the harness (user presets)

User presets live under the harness home: `~/.dsh/.agent-presets/<preset-id>/`
(Windows: `C:\Users\<you>\.dsh\.agent-presets\`). The directory is created on
first sync; discovery re-reads the root on every call, so **no restart needed**.

PowerShell (from this repo):

```powershell
$dest = Join-Path $env:USERPROFILE ".dsh\.agent-presets"
New-Item -ItemType Directory -Force -Path $dest | Out-Null
Copy-Item -Recurse -Force "experiments\<path-id>\dsh\presets\<preset-id>" (Join-Path $dest "<preset-id>")
```

Then pick the preset in the harness session/preset picker. Verify it appears:

```powershell
Get-ChildItem (Join-Path $env:USERPROFILE ".dsh\.agent-presets")
```

## Authoring a preset for a stage

Start from the example at `dsh/presets/_example/`:

- Copy `_example` to `<preset-id>` (your stage's id).
- Edit `agent.cordis.yml`: set the persona text (stage name, protocol
  instructions), keep or drop tool rows, add skills.
- Edit `preset.yml`: name/description/order.
- Sync as above and select it in a fresh session.

## Notes

- Rows reference packages like `@deepseek-ai/dsh-tool-*`; `cordis:group` groups
  rows behind an `isolate` realm (per-session services must be isolated — a
  service row outside a group with `isolate` is rejected at mount).
- `!!js process.platform === 'win32'` disables a row conditionally (the shipped
  `code` preset uses this to pick bash vs pwsh).
- Skills directories are discovered from the preset's `skills/` folder.
