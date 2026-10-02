# Academic Research Skills — ZCode Edition

[![Upstream](https://img.shields.io/badge/upstream-academic--research--skills-blue)](https://github.com/Imbad0202/academic-research-skills)
[![Version](https://img.shields.io/badge/version-3.22.2-blue)](./.zcode-plugin/plugin.json)
[![License: CC BY-NC 4.0](https://img.shields.io/badge/license-CC%20BY--NC%204.0-lightgrey)](./LICENSE)

ZCode plugin adaptation of [academic-research-skills](https://github.com/Imbad0202/academic-research-skills) v3.22.2 (upstream targets Claude Code), installable from the ZCode plugin marketplace. Full documentation in [README.zh-CN.md](./README.zh-CN.md).

A contract-audited academic research pipeline: **research → write → integrity check → peer review → revise → re-review → finalize**.

## Install in ZCode

1. Open **Plugin Marketplace** → **Add → Add Plugin Marketplace**, paste this repository's GitHub URL (or the local repo root directory containing `marketplace.json`).
2. Under **Personal**, find market **academic-research-skills-zcode** → **Academic Research Skills (ZCode)** → **Install**.
3. Manage it later under **Settings → Plugins**.

## Skills

| Skill | Purpose |
|---|---|
| `deep-research` | 13-agent deep research pipeline: question formulation, systematic search, source verification, synthesis, meta-analysis, fact-checking (8 modes) |
| `academic-paper` | 12-agent paper writing pipeline (11 modes): outline, drafting, abstracts, lit reviews, format conversion, citation checks, AI disclosure, rebuttal audit |
| `academic-paper-reviewer` | 5-seat role-separated simulated peer review panel with calibration modes |
| `academic-pipeline` | End-to-end 10-stage orchestrator from research to final paper |

16 `/ars-*` slash commands are included (see the Chinese README for the full list).

## Requirements

- Python 3 (optional — the plugin degrades gracefully without it); network access for scholarly APIs; pandoc/LaTeX only for those output formats.

## Adaptation notes

Minimal-diff adaptation of upstream v3.22.2: skill content is byte-identical. Changes: ZCode-native `.zcode-plugin/plugin.json` + root-level `marketplace.json`, skill-reference prefixes renamed to `academic-research-skills-zcode:` in the 16 command files and the session-start announce script, upstream dev-only assets (evals, tests, audits, CI) excluded, upstream `skills/` symlink directory dropped in favor of explicit manifest declarations. Hooks (`SessionStart`, `PreToolUse`) and `${CLAUDE_PLUGIN_ROOT}` are supported by ZCode as-is.

## Attribution & license

Upstream author: [Cheng-I Wu (Imbad0202)](https://github.com/Imbad0202). Released under **CC BY-NC 4.0** — see [LICENSE](./LICENSE), [NOTICE.md](./NOTICE.md), [THIRD_PARTY.md](./THIRD_PARTY.md).
