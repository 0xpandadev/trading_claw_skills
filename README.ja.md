# trading_claw_skills

AIエージェント向けの、実務レベルなトレーディング / 投資スキル集です。

[English](README.md) | [中文](README.zh.md)

## このリポジトリの目的

一般的な「投資アドバイス系プロンプト」は再現性が低く、改善しづらいです。  
このリポジトリは分析手順をスキルとして構造化し、次を実現するために作っています。

- 出力品質の安定
- 分析ロジックの再利用
- 検証と改善のしやすさ

## 含まれる内容

現在 **54スキル** を収録しています。主な領域は次のとおりです。

- 市場・テクニカル分析
- 銘柄発掘・スクリーニング
- 決算・イベント・カタリスト分析
- リスク管理・ポートフォリオ運用
- エッジ発見パイプライン

各スキルには通常、以下が含まれます。

- `SKILL.md`（実行仕様）
- `references/`（方法論・チェックリスト）
- 必要に応じて `scripts/`, `assets/`, `agents/`

## カテゴリ別スキル

### 1. 市場・テクニカル分析

- `technical-analyst`
- `market-breadth-analyzer`
- `uptrend-analyzer`
- `macro-regime-detector`
- `sector-analyst`
- `theme-detector`

### 2. 銘柄発掘・スクリーニング

- `canslim-screener`
- `vcp-screener`
- `value-dividend-screener`
- `pead-screener`
- `pair-trade-screener`
- `tenbagger-screener`
- `buffett-value-evaluator`

### 3. 決算・イベント・カタリスト

- `earnings-calendar`
- `earnings-trade-analyzer`
- `economic-calendar-fetcher`
- `institutional-flow-tracker`

### 4. リスク管理・ポートフォリオ・実行

- `position-sizer`
- `portfolio-manager`
- `exposure-coach`
- `scenario-analyzer`
- `signal-postmortem`
- `trader-memory-core`

### 5. エッジ発見パイプライン

- `edge-candidate-agent`
- `edge-concept-synthesizer`
- `edge-hint-extractor`
- `edge-strategy-designer`
- `edge-strategy-reviewer`
- `edge-pipeline-orchestrator`
- `edge-signal-aggregator`

## クイックスタート（Codex / Claude Code）

1. `skills/` から必要なスキルフォルダをローカルの skills ディレクトリへコピー
2. エージェントを再起動
3. スキル名で呼び出し（例: `$technical-analyst`, `$tenbagger-screener`）

## 利用例

### テンバガー候補探索

```text
$tenbagger-screener
米国株と日本株を対象にテンバガー候補をスクリーニング。
上位15銘柄をスコア順で出し、上位3銘柄はbull/base/bearで深掘り。
```

### バフェット流の評価

```text
$buffett-value-evaluator
この8銘柄を moat、経営、owner earnings、財務安全性、
margin of safety で評価して、確信度順に並べて。
```

## このリポジトリの強み

- **プロセス重視**: 出力文体ではなく分析手順をスキル化
- **根拠重視**: references / scripts による再現性
- **組み合わせ可能**: 複数スキルを連携して運用可能
- **拡張しやすい**: スキル単位で改善できる

## 構成

- `skills/` - スキル本体
- `LICENSE` - ライセンス
- `README.md` / `README.ja.md` / `README.zh.md` - 多言語ドキュメント

## 今後の改善

- スキル品質評価用ベンチマークの強化
- スコアリングの校正ルール統一
- API連携型データパイプラインのガイド追加

## 貢献歓迎

特に以下のPRを歓迎します。

- 方法論の改善
- script テスト強化
- 多言語ドキュメント品質改善
- 高シグナルな新規スキル追加

## 免責

本リポジトリは研究・教育目的です。  
投資助言ではありません。最終判断は自己責任で行ってください。
