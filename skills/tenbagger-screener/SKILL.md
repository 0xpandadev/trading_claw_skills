---
name: tenbagger-screener
description: Find potential multibagger stocks using a structured scoring model across growth runway, reinvestment quality, financial durability, valuation setup, and catalyst timing.
---

# Tenbagger Screener

Use this skill to find high-upside stocks that could compound into outsized winners over 5-10 years.

This is not a hype filter. It is a disciplined multibagger screening and ranking workflow.

## When To Use

Use when the user asks for:

- tenbagger candidates
- multibagger screens
- high-upside growth stocks with quality filters
- cheap stocks with asymmetrical upside

## Inputs

- market (`US`, `JP`, `CN`, or mixed)
- style preference (`quality growth`, `deep value turnaround`, `balanced`)
- holding horizon (`3y`, `5y`, `10y`)
- risk tolerance (`low`, `medium`, `high`)
- optional sector constraints

## Workflow

1. Build candidate universe from watchlist or broad screen.
2. Apply hard exclusion rules first.
3. Score each remaining name using the Tenbagger Score model.
4. Run scenario stress (`bull`, `base`, `bear`) and estimate payoff asymmetry.
5. Rank names and output diligence priority.

Read [references/tenbagger-model.md](references/tenbagger-model.md) for scoring details.

## Hard Exclusion Rules

Exclude if any are true:

- severe accounting red flags not explainable by business model
- unsustainable refinancing risk within 18 months without credible liquidity plan
- persistent dilution spiral with no path to self-funded growth
- thesis depends only on narrative without measurable business drivers

## Output Format

### Screen Summary

- universe size
- excluded count and reasons
- final ranked candidates

### Ranked Candidates Table

| Rank | Ticker | Tenbagger Score | Upside Profile | Main Risk | Trigger |
|---|---|---:|---|---|---|

### Candidate Card (for top names)

1. Why this could 10x
2. Key metrics that must hold
3. What the market may be missing
4. Disconfirming evidence to watch
5. 90-day catalyst map

## Important Rules

- Separate discovery from conviction. A high screen score is not a buy signal by itself.
- Always include disconfirming indicators.
- Prefer fewer high-quality candidates over long low-signal lists.

