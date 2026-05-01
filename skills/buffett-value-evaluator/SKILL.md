---
name: buffett-value-evaluator
description: Evaluate stocks with a Buffett-style framework across moat quality, management discipline, capital efficiency, owner earnings, leverage safety, and margin of safety valuation.
---

# Buffett Value Evaluator

Use this skill to evaluate whether a company fits a long-duration quality-value profile inspired by Buffett principles.

## When To Use

Use when the user asks for:

- Buffett-style stock evaluation
- moat and management quality analysis
- quality compounder at reasonable price
- margin of safety checks

## Inputs

- company list or single ticker
- required margin of safety target
- preferred holding period
- optional excluded industries

## Workflow

1. Assess business understandability and moat profile.
2. Assess management quality and capital allocation behavior.
3. Normalize financials to estimate owner-earnings quality.
4. Assess leverage safety and downside fragility.
5. Estimate intrinsic value range and margin of safety.
6. Output conviction, watch triggers, and pass/fail reasons.

Read [references/buffett-framework.md](references/buffett-framework.md) for scoring and thresholds.

## Hard Pass Rules

Pass on the name if any apply:

- persistent value destruction from capital allocation despite good narrative
- balance sheet fragility inconsistent with long holding durability
- accounting opacity that blocks owner-earnings confidence
- valuation has no margin of safety under conservative assumptions

## Output Format

### Buffett Fit Table

| Ticker | Buffett Fit Score | Moat | Management | Owner Earnings | Balance Sheet | Margin Of Safety |
|---|---:|---|---|---|---|---|

### Investment Memo (Top Names)

1. Business quality verdict
2. Management and allocation verdict
3. Intrinsic value range and margin of safety
4. What would invalidate the thesis
5. Hold-or-wait decision

## Important Rules

- Be conservative in assumptions.
- Do not force valuation precision when uncertainty is high.
- Explicitly separate `great business`, `fair business`, and `speculative turnaround`.

