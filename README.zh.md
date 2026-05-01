# trading_claw_skills

面向 AI Agent 的实战级交易与投资技能库。

[English](README.md) | [日本語](README.ja.md)

## 项目目标

很多“投资建议型提示词”缺乏可复用性和可验证性。  
本仓库将分析流程结构化为技能（Skill），目标是：

- 稳定输出质量
- 复用分析框架
- 便于持续优化

## 仓库内容

当前共收录 **54 个技能**，覆盖以下方向：

- 市场与技术分析
- 选股与机会发现
- 财报、事件与催化剂分析
- 风险管理与组合执行
- Edge 研究流水线

每个技能目录通常包含：

- `SKILL.md`（执行规范）
- `references/`（方法论、清单、模板）
- 可选 `scripts/`, `assets/`, `agents/`

## 技能分类

### 1. 市场与技术分析

- `technical-analyst`
- `market-breadth-analyzer`
- `uptrend-analyzer`
- `macro-regime-detector`
- `sector-analyst`
- `theme-detector`

### 2. 选股与机会发现

- `canslim-screener`
- `vcp-screener`
- `value-dividend-screener`
- `pead-screener`
- `pair-trade-screener`
- `tenbagger-screener`
- `buffett-value-evaluator`

### 3. 财报、事件与催化剂

- `earnings-calendar`
- `earnings-trade-analyzer`
- `economic-calendar-fetcher`
- `institutional-flow-tracker`

### 4. 风险管理、组合与执行

- `position-sizer`
- `portfolio-manager`
- `exposure-coach`
- `scenario-analyzer`
- `signal-postmortem`
- `trader-memory-core`

### 5. Edge 研究流水线

- `edge-candidate-agent`
- `edge-concept-synthesizer`
- `edge-hint-extractor`
- `edge-strategy-designer`
- `edge-strategy-reviewer`
- `edge-pipeline-orchestrator`
- `edge-signal-aggregator`

## 快速开始（Codex / Claude Code）

1. 将 `skills/` 中需要的技能目录复制到本地 skills 目录  
2. 重启 Agent 运行环境  
3. 用技能名调用（例如：`$technical-analyst`, `$tenbagger-screener`）

## 使用示例

### 十倍股候选筛选

```text
$tenbagger-screener
在美股和日股中筛选潜在十倍股。
按评分输出前15只，并对前3只做 bull/base/bear 场景分析。
```

### 巴菲特风格估值评估

```text
$buffett-value-evaluator
对这8只股票按 moat、管理层、owner earnings、资产负债安全性、
安全边际进行评估，并按置信度排序。
```

## 仓库优势

- **流程优先**：不是只改文风，而是固化分析流程
- **证据导向**：references / scripts 提升可验证性
- **可组合**：多个技能可串联成完整工作流
- **可演进**：按技能模块逐步升级

## 目录结构

- `skills/` - 技能目录
- `LICENSE` - 许可证
- `README.md` / `README.ja.md` / `README.zh.md` - 多语言文档

## 路线图

- 强化技能质量评测基准
- 统一筛选器评分校准规则
- 增加 API 数据流水线接入指南

## 欢迎贡献

欢迎以下方向的 PR：

- 方法论优化
- scripts 测试补强
- 多语言文档质量提升
- 高信号新技能补充

## 免责声明

本项目仅用于研究与教育。  
不构成任何投资建议。请自行判断并做好风险管理。
