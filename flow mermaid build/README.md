# Flow Chart Style — Claude Code Skill

House visual style for **Mermaid flowcharts**: pill / rounded-card / diamond
nodes, five semantic arrow colours, tinted group frames, no shadows, `basis`
curves.

Self-contained. The fast path is **`build_flow.py`**: hand it a plain
`flowchart` and it returns a fully-styled, validated, rendered SVG (and PNG) —
node classes assigned, `linkStyle` auto-numbered by edge order, group frames
drawn, Kroki's shadow bug stripped. Also ships a portable Mermaid config
(`flow-chart.mermaid.json`), a copy-paste style block, and `render.sh`.

```
flow-chart-style-skill/
├─ .claude-plugin/
│  ├─ plugin.json          # plugin manifest
│  └─ marketplace.json     # this repo doubles as a 1-plugin marketplace
├─ skills/
│  └─ flow-chart-style/
│     ├─ SKILL.md          # the skill
│     ├─ build_flow.py     # plain flowchart -> styled + validated + rendered
│     ├─ flow-chart.mermaid.json
│     ├─ render.sh
│     ├─ templates/flow_template.mmd
│     └─ examples/flow_sample.mmd, flow_pipeline.mmd, requirement_flow.mmd
└─ README.md
```

## Before publishing

Set the author / `homepage` / `owner` fields in `.claude-plugin/plugin.json` and
`.claude-plugin/marketplace.json` to your GitHub account and repo, then push
this folder to that repo (e.g. `github.com/<you>/flow-chart-style`).

## Install — Method A: as a plugin (recommended, updatable)

```
/plugin marketplace add <you>/flow-chart-style
/plugin install flow-chart-style@flow-chart
```

Or from the CLI:

```
claude plugin marketplace add <you>/flow-chart-style
claude plugin install flow-chart-style@flow-chart
```

Update later with `claude plugin update flow-chart-style@flow-chart`.

## Install — Method B: as a personal skill (copy, no plugin system)

```
git clone https://github.com/<you>/flow-chart-style
cp -r flow-chart-style/skills/flow-chart-style ~/.claude/skills/
```

## Install — Method C: as a project skill (share with a repo)

```
cp -r flow-chart-style/skills/flow-chart-style <your-project>/.claude/skills/
```

Commit it so everyone on the project gets it.

## Use

After install the command is **`/flow-chart-style`** (it is *not* the global
`/mermaid-skill` — that is a separate, general diagram skill). Ask for a
flowchart and mention the style, or invoke it directly:

```
/flow-chart-style
畫一張使用者註冊流程圖，套用 flow-chart 樣式
```

It also triggers on phrases like "Flow Chart style", "flow_chart_style",
"套用 Flow Chart 樣式".

### One-shot with the script

Write a plain `flowchart` (optionally with `%% @…` hints), then:

```bash
python3 skills/flow-chart-style/build_flow.py diagram.mmd          # -> diagram.styled.mmd + diagram.svg
python3 skills/flow-chart-style/build_flow.py diagram.mmd --png    # also a PNG preview
python3 skills/flow-chart-style/build_flow.py diagram.mmd --stdout # print styled .mmd only
```

## Requirements

- **`python3`** (standard library only) — for `build_flow.py`.
- **`curl`** — Kroki export route (no install). Used when `mmdc` is absent.
- Optional: **`mmdc`** (`npm i -g @mermaid-js/mermaid-cli`) — local rendering,
  correct CJK font metrics, direct PNG/PDF.
- Optional: **Google Chrome / Chromium** (+ `python3-Pillow` for `render.sh`'s
  trim) — PNG output on the Kroki route.

## License

MIT. See `LICENSE`.
