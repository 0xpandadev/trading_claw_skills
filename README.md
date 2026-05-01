# trading_claw_skills

Production-grade trading and investing skill pack for AI coding agents.

[日本語版はこちら](README.ja.md) | [中文说明在这里](README.zh.md)

## Why this repo exists

Most trading prompts are generic and non-repeatable.  
This repository provides a structured, reusable skill system so agent outputs become:

- more consistent
- more testable
- easier to improve over time

Instead of one-off advice, you get workflow-driven analysis with reusable references, scripts, and templates.

## What's inside

This repository currently includes **54 skills** across:

- market and technical analysis
- screening and idea generation
- earnings, events, and catalyst workflows
- risk, portfolio, and execution support
- edge research pipeline orchestration

Each skill folder contains:

- `SKILL.md` (execution instructions)
- `references/` (frameworks, methods, checklists)
- optional `scripts/`, `assets/`, `agents/`

## Skill categories

### 1. Market and technical analysis

- `technical-analyst`
- `market-breadth-analyzer`
- `uptrend-analyzer`
- `macro-regime-detector`
- `sector-analyst`
- `theme-detector`

### 2. Screening and idea generation

- `canslim-screener`
- `vcp-screener`
- `value-dividend-screener`
- `pead-screener`
- `pair-trade-screener`
- `tenbagger-screener`
- `buffett-value-evaluator`

### 3. Earnings, events, and catalysts

- `earnings-calendar`
- `earnings-trade-analyzer`
- `economic-calendar-fetcher`
- `institutional-flow-tracker`

### 4. Risk, portfolio, and execution

- `position-sizer`
- `portfolio-manager`
- `exposure-coach`
- `scenario-analyzer`
- `signal-postmortem`
- `trader-memory-core`

### 5. Edge pipeline and research ops

- `edge-candidate-agent`
- `edge-concept-synthesizer`
- `edge-hint-extractor`
- `edge-strategy-designer`
- `edge-strategy-reviewer`
- `edge-pipeline-orchestrator`
- `edge-signal-aggregator`

## Quick start (Codex / Claude Code style)

1. Copy desired skill folders from `skills/` into your local skills directory.
2. Restart your agent runtime.
3. Invoke by skill name (for example: `$technical-analyst`, `$tenbagger-screener`).

## Example prompts

### Tenbagger discovery

```text
$tenbagger-screener
Screen US + Japan stocks for potential 10x candidates.
Rank top 15 by score, then deep-dive top 3 with bull/base/bear scenarios.
```

### Buffett-style quality-value review

```text
$buffett-value-evaluator
Evaluate these 8 stocks with moat, management, owner earnings, balance-sheet safety,
and margin-of-safety logic. Rank by conviction.
```

### Market regime + position sizing

```text
$macro-regime-detector
Detect current US macro regime and assign confidence.

$position-sizer
Given my entry/stop and risk budget, calculate position size and constraint impact.
```

## What makes this different

- **Workflow-first**: skills encode process, not just output style.
- **Evidence-aware**: references and scripts reduce hand-wavy analysis.
- **Composable**: combine skills into your own pipeline.
- **Upgradable**: each skill can evolve independently.

## Repository structure

- `skills/` - all skill folders
- `LICENSE` - repository license
- `README.md` / `README.ja.md` / `README.zh.md` - multilingual docs

## Roadmap

- better benchmark datasets for skill quality checks
- standardized score calibration across screeners
- optional integration guides for API-backed data pipelines

## Contributing

PRs are welcome, especially for:

- methodology improvements
- test additions for scripts
- multilingual docs quality
- new high-signal trading/investing skills

## Disclaimer

This project is for research and education.  
It is **not** investment advice.  
Always do your own due diligence and risk management.
