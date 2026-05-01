# Trading Claw Skills: Detailed Guide

This guide explains each skill with practical usage and expected outcomes.

- Total skills: 54
- Invocation: `[$skill-name](skills/<skill-name>/SKILL.md)` or call in chat as `$skill-name`
- Best practice: always specify market scope, horizon, constraints, and risk tolerance

## backtest-expert
- What it does: Expert guidance for systematic backtesting of trading strategies. Use when developing, testing, stress-testing, or validating quantitative trading strategies. Covers "beating ideas to death" methodology, parameter robustness testing, slippage modeling, bias prevention, and interpreting backtest results. Applicable when user asks about backtesting, strategy validation, robustness testing, avoiding overfitting, or systematic trading development.
- When to use: Use this skill when: / - Developing or validating systematic trading strategies / - Evaluating whether a trading idea is robust enough for live implementation / - Troubleshooting why a backtest might be misleading
- How to use (inputs): - Python 3.9+ (for evaluation script) / - No API keys required / - No external data dependencies metrics are user-provided
- Process summary: ### 1. State the Hypothesis / Define the edge in one sentence. / **Example**: "Stocks that gap up >3% on earnings and pull back to previous day's close within first hour provide mean-reversion opportunity."
- Expected effect: - `reports/backtest_eval_<timestamp>.json` structured evaluation with per-dimension scores, red flags, and verdict / - `reports/backtest_eval_<timestamp>.md` human-readable report with dimension table, key metrics, and red flag details
- Example call: `$backtest-expert run with US/JP scope and explicit constraints`

## breadth-chart-analyst
- What it does: This skill should be used when analyzing market breadth charts, specifically the S&P 500 Breadth Index (200-Day MA based) and the US Stock Market Uptrend Stock Ratio charts. Use this skill when the user provides breadth chart images for analysis, requests market breadth assessment, positioning strategy recommendations, or wants to understand medium-term strategic and short-term tactical market outlook based on breadth indicators. Also works WITHOUT chart images by fetching CSV data directly from public sources. All analysis and output are conducted in English.
- When to use: Use this skill when: / - User provides S&P 500 Breadth Index (200-Day MA based) chart images for analysis / - User provides US Stock Market Uptrend Stock Ratio chart images for analysis / - User requests market breadth assessment or market health evaluation
- How to use (inputs): - **Chart Images Optional**: CSV data from public sources is the PRIMARY data source; chart images provide supplementary visual context / - **No API Keys Required**: CSV data is fetched from public GitHub Pages; no external API subscriptions needed / - **Language**: All analysis and output conducted in English
- Process summary: ### Step 0: Fetch CSV Data (PRIMARY SOURCE - MANDATORY) / **CRITICAL**: CSV data is the PRIMARY source for all Breadth values. This step MUST be executed BEFORE any image analysis. / ```bash
- Expected effect: This skill generates markdown analysis reports saved to the `reports/` directory: / - Chart 1 only: `breadth_200ma_analysis_[YYYY-MM-DD].md` / - Chart 2 only: `uptrend_ratio_analysis_[YYYY-MM-DD].md` / - Both charts: `breadth_combined_analysis_[YYYY-MM-DD].md`
- Example call: `$breadth-chart-analyst run with US/JP scope and explicit constraints`

## breakout-trade-planner
- What it does: Generate Minervini-style breakout trade plans from VCP screener output with worst-case risk calculation, portfolio heat management, and Alpaca-compatible order templates (stop-limit bracket for pre-placement, limit bracket for post-confirmation). Use when user has VCP screener results and wants actionable trade plans with entry/stop/target levels and position sizing.
- When to use: - User has VCP screener JSON output and wants trade plans / - User asks for breakout entry/stop/target calculation / - User wants Alpaca order templates for VCP breakout candidates / - User needs position sizing with portfolio heat management
- How to use (inputs): - VCP screener JSON output with `schema_version: "1.0"` / - No API keys required (works with local JSON files) / - No external skill dependencies (position sizing is built-in)
- Process summary: ### Step 1: Generate Trade Plans / Run the planner with VCP screener output: / ```bash
- Expected effect: - `breakout_trade_plan_YYYY-MM-DD_HHMMSS.json` Structured plans with order templates / - `breakout_trade_plan_YYYY-MM-DD_HHMMSS.md` Human-readable report
- Example call: `$breakout-trade-planner run with US/JP scope and explicit constraints`

## buffett-value-evaluator
- What it does: Evaluate stocks with a Buffett-style framework across moat quality, management discipline, capital efficiency, owner earnings, leverage safety, and margin of safety valuation.
- When to use: Use when the user asks for: / - Buffett-style stock evaluation / - moat and management quality analysis / - quality compounder at reasonable price
- How to use (inputs): - company list or single ticker / - required margin of safety target / - preferred holding period / - optional excluded industries
- Process summary: 1. Assess business understandability and moat profile. / 2. Assess management quality and capital allocation behavior. / 3. Normalize financials to estimate owner-earnings quality.
- Expected effect: ### Buffett Fit Table / | Ticker | Buffett Fit Score | Moat | Management | Owner Earnings | Balance Sheet | Margin Of Safety | / |---|---:|---|---|---|---|---| / ### Investment Memo (Top Names)
- Example call: `$buffett-value-evaluator run with US/JP scope and explicit constraints`

## canslim-screener
- What it does: Screen US stocks using William O'Neil's CANSLIM growth stock methodology. Use when user requests CANSLIM stock screening, growth stock analysis, momentum stock identification, or wants to find stocks with strong earnings and price momentum following O'Neil's investment system.
- When to use: **Explicit Triggers:** / - "Find CANSLIM stocks" / - "Screen for growth stocks using O'Neil's method" / - "Which stocks have strong earnings and momentum?"
- How to use (inputs): **API Requirements:** / - **FMP API key** (free tier: 250 calls/day, sufficient for 35 stocks; Starter tier $29.99/mo for 40+ stocks) / - Sign up: https://site.financialmodelingprep.com/developer/docs / - Set via environment variable: `export FMP_API_KEY=your_key_here`
- Process summary: ### Step 1: Verify API Access and Requirements / Check if user has FMP API key configured: / ```bash
- Expected effect: **Output Directory:** `reports/` (default) or custom via `--output-dir` / **Generated Files:** / - `canslim_screener_YYYY-MM-DD_HHMMSS.json` - Structured data for programmatic use / - `canslim_screener_YYYY-MM-DD_HHMMSS.md` - Human-readable report
- Example call: `$canslim-screener run with US/JP scope and explicit constraints`

## data-quality-checker
- What it does: Validate data quality in market analysis documents and blog articles before publication. Use when checking for price scale inconsistencies (ETF vs futures), instrument notation errors, date/day-of-week mismatches, allocation total errors, and unit mismatches. Supports English and Japanese content. Advisory mode -- flags issues as warnings for human review, not as blockers.
- When to use: - Before publishing a weekly strategy blog or market analysis report / - After generating automated market summaries / - When reviewing translated documents (English/Japanese) for data accuracy / - When combining data from multiple sources (FRED, FMP, FINVIZ) into one report
- How to use (inputs): - Python 3.9+ / - No external API keys required / - No third-party Python packages required (uses only standard library)
- Process summary: ### Step 1: Receive Input Document / Accept the target markdown file path and optional parameters: / - `--file`: Path to the markdown document to validate (required)
- Expected effect: ### JSON Finding Structure / ```json / { / "severity": "WARNING",
- Example call: `$data-quality-checker run with US/JP scope and explicit constraints`

## dividend-growth-pullback-screener
- What it does: Use this skill to find high-quality dividend growth stocks (12%+ annual dividend growth, 1.5%+ yield) that are experiencing temporary pullbacks, identified by RSI oversold conditions (RSI 40). This skill combines fundamental dividend analysis with technical timing indicators to identify buying opportunities in strong dividend growers during short-term weakness.
- When to use: Use this skill when: / - Looking for dividend growth stocks with exceptional compounding potential (12%+ dividend CAGR) / - Seeking entry opportunities in quality stocks during temporary market weakness / - Willing to accept lower current yields (1.5-3%) for higher dividend growth
- How to use (inputs): - **FMP API key** (required): Set `FMP_API_KEY` environment variable or pass `--fmp-api-key`. Free tier (250 calls/day) is sufficient for FMP-only mode ( 40 stocks). [Sign up](https://site.financialmodelingprep.com/developer/docs). / - **FINVIZ Elite API key** (optional, recommended): Set `FINVIZ_API_KEY` environment variable or pass `--finviz-api-key`. Reduces execution time from 10 5 min to 2 min. [Sign up](https://elite.finviz.com/). / - Python 3.8+ with `requests` and `pandas` libraries installed.
- Process summary: Collect inputs -> run framework -> synthesize evidence -> propose actions.
- Expected effect: The script saves two files to the current working directory (or `--output-dir` if specified): / | File | Description | / |---|---| / | `dividend_growth_pullback_results_YYYY-MM-DD.json` | Structured data with all metrics (yield, dividend CAGR, RSI, composite score, etc.) |
- Example call: `$dividend-growth-pullback-screener run with US/JP scope and explicit constraints`

## downtrend-duration-analyzer
- What it does: Analyze historical downtrend durations and generate interactive HTML histograms showing typical correction lengths by sector and market cap.
- When to use: - Trader asks about typical correction lengths for a sector or market cap tier / - User wants to understand historical drawdown recovery times / - Building mean reversion or pullback strategies that need realistic holding period estimates / - Comparing correction behavior across different market segments
- How to use (inputs): - Python 3.9+ / - FMP API key (set `FMP_API_KEY` environment variable or use `--api-key`) / - Required packages: `requests`, `pandas`, `numpy` (standard data analysis stack)
- Process summary: ### Step 1: Fetch Historical Price Data / Run the analysis script to fetch OHLC data for a universe of stocks and identify downtrend periods. / ```bash
- Expected effect: ### JSON Report / ```json / { / "schema_version": "1.0",
- Example call: `$downtrend-duration-analyzer run with US/JP scope and explicit constraints`

## dual-axis-skill-reviewer
- What it does: "Review skills in any project using a dual-axis method: (1) deterministic code-based checks (structure, scripts, tests, execution safety) and (2) LLM deep review findings. Use when you need reproducible quality scoring for `skills/*/SKILL.md`, want to gate merges with a score threshold (for example 90+), or need concrete improvement items for low-scoring skills. Works across projects via --project-root."
- When to use: - Need reproducible scoring for one skill in `skills/*/SKILL.md`. / - Need improvement items when final score is below 90. / - Need both deterministic checks and qualitative LLM code/content review. / - Need to review skills in a **different project** from the command line.
- How to use (inputs): - Python 3.9+ / - `uv` (recommended auto-resolves `pyyaml` dependency via inline metadata) / - For tests: `uv sync --extra dev` or equivalent in the target project / - For LLM-axis merge: JSON file that follows the LLM review schema (see Resources)
- Process summary: Determine the correct script path based on your context: / - **Same project**: `skills/dual-axis-skill-reviewer/scripts/run_dual_axis_review.py` / - **Global install**: `~/.claude/skills/dual-axis-skill-reviewer/scripts/run_dual_axis_review.py`
- Expected effect: - `reports/skill_review_<skill>_<timestamp>.json` / - `reports/skill_review_<skill>_<timestamp>.md` / - `reports/skill_review_prompt_<skill>_<timestamp>.md` (when `--emit-llm-prompt` is enabled)
- Example call: `$dual-axis-skill-reviewer run with US/JP scope and explicit constraints`

## earnings-calendar
- What it does: This skill retrieves upcoming earnings announcements for US stocks using the Financial Modeling Prep (FMP) API. Use this when the user requests earnings calendar data, wants to know which companies are reporting earnings in the upcoming week, or needs a weekly earnings review. The skill focuses on mid-cap and above companies (over $2B market cap) that have significant market impact, organizing the data by date and timing in a clean markdown table format. Supports multiple environments (CLI, Desktop, Web) with flexible API key management.
- When to use: Use when you need structured analysis, ranking, or decision support for this domain.
- How to use (inputs): ### FMP API Key / This skill requires a Financial Modeling Prep API key. / **Get Free API Key**: / 1. Visit: https://site.financialmodelingprep.com/developer/docs
- Process summary: Collect inputs -> run framework -> synthesize evidence -> propose actions.
- Expected effect: Actionable output with rankings, key findings, and next-step recommendations.
- Example call: `$earnings-calendar run with US/JP scope and explicit constraints`

## earnings-trade-analyzer
- What it does: Analyze recent post-earnings stocks using a 5-factor scoring system (Gap Size, Pre-Earnings Trend, Volume Trend, MA200 Position, MA50 Position). Scores each stock 0-100 and assigns A/B/C/D grades. Use when user asks about earnings trade analysis, post-earnings momentum screening, earnings gap scoring, or finding best recent earnings reactions.
- When to use: - User asks for post-earnings trade analysis or earnings gap screening / - User wants to find the best recent earnings reactions / - User requests earnings momentum scoring or grading / - User asks about post-earnings accumulation day (PEAD) candidates
- How to use (inputs): - FMP API key (set `FMP_API_KEY` environment variable or pass `--api-key`) / - Free tier (250 calls/day) is sufficient for default screening (lookback 2 days, top 20) / - Paid tier recommended for larger lookback windows or full screening
- Process summary: ### Step 1: Run the Earnings Trade Analyzer / Execute the analyzer script: / ```bash
- Expected effect: - `earnings_trade_analyzer_YYYY-MM-DD_HHMMSS.json` - Structured results with schema_version "1.0" / - `earnings_trade_analyzer_YYYY-MM-DD_HHMMSS.md` - Human-readable report with tables
- Example call: `$earnings-trade-analyzer run with US/JP scope and explicit constraints`

## economic-calendar-fetcher
- What it does: "Fetch upcoming economic events and data releases using FMP API. Retrieve scheduled central bank decisions, employment reports, inflation data, GDP releases, and other market-moving economic indicators for specified date ranges (default: next 7 days). The script outputs raw JSON or text; the assistant filters, assesses impact, and generates the Markdown report."
- When to use: Use this skill when the user requests: / 1. **Economic Calendar Queries:** / - "What economic events are coming up this week?" / - "Show me the economic calendar for the next two weeks"
- How to use (inputs): - **FMP API Key** (required): Sign up at https://financialmodelingprep.com for a free key (250 requests/day). Set via `FMP_API_KEY` environment variable or pass `--api-key` to the script. / - **Python 3.10+**: Required to run `skills/economic-calendar-fetcher/scripts/get_economic_calendar.py`. / - **No third-party packages**: The script uses only the Python standard library.
- Process summary: Follow these steps to fetch and analyze the economic calendar: / ### Step 1: Obtain FMP API Key / **Check for API key availability (in priority order):**
- Expected effect: Actionable output with rankings, key findings, and next-step recommendations.
- Example call: `$economic-calendar-fetcher run with US/JP scope and explicit constraints`

## edge-candidate-agent
- What it does: Generate and prioritize US equity long-side edge research tickets from EOD observations, then export pipeline-ready candidate specs for trade-strategy-pipeline Phase I. Use when users ask to turn hypotheses/anomalies into reproducible research tickets, convert validated ideas into `strategy.yaml` + `metadata.json`, or preflight-check interface compatibility (`edge-finder-candidate/v1`) before running pipeline backtests.
- When to use: - Convert market observations, anomalies, or hypotheses into structured research tickets. / - Run daily auto-detection to discover new edge candidates from EOD OHLCV and optional hints. / - Export validated tickets as `strategy.yaml` + `metadata.json` for `trade-strategy-pipeline` Phase I. / - Run preflight compatibility checks for `edge-finder-candidate/v1` before pipeline execution.
- How to use (inputs): - Python 3.9+ with `PyYAML` installed. / - Access to the target `trade-strategy-pipeline` repository for schema/stage validation. / - `uv` available when running pipeline-managed validation via `--pipeline-root`.
- Process summary: 1. Run auto-detection from EOD OHLCV: / - `skills/edge-candidate-agent/scripts/auto_detect_candidates.py` / - Optional: `--hints` for human ideation input
- Expected effect: - `strategies/<candidate_id>/strategy.yaml`: Phase I-compatible strategy spec. / - `strategies/<candidate_id>/metadata.json`: provenance metadata including interface version and ticket context. / - Validation status from `scripts/validate_candidate.py` (pass/fail + reasons). / - Daily detection artifacts:
- Example call: `$edge-candidate-agent run with US/JP scope and explicit constraints`

## edge-concept-synthesizer
- What it does: Abstract detector tickets and hints into reusable edge concepts with thesis, invalidation signals, and strategy playbooks before strategy design/export.
- When to use: - You have many raw tickets and need mechanism-level structure. / - You want to avoid direct ticket-to-strategy overfitting. / - You need concept-level review before strategy drafting.
- How to use (inputs): - Python 3.9+ / - `PyYAML` / - Ticket YAML directory from detector output (`tickets/exportable`, `tickets/research_only`) / - Optional `hints.yaml`
- Process summary: 1. Collect ticket YAML files from auto-detection output. / 2. Optionally provide `hints.yaml` for context matching. / 3. Run `scripts/synthesize_edge_concepts.py`.
- Expected effect: - `edge_concepts.yaml` containing: / - concept clusters / - support statistics / - abstract thesis
- Example call: `$edge-concept-synthesizer run with US/JP scope and explicit constraints`

## edge-hint-extractor
- What it does: Extract edge hints from daily market observations and news reactions, with optional LLM ideation, and output canonical hints.yaml for downstream concept synthesis and auto detection.
- When to use: - You want to turn daily market observations into reusable hint objects. / - You want LLM-generated ideas constrained by current anomalies/news context. / - You need a clean `hints.yaml` input for concept synthesis or auto detection.
- How to use (inputs): - Python 3.9+ / - `PyYAML` / - Optional inputs from detector run: / - `market_summary.json`
- Process summary: 1. Gather observation files (`market_summary`, `anomalies`, optional news reactions). / 2. Run `scripts/build_hints.py` to generate deterministic hints. / 3. Optionally augment hints with LLM ideas via one of two methods:
- Expected effect: - `hints.yaml` containing: / - `hints` list / - generation metadata / - rule/LLM hint counts
- Example call: `$edge-hint-extractor run with US/JP scope and explicit constraints`

## edge-pipeline-orchestrator
- What it does: Orchestrate the full edge research pipeline from candidate detection through strategy design, review, revision, and export. Use when coordinating multi-stage edge research workflows end-to-end.
- When to use: - Run the full edge pipeline from tickets (or OHLCV) to exported strategies / - Resume a partially completed pipeline from the drafts stage / - Review and revise existing strategy drafts with feedback loop / - Dry-run the pipeline to preview results without exporting
- How to use (inputs): Ticker/universe, market scope, time horizon, risk constraints, and optional chart/data inputs.
- Process summary: 1. Load pipeline configuration from CLI arguments / 2. Run auto_detect stage if --from-ohlcv is provided (generates tickets from raw OHLCV data) / 3. Run hints stage to extract edge hints from market summary and anomalies
- Expected effect: All artifacts are written to `--output-dir`: / ``` / output-dir/ / pipeline_run_manifest.json
- Example call: `$edge-pipeline-orchestrator run with US/JP scope and explicit constraints`

## edge-signal-aggregator
- What it does: Aggregate and rank signals from multiple edge-finding skills (edge-candidate-agent, theme-detector, sector-analyst, institutional-flow-tracker) into a prioritized conviction dashboard with weighted scoring, deduplication, and contradiction detection.
- When to use: - After running multiple edge-finding skills and wanting a unified view / - When consolidating signals from edge-candidate-agent, theme-detector, sector-analyst, and institutional-flow-tracker / - Before making portfolio allocation decisions based on multiple signal sources / - To identify contradictions between different analysis approaches
- How to use (inputs): - Python 3.9+ / - No API keys required (processes local JSON/YAML files from other skills) / - Dependencies: `pyyaml` (standard in most environments)
- Process summary: ### Step 1: Gather Upstream Skill Outputs / Collect output files from the upstream skills you want to aggregate: / - `reports/edge_candidate_*.json` from edge-candidate-agent
- Expected effect: ### JSON Report / ```json / { / "schema_version": "1.0",
- Example call: `$edge-signal-aggregator run with US/JP scope and explicit constraints`

## edge-strategy-designer
- What it does: Convert abstract edge concepts into strategy draft variants and optional exportable ticket YAMLs for edge-candidate-agent export/validation.
- When to use: - You have `edge_concepts.yaml` and need strategy candidates. / - You want multiple variants (core/conservative/research-probe) per concept. / - You want optional exportable ticket files for interface v1 families.
- How to use (inputs): - Python 3.9+ / - `PyYAML` / - `edge_concepts.yaml` produced by concept synthesis
- Process summary: 1. Load `edge_concepts.yaml`. / 2. Choose risk profile (`conservative`, `balanced`, `aggressive`). / 3. Generate per-concept variants with hypothesis-type exit calibration.
- Expected effect: - `strategy_drafts/*.yaml` / - `strategy_drafts/run_manifest.json` / - Optional `exportable_tickets/*.yaml` for downstream `export_candidate.py`
- Example call: `$edge-strategy-designer run with US/JP scope and explicit constraints`

## edge-strategy-reviewer
- What it does: >
- When to use: - After `edge-strategy-designer` generates `strategy_drafts/*.yaml` / - Before exporting drafts to `edge-candidate-agent` via the pipeline / - When manually validating a draft strategy for edge plausibility
- How to use (inputs): - Strategy draft YAML files (output of `edge-strategy-designer`) / - Python 3.10+ with PyYAML
- Process summary: 1. Load draft YAML files from `--drafts-dir` or a single `--draft` file / 2. Evaluate each draft against 8 criteria (C1-C8) with weighted scoring / 3. Compute confidence score (weighted average of all criteria)
- Expected effect: Primary output: `review.yaml` (or `review.json`) / ```yaml / generated_at_utc: "2026-02-28T12:00:00+00:00" / source:
- Example call: `$edge-strategy-reviewer run with US/JP scope and explicit constraints`

## exposure-coach
- What it does: Generate a one-page Market Posture summary with net exposure ceiling, growth-vs-value bias, participation breadth, and new-entry-allowed vs cash-priority recommendation by integrating signals from breadth, regime, and flow analysis skills.
- When to use: - Before initiating any new stock positions to determine appropriate capital commitment / - At the start of each trading week to calibrate portfolio exposure / - When multiple market signals conflict and a unified posture is needed / - After significant macro or market events to reassess exposure ceiling
- How to use (inputs): - Python 3.9+ / - FMP API key (set `FMP_API_KEY` environment variable) for institutional-flow-tracker data / - Input JSON files from upstream skills (see Workflow Step 1) / - Standard library + `argparse`, `json`, `datetime`
- Process summary: ### Step 1: Gather Upstream Skill Outputs / Collect the most recent JSON outputs from integrated skills. Each file provides a specific signal dimension: / | Skill | Output File Pattern | Signal Provided |
- Expected effect: ### JSON Report / ```json / { / "schema_version": "1.0",
- Example call: `$exposure-coach run with US/JP scope and explicit constraints`

## finviz-screener
- What it does: Build and open FinViz screener URLs from natural language requests. Use when user wants to screen stocks, find stocks matching criteria, filter by fundamentals or technicals, or asks to open FinViz with specific conditions. Supports both Japanese and English input (e.g., " , "Find oversold large caps with high ROE").
- When to use: **Explicit Triggers:** / - " / - "Find oversold large caps near 52-week lows" / - "
- How to use (inputs): Ticker/universe, market scope, time horizon, risk constraints, and optional chart/data inputs.
- Process summary: ### Step 1: Load Filter Reference / Read the filter knowledge base: / ```bash
- Expected effect: Actionable output with rankings, key findings, and next-step recommendations.
- Example call: `$finviz-screener run with US/JP scope and explicit constraints`

## ftd-detector
- What it does: Detects Follow-Through Day (FTD) signals for market bottom confirmation using William O'Neil's methodology. Dual-index tracking (S&P 500 + NASDAQ) with state machine for rally attempt, FTD qualification, and post-FTD health monitoring. Use when user asks about market bottom signals, follow-through days, rally attempts, re-entry timing after corrections, or whether it's safe to increase equity exposure. Complementary to market-top-detector (defensive) - this skill is offensive (bottom confirmation).
- When to use: **English:** / - User asks "Is the market bottoming?" or "Is it safe to buy again?" / - User observes a market correction (3%+ decline) and wants re-entry timing / - User asks about Follow-Through Days or rally attempts
- How to use (inputs): - **FMP API Key:** Required. Set `FMP_API_KEY` environment variable or pass via `--api-key` flag. / - **Python 3.8+:** With `requests` library installed. / - **API Budget:** 4 calls per execution (well within FMP free tier of 250/day).
- Process summary: Collect inputs -> run framework -> synthesize evidence -> propose actions.
- Expected effect: Actionable output with rankings, key findings, and next-step recommendations.
- Example call: `$ftd-detector run with US/JP scope and explicit constraints`

## institutional-flow-tracker
- What it does: Use this skill to track institutional investor ownership changes and portfolio flows using 13F filings data. Analyzes hedge funds, mutual funds, and other institutional holders to identify stocks with significant smart money accumulation or distribution. Helps discover stocks before major moves by following where sophisticated investors are deploying capital.
- When to use: Use this skill when: / - Validating investment ideas (checking if smart money agrees with your thesis) / - Discovering new opportunities (finding stocks institutions are accumulating) / - Risk assessment (identifying stocks institutions are exiting)
- How to use (inputs): - **FMP API Key:** Set `FMP_API_KEY` environment variable or pass `--api-key` to scripts / - **Python 3.8+:** Required for running analysis scripts / - **Dependencies:** `pip install requests` (scripts handle missing dependencies gracefully)
- Process summary: ### Step 1: Identify Stocks with Significant Institutional Changes / Execute the main screening script to find stocks with notable institutional activity: / **Quick scan (top 50 stocks by institutional change):**
- Expected effect: All analysis generates structured markdown reports saved to repository root: / **Filename convention:** `institutional_flow_analysis_<TICKER/THEME>_<DATE>.md` / **Report sections:** / 1. Executive Summary (key findings)
- Example call: `$institutional-flow-tracker run with US/JP scope and explicit constraints`

## kanchi-dividend-review-monitor
- What it does: Monitor dividend portfolios with Kanchi-style forced-review triggers (T1-T5) and convert anomalies into OK/WARN/REVIEW states without auto-selling. Use when users ask for , 8-K , REVIEW , or periodic dividend risk checks.
- When to use: Use this skill when the user needs: / - Daily/weekly/quarterly anomaly detection for dividend holdings. / - Forced review queueing for T1-T5 risk triggers. / - 8-K/governance keyword scans tied to portfolio tickers.
- How to use (inputs): Provide normalized input JSON that follows: / - `references/input-schema.md` / If upstream data is unavailable, provide at least: / - `ticker`
- Process summary: ### 1) Normalize input dataset / Collect per ticker fields in one JSON document: / - Dividend points (latest regular, prior regular, missing/zero flag).
- Expected effect: Actionable output with rankings, key findings, and next-step recommendations.
- Example call: `$kanchi-dividend-review-monitor run with US/JP scope and explicit constraints`

## kanchi-dividend-sop
- What it does: Convert Kanchi-style dividend investing into a repeatable US-stock operating procedure. Use when users ask for dividend screening, dividend growth quality checks, PERxPBR adaptation for US sectors, pullback limit-order planning, or one-page stock memo creation. Covers screening, deep dive, entry planning, and post-purchase monitoring cadence.
- When to use: Use this skill when the user needs: / - Kanchi-style dividend stock selection adapted for US equities. / - A repeatable screening and pullback-entry process instead of ad-hoc picks. / - One-page underwriting memos with explicit invalidation conditions.
- How to use (inputs): ### API Key Setup / The entry signal script requires FMP API access: / ```bash / export FMP_API_KEY=your_api_key_here
- Process summary: ### 1) Define mandate before screening / Collect and lock the parameters first: / - Objective: current cash income vs dividend growth.
- Expected effect: Return and/or generate: / 1. SOP screening summary in markdown. / 2. Underwriting memo set based on / `references/stock-note-template.md`.
- Example call: `$kanchi-dividend-sop run with US/JP scope and explicit constraints`

## kanchi-dividend-us-tax-accounting
- What it does: Provide US dividend tax and account-location workflow for Kanchi-style income portfolios. Use when users ask about qualified vs ordinary dividends, 1099-DIV interpretation, REIT/BDC distribution treatment, holding-period checks, or taxable-vs-IRA account placement decisions for dividend assets.
- When to use: Use this skill when the user needs: / - US dividend tax classification planning (qualified vs ordinary assumptions). / - Holding-period checks before year-end tax planning. / - Account-location decisions for stock/REIT/BDC/MLP income holdings.
- How to use (inputs): Prepare holding-level inputs: / - `ticker` / - `instrument_type` / - `account_type`
- Process summary: ### 1) Classify each distribution stream / For each holding, classify expected cash flow into: / - Potential qualified dividend.
- Expected effect: Always output: / 1. Holding-level distribution classification table. / 2. Account-location recommendation table with rationale. / 3. Open-risk checklist for unresolved tax assumptions.
- Example call: `$kanchi-dividend-us-tax-accounting run with US/JP scope and explicit constraints`

## macro-regime-detector
- What it does: Detect structural macro regime transitions (1-2 year horizon) using cross-asset ratio analysis. Analyze RSP/SPY concentration, yield curve, credit conditions, size factor, equity-bond relationship, and sector rotation to identify regime shifts between Concentration, Broadening, Contraction, Inflationary, and Transitional states. Run when user asks about macro regime, market regime change, structural rotation, or long-term market positioning.
- When to use: - User asks about current macro regime or regime transitions / - User wants to understand structural market rotations (concentration vs broadening) / - User asks about long-term positioning based on yield curve, credit, or cross-asset signals / - User references RSP/SPY ratio, IWM/SPY, HYG/LQD, or other cross-asset ratios
- How to use (inputs): - **FMP API Key** (required): Set `FMP_API_KEY` environment variable or pass `--api-key` / - Free tier (250 calls/day) is sufficient (script uses ~10 calls)
- Process summary: 1. Load reference documents for methodology context: / - `references/regime_detection_methodology.md` / - `references/indicator_interpretation_guide.md`
- Expected effect: - `macro_regime_YYYY-MM-DD_HHMMSS.json` Structured data for programmatic use / - `macro_regime_YYYY-MM-DD_HHMMSS.md` Human-readable report with: / 1. Current Regime Assessment / 2. Transition Signal Dashboard
- Example call: `$macro-regime-detector run with US/JP scope and explicit constraints`

## market-breadth-analyzer
- What it does: Quantifies market breadth health using TraderMonty's public CSV data. Generates a 0-100 composite score across 6 components (100 = healthy). No API key required. Use when user asks about market breadth, participation rate, advance-decline health, whether the rally is broad-based, or general market health assessment.
- When to use: **English:** / - User asks "Is the market rally broad-based?" or "How healthy is market breadth?" / - User wants to assess market participation rate / - User asks about advance-decline indicators or breadth thrust
- How to use (inputs): - **Python 3.8+** with `requests` library (for fetching CSV data) / - **Internet access** to reach GitHub Pages URLs / - **No API keys required** - uses freely available public CSV data
- Process summary: Collect inputs -> run framework -> synthesize evidence -> propose actions.
- Expected effect: Actionable output with rankings, key findings, and next-step recommendations.
- Example call: `$market-breadth-analyzer run with US/JP scope and explicit constraints`

## market-environment-analysis
- What it does: Comprehensive market environment analysis and reporting tool. Analyzes global markets including US, European, Asian markets, forex, commodities, and economic indicators. Provides risk-on/risk-off assessment, sector analysis, and technical indicator interpretation. Triggers on keywords like market analysis, market environment, global markets, trading environment, market conditions, investment climate, market sentiment, forex analysis, stock market analysis, ,
- When to use: - When you need a comprehensive overview of global market conditions / - Before making trading or investment decisions / - For daily/weekly market briefings / - When assessing risk-on/risk-off sentiment
- How to use (inputs): - **WebSearch access**: Required for fetching real-time market data / - **No API keys required**: This skill uses web search for data collection / - **Optional**: Economic calendar data for event-driven analysis
- Process summary: Collect inputs -> run framework -> synthesize evidence -> propose actions.
- Expected effect: Actionable output with rankings, key findings, and next-step recommendations.
- Example call: `$market-environment-analysis run with US/JP scope and explicit constraints`

## market-news-analyst
- What it does: This skill should be used when analyzing recent market-moving news events and their impact on equity markets and commodities. Use this skill when the user requests analysis of major financial news from the past 10 days, wants to understand market reactions to monetary policy decisions (FOMC, ECB, BOJ), needs assessment of geopolitical events' impact on commodities, or requires comprehensive review of earnings announcements from mega-cap stocks. The skill automatically collects news using WebSearch/WebFetch tools and produces impact-ranked analysis reports. All analysis thinking and output are conducted in English.
- When to use: Use this skill when: / - User requests analysis of recent major market news (past 10 days) / - User wants to understand market reactions to specific events (FOMC decisions, earnings, geopolitical) / - User needs comprehensive market news summary with impact assessment
- How to use (inputs): - **Tools:** WebSearch and WebFetch tools must be available for news collection / - **API Keys:** None required (uses built-in web search capabilities) / - **Knowledge:** Familiarity with financial markets terminology is helpful but not required
- Process summary: Follow this structured 6-step workflow when analyzing market news: / ### Step 1: News Collection via WebSearch/WebFetch / **Objective:** Gather comprehensive news from the past 10 days covering major market-moving events.
- Expected effect: This skill produces **conversational guidance** during the analysis session. When the full workflow is executed, Claude generates a comprehensive Markdown report (see Step 6 for format) that can be saved to the `reports/` directory upon user request. No files are generated automatically; output is presented in the conversation.
- Example call: `$market-news-analyst run with US/JP scope and explicit constraints`

## market-top-detector
- What it does: Detects market top probability using O'Neil Distribution Days, Minervini Leading Stock Deterioration, and Monty Defensive Sector Rotation. Generates a 0-100 composite score with risk zone classification. Use when user asks about market top risk, distribution days, defensive rotation, leadership breakdown, or whether to reduce equity exposure. Focuses on 2-8 week tactical timing signals for 10-20% corrections.
- When to use: **English:** / - User asks "Is the market topping?" or "Are we near a top?" / - User notices distribution days accumulating / - User observes defensive sectors outperforming growth
- How to use (inputs): **Required:** / - **FMP API Key:** Set `$FMP_API_KEY` environment variable or pass `--api-key`. Free tier sufficient (~33 API calls per execution). / - **WebSearch Access:** Required to collect S&P 500 breadth (50DMA %) and CBOE Put/Call ratio data. / **Optional:**
- Process summary: Collect inputs -> run framework -> synthesize evidence -> propose actions.
- Expected effect: Actionable output with rankings, key findings, and next-step recommendations.
- Example call: `$market-top-detector run with US/JP scope and explicit constraints`

## options-strategy-advisor
- What it does: Options trading strategy analysis and simulation tool. Provides theoretical pricing using Black-Scholes model, Greeks calculation, strategy P/L simulation, and risk management guidance. Use when user requests options strategy analysis, covered calls, protective puts, spreads, iron condors, earnings plays, or options risk management. Includes volatility analysis, position sizing, and earnings-based strategy recommendations. Educational focus with practical trade simulation.
- When to use: Use this skill when: / - User asks about options strategies ("What's a covered call?", "How does an iron condor work?") / - User wants to simulate strategy P/L ("What's my max profit on a bull call spread?") / - User needs Greeks analysis ("What's my delta exposure?")
- How to use (inputs): **Required:** / - Python 3.8+ with `numpy`, `scipy`, `requests` / **Optional:** / - FMP API key (for real-time stock prices and historical volatility)
- Process summary: ### Step 1: Gather Input Data / **Required from User:** / - Ticker symbol
- Expected effect: **Strategy Analysis Report Template:** / ```markdown / # Options Strategy Analysis: [Strategy Name] / **Symbol:** [TICKER]
- Example call: `$options-strategy-advisor run with US/JP scope and explicit constraints`

## pair-trade-screener
- What it does: Statistical arbitrage tool for identifying and analyzing pair trading opportunities. Detects cointegrated stock pairs within sectors, analyzes spread behavior, calculates z-scores, and provides entry/exit recommendations for market-neutral strategies. Use when user requests pair trading opportunities, statistical arbitrage screening, mean-reversion strategies, or market-neutral portfolio construction. Supports correlation analysis, cointegration testing, and spread backtesting.
- When to use: Use this skill when: / - User asks for "pair trading opportunities" / - User wants "market-neutral strategies" / - User requests "statistical arbitrage screening"
- How to use (inputs): Ticker/universe, market scope, time horizon, risk constraints, and optional chart/data inputs.
- Process summary: ### Step 1: Define Pair Universe / **Objective:** Establish the pool of stocks to analyze for pair relationships. / **Option A: Sector-Based Screening (Recommended)**
- Expected effect: Actionable output with rankings, key findings, and next-step recommendations.
- Example call: `$pair-trade-screener run with US/JP scope and explicit constraints`

## pead-screener
- What it does: Screen post-earnings gap-up stocks for PEAD (Post-Earnings Announcement Drift) patterns. Analyzes weekly candle formation to detect red candle pullbacks and breakout signals. Supports two input modes - FMP earnings calendar (Mode A) or earnings-trade-analyzer JSON output (Mode B). Use when user asks about PEAD screening, post-earnings drift, earnings gap follow-through, red candle breakout patterns, or weekly earnings momentum setups.
- When to use: - User asks for PEAD screening or post-earnings drift analysis / - User wants to find earnings gap-up stocks with follow-through potential / - User requests red candle breakout patterns after earnings / - User asks for weekly earnings momentum setups
- How to use (inputs): - FMP API key (set `FMP_API_KEY` environment variable or pass `--api-key`) / ```bash / export FMP_API_KEY=your_api_key_here / ```
- Process summary: ### Step 1: Prepare and Execute Screening / Run the PEAD screener script in one of two modes: / **Mode A (FMP earnings calendar):**
- Expected effect: - `pead_screener_YYYY-MM-DD_HHMMSS.json` - Structured results with stage classification / - `pead_screener_YYYY-MM-DD_HHMMSS.md` - Human-readable report grouped by stage
- Example call: `$pead-screener run with US/JP scope and explicit constraints`

## portfolio-manager
- What it does: Comprehensive portfolio analysis using Alpaca MCP Server integration to fetch holdings and positions, then analyze asset allocation, risk metrics, individual stock positions, diversification, and generate rebalancing recommendations. Use when user requests portfolio review, position analysis, risk assessment, performance evaluation, or rebalancing suggestions for their brokerage account.
- When to use: Invoke this skill when the user requests: / - "Analyze my portfolio" / - "Review my current positions" / - "What's my asset allocation?"
- How to use (inputs): ### Alpaca MCP Server Setup / This skill requires Alpaca MCP Server to be configured and connected. The MCP server provides access to: / - Current portfolio positions / - Account equity and buying power
- Process summary: ### Step 1: Fetch Portfolio Data via Alpaca MCP / Use Alpaca MCP Server tools to gather current portfolio information: / **1.1 Get Account Information:**
- Expected effect: Actionable output with rankings, key findings, and next-step recommendations.
- Example call: `$portfolio-manager run with US/JP scope and explicit constraints`

## position-sizer
- What it does: Calculate risk-based position sizes for long stock trades. Use when user asks about position sizing, how many shares to buy, risk per trade, Kelly criterion, ATR-based sizing, or portfolio risk allocation. Supports stop-loss distance calculation, volatility scaling, and sector concentration checks.
- When to use: - User asks "how many shares should I buy?" / - User wants to calculate position size for a specific trade setup / - User mentions risk per trade, stop-loss sizing, or portfolio allocation / - User asks about Kelly Criterion or ATR-based position sizing
- How to use (inputs): - No API keys required / - Python 3.9+ with standard library only
- Process summary: ### Step 1: Gather Trade Parameters / Collect from the user: / - **Required**: Account size (total equity)
- Expected effect: ### JSON Report / ```json / { / "schema_version": "1.0",
- Example call: `$position-sizer run with US/JP scope and explicit constraints`

## scenario-analyzer
- What it does: |
- When to use: - / - 18 / - /2 /3 / -
- How to use (inputs): - **API Keys**: ebSearch/WebFetch / - **MCP Servers**: / - **Dependencies**: scenario-analyst strategy-reviewer Task tool
- Process summary: ### Phase 1: / #### Step 1.1: / 1. ** *
- Expected effect: | | | | / |---------|------|------| / | `reports/scenario_analysis_<topic>_YYYYMMDD.md` | Markdown | | / ** :**
- Example call: `$scenario-analyzer run with US/JP scope and explicit constraints`

## sector-analyst
- What it does: This skill should be used when analyzing sector rotation patterns and market cycle positioning. It fetches sector uptrend data from CSV (no API key required) and optionally accepts chart images for supplementary analysis. Use this skill when the user requests sector rotation analysis, cyclical vs defensive assessment, overbought/oversold identification, or market cycle phase estimation. All analysis and output are conducted in English.
- When to use: Use this skill when: / - User requests sector rotation analysis (no chart images required) / - User asks about cyclical vs defensive positioning / - User wants to know which sectors are overbought or oversold
- How to use (inputs): - **Python 3.8+** with `requests` library (for CSV fetching) / - **No API keys required** data is fetched from a public GitHub repository / - **Optional**: Sector performance chart images for supplementary analysis
- Process summary: Follow this structured workflow: / ### Step 1: CSV Data Collection / 1. Run the analysis script: `python3 scripts/analyze_sector_rotation.py`
- Expected effect: Save analysis results as a Markdown file with naming convention: `sector_analysis_YYYY-MM-DD.md` / Use this structure: / ```markdown / # Sector Performance Analysis - [Date]
- Example call: `$sector-analyst run with US/JP scope and explicit constraints`

## signal-postmortem
- What it does: Record and analyze post-trade outcomes for signals generated by edge pipeline and other skills. Track false positives, missed opportunities, and regime mismatches. Feed results back to edge-signal-aggregator weights and skill improvement backlog.
- When to use: - After a trade has been closed and you want to record the outcome / - When reviewing a batch of signals that have reached their holding period (5 or 20 days) / - To identify systematic false positive patterns from specific skills / - To generate feedback for edge-signal-aggregator weight calibration
- How to use (inputs): - Python 3.9+ / - FMP API key (optional, for fetching realized returns if not provided manually) / - Standard library + `requests` for API calls / - Input: signal records in JSON format (from edge-signal-aggregator or screener outputs)
- Process summary: ### Step 1: Prepare Signal Records / Gather closed or matured signal records. Each record should include: / - `signal_id`: Unique identifier
- Expected effect: ### Postmortem Record (JSON) / ```json / { / "schema_version": "1.0",
- Example call: `$signal-postmortem run with US/JP scope and explicit constraints`

## skill-designer
- What it does: Design new Claude skills from structured idea specifications. Use when the skill auto-generation pipeline needs to produce a Claude CLI prompt that creates a complete skill directory (SKILL.md, references, scripts, tests) following repository conventions.
- When to use: - The skill auto-generation pipeline selects an idea from the backlog and needs / a design prompt for `claude -p` / - A developer wants to bootstrap a new skill from a JSON idea specification / - Quality review of generated skills requires awareness of the scoring rubric
- How to use (inputs): - Python 3.9+ / - No external API keys required / - Reference files must exist under `references/`
- Process summary: ### Step 1: Prepare Idea Specification / Accept a JSON file (`--idea-json`) containing: / - `title`: Human-readable idea name
- Expected effect: The script outputs a plain-text prompt to stdout. Exit code 0 on success, / 1 if required reference files are missing.
- Example call: `$skill-designer run with US/JP scope and explicit constraints`

## skill-idea-miner
- What it does: Mine Claude Code session logs for skill idea candidates. Use when running the weekly skill generation pipeline to extract, score, and backlog new skill ideas from recent coding sessions.
- When to use: - Weekly automated pipeline run (Saturday 06:00 via launchd) / - Manual backlog refresh: `python3 scripts/run_skill_generation_pipeline.py --mode weekly` / - Dry-run to preview candidates without LLM scoring
- How to use (inputs): - **Python 3.10+** with `pyyaml` package / - **Claude CLI** installed and authenticated (`claude --version` to verify) / - **Session logs** in `~/.claude/projects/<project>/` (created automatically by Claude Code) / - No API keys required (uses Claude CLI for LLM calls)
- Process summary: ### Quick Start / ```bash / # Dry-run: preview mined candidates without LLM scoring
- Expected effect: ### raw_candidates.yaml / ```yaml / generated_at_utc: "2026-03-08T06:00:00Z" / period: {from: "2026-03-01", to: "2026-03-07"}
- Example call: `$skill-idea-miner run with US/JP scope and explicit constraints`

## skill-integration-tester
- What it does: Validate multi-skill workflows defined in CLAUDE.md by checking skill existence, inter-skill data contracts (JSON schema compatibility), file naming conventions, and handoff integrity. Use when adding new workflows, modifying skill outputs, or verifying pipeline health before release.
- When to use: - After adding or modifying a multi-skill workflow in CLAUDE.md / - After changing a skill's output format (JSON schema, file naming) / - Before releasing new skills to verify pipeline compatibility / - When debugging broken handoffs between consecutive workflow steps
- How to use (inputs): - Python 3.9+ / - No API keys required / - No third-party Python packages required (uses only standard library)
- Process summary: ### Step 1: Run Integration Validation / Execute the validation script against the project's CLAUDE.md: / ```bash
- Expected effect: ### JSON Report / ```json / { / "schema_version": "1.0",
- Example call: `$skill-integration-tester run with US/JP scope and explicit constraints`

## stanley-druckenmiller-investment
- What it does: Druckenmiller Strategy Synthesizer - Integrates 8 upstream skill outputs (Market Breadth, Uptrend Analysis, Market Top, Macro Regime, FTD Detector, VCP Screener, Theme Detector, CANSLIM Screener) into a unified conviction score (0-100), pattern classification, and allocation recommendation. Use when user asks about overall market conviction, portfolio positioning, asset allocation, strategy synthesis, or Druckenmiller-style analysis. Triggers on queries like "What is my conviction level?", "How should I position?", "Run the strategy synthesizer", "Druckenmiller analysis", " ", " ", " ", " ".
- When to use: **English:** / - User asks "What's my overall conviction?" or "How should I be positioned?" / - User wants a unified view synthesizing breadth, uptrend, top risk, macro, and FTD signals / - User asks about Druckenmiller-style portfolio positioning
- How to use (inputs): Ticker/universe, market scope, time horizon, risk constraints, and optional chart/data inputs.
- Process summary: Collect inputs -> run framework -> synthesize evidence -> propose actions.
- Expected effect: Actionable output with rankings, key findings, and next-step recommendations.
- Example call: `$stanley-druckenmiller-investment run with US/JP scope and explicit constraints`

## strategy-pivot-designer
- What it does: Detect backtest iteration stagnation and generate structurally different strategy pivot proposals when parameter tuning reaches a local optimum.
- When to use: - Backtest scores have plateaued despite multiple refinement iterations. / - A strategy shows signs of overfitting (high in-sample, low robustness). / - Transaction costs defeat the strategy's thin edge. / - Tail risk or drawdown exceeds acceptable thresholds.
- How to use (inputs): - Python 3.9+ / - `PyYAML` / - Iteration history JSON (accumulated backtest-expert evaluations) / - Source strategy draft YAML (from edge-strategy-designer)
- Process summary: 1. Accumulate backtest evaluation results into an iteration history file using `--append-eval`. / 2. Run stagnation detection on the history to identify triggers (plateau, overfitting, cost defeat, tail risk). / 3. If stagnation detected, generate pivot proposals using three techniques: assumption inversion, archetype switch, objective reframe.
- Expected effect: - `pivot_drafts/research_only/*.yaml` strategy_draft compatible YAML proposals / - `pivot_drafts/exportable/*.yaml` export-ready drafts + ticket YAML for candidate-agent / - `pivot_report_*.md` human-readable pivot analysis / - `pivot_manifest_*.json` metadata for all generated files
- Example call: `$strategy-pivot-designer run with US/JP scope and explicit constraints`

## technical-analyst
- What it does: This skill should be used when analyzing weekly price charts for stocks, stock indices, cryptocurrencies, or forex pairs. Use this skill when the user provides chart images and requests technical analysis, trend identification, support/resistance levels, scenario planning, or probability assessments based purely on chart data without consideration of news or fundamental factors.
- When to use: - User provides weekly chart images (stocks, indices, crypto, forex) and requests technical analysis / - Need to identify trend direction, strength, and potential reversal points / - Looking for support/resistance levels and key price zones / - Want probabilistic scenario planning with specific price targets
- How to use (inputs): - **Chart Images**: User must provide weekly timeframe chart images for analysis / - **No API Keys Required**: This skill analyzes user-provided images; no external data fetches
- Process summary: ### Step 1: Receive Chart Images / When the user provides one or more weekly chart images for analysis: / 1. Confirm receipt of all chart images
- Expected effect: This skill generates markdown analysis reports saved to the `reports/` directory: / - **File format**: `[SYMBOL]_technical_analysis_[YYYY-MM-DD].md` / - **Content**: Comprehensive analysis including trend, S/R levels, MA analysis, volume, patterns, and 2-4 probabilistic scenarios with targets and invalidation levels
- Example call: `$technical-analyst run with US/JP scope and explicit constraints`

## tenbagger-screener
- What it does: Find potential multibagger stocks using a structured scoring model across growth runway, reinvestment quality, financial durability, valuation setup, and catalyst timing.
- When to use: Use when the user asks for: / - tenbagger candidates / - multibagger screens / - high-upside growth stocks with quality filters
- How to use (inputs): - market (`US`, `JP`, `CN`, or mixed) / - style preference (`quality growth`, `deep value turnaround`, `balanced`) / - holding horizon (`3y`, `5y`, `10y`) / - risk tolerance (`low`, `medium`, `high`)
- Process summary: 1. Build candidate universe from watchlist or broad screen. / 2. Apply hard exclusion rules first. / 3. Score each remaining name using the Tenbagger Score model.
- Expected effect: ### Screen Summary / - universe size / - excluded count and reasons / - final ranked candidates
- Example call: `$tenbagger-screener run with US/JP scope and explicit constraints`

## theme-detector
- What it does: Detect and analyze trending market themes across sectors. Use when user asks about current market themes, trending sectors, sector rotation, thematic investing, what themes are hot or cold, or wants to identify bullish and bearish market narratives with lifecycle analysis.
- When to use: **Explicit Triggers:** / - "What market themes are trending right now?" / - "Which sectors are hot/cold?" / - "Detect current market themes"
- How to use (inputs): **Required:** / - Python 3.7+ with core dependencies: / ```bash / pip install requests beautifulsoup4 lxml pandas numpy yfinance
- Process summary: ### Step 1: Verify Environment / Check that API keys are configured (see Prerequisites): / ```bash
- Expected effect: The skill generates two output files in the `reports/` directory: / **JSON Output** (`theme_detector_YYYY-MM-DD_HHMMSS.json`): / ```json / {
- Example call: `$theme-detector run with US/JP scope and explicit constraints`

## trade-hypothesis-ideator
- What it does: >
- When to use: Use when you need structured analysis, ranking, or decision support for this domain.
- How to use (inputs): Ticker/universe, market scope, time horizon, risk constraints, and optional chart/data inputs.
- Process summary: 1. Receive input JSON bundle. / 2. Run pass 1 normalization + evidence extraction. / 3. Generate hypotheses with prompts:
- Expected effect: Actionable output with rankings, key findings, and next-step recommendations.
- Example call: `$trade-hypothesis-ideator run with US/JP scope and explicit constraints`

## trader-memory-core
- What it does: Track investment theses across their lifecycle from screening idea to closed position with postmortem. Register theses from screener outputs, manage state transitions, attach position sizing, review due dates, and generate postmortem reports with P&L and MAE/MFE analysis. Trigger when user says "register thesis", "track this idea", "thesis status", "review due", "close position", "postmortem", or "trading journal".
- When to use: - After a screener (kanchi, earnings-trade-analyzer, vcp, pead, canslim, edge-candidate-agent) produces candidates / - When transitioning a thesis from IDEA ENTRY_READY ACTIVE CLOSED / - When attaching position-sizer output to a thesis / - When checking which theses are due for review
- How to use (inputs): - Python 3.10+ / - `pyyaml` (already in project dependencies) / - FMP API key (optional, only for MAE/MFE calculation in postmortem)
- Process summary: ### 1. Register Ingest screener output as thesis / Read the screener's JSON output and convert to thesis using the appropriate adapter. / ```bash
- Expected effect: ### Thesis YAML (state/theses/) / Each thesis is a YAML file with: / - Identity: thesis_id, ticker, created_at / - Classification: thesis_type, setup_type, catalyst
- Example call: `$trader-memory-core run with US/JP scope and explicit constraints`

## uptrend-analyzer
- What it does: Analyzes market breadth using Monty's Uptrend Ratio Dashboard data to diagnose the current market environment. Generates a 0-100 composite score from 5 components (breadth, sector participation, rotation, momentum, historical context). Use when asking about market breadth, uptrend ratios, or whether the market environment supports equity exposure. No API key required.
- When to use: **English:** / - User asks "Is the market breadth healthy?" or "How broad is the rally?" / - User wants to assess uptrend ratios across sectors / - User asks about market participation or breadth conditions
- How to use (inputs): Ticker/universe, market scope, time horizon, risk constraints, and optional chart/data inputs.
- Process summary: Collect inputs -> run framework -> synthesize evidence -> propose actions.
- Expected effect: Actionable output with rankings, key findings, and next-step recommendations.
- Example call: `$uptrend-analyzer run with US/JP scope and explicit constraints`

## us-market-bubble-detector
- What it does: Evaluates market bubble risk through quantitative data-driven analysis using the revised Minsky/Kindleberger framework v2.1. Prioritizes objective metrics (Put/Call, VIX, margin debt, breadth, IPO data) over subjective impressions. Features strict qualitative adjustment criteria with confirmation bias prevention. Supports practical investment decisions with mandatory data collection and mechanical scoring. Use when user asks about bubble risk, valuation concerns, or profit-taking timing.
- When to use: Use this skill when: / **English:** / - User asks "Is the market in a bubble?" or "Are we in a bubble?" / - User seeks advice on profit-taking, new entry timing, or short-selling decisions
- How to use (inputs): Ticker/universe, market scope, time horizon, risk constraints, and optional chart/data inputs.
- Process summary: Collect inputs -> run framework -> synthesize evidence -> propose actions.
- Expected effect: ### Evaluation Report Structure (v2.1) / ```markdown / # [Market Name] Bubble Evaluation Report (Revised v2.1)
- Example call: `$us-market-bubble-detector run with US/JP scope and explicit constraints`

## us-stock-analysis
- What it does: Comprehensive US stock analysis including fundamental analysis (financial metrics, business quality, valuation), technical analysis (indicators, chart patterns, support/resistance), stock comparisons, and investment report generation. Use when user requests analysis of US stock tickers (e.g., "analyze AAPL", "compare TSLA vs NVDA", "give me a report on Microsoft"), evaluation of financial metrics, technical chart analysis, or investment recommendations for American stocks.
- When to use: Use when you need structured analysis, ranking, or decision support for this domain.
- How to use (inputs): Ticker/universe, market scope, time horizon, risk constraints, and optional chart/data inputs.
- Process summary: Collect inputs -> run framework -> synthesize evidence -> propose actions.
- Expected effect: Actionable output with rankings, key findings, and next-step recommendations.
- Example call: `$us-stock-analysis run with US/JP scope and explicit constraints`

## value-dividend-screener
- What it does: Screen US stocks for high-quality dividend opportunities combining value characteristics (P/E ratio under 20, P/B ratio under 2), attractive yields (3% or higher), and consistent growth (dividend/revenue/EPS trending up over 3 years). Supports two-stage screening using FINVIZ Elite API for efficient pre-filtering followed by FMP API for detailed analysis. Use when user requests dividend stock screening, income portfolio ideas, or quality value stocks with strong fundamentals.
- When to use: Invoke this skill when the user requests: / - "Find high-quality dividend stocks" / - "Screen for value dividend opportunities" / - "Show me stocks with strong dividend growth"
- How to use (inputs): Ticker/universe, market scope, time horizon, risk constraints, and optional chart/data inputs.
- Process summary: ### Step 1: Verify API Key Availability / **For Two-Stage Screening (Recommended):** / Check if both API keys are available:
- Expected effect: Actionable output with rankings, key findings, and next-step recommendations.
- Example call: `$value-dividend-screener run with US/JP scope and explicit constraints`

## vcp-screener
- What it does: Screen S&P 500 stocks for Mark Minervini's Volatility Contraction Pattern (VCP). Identifies Stage 2 uptrend stocks forming tight bases with contracting volatility near breakout pivot points. Use when user requests VCP screening, Minervini-style setups, tight base patterns, volatility contraction breakout candidates, or Stage 2 momentum stock scanning.
- When to use: - User asks for VCP screening or Minervini-style setups / - User wants to find tight base / volatility contraction patterns / - User requests Stage 2 momentum stock scanning / - User asks for breakout candidates with defined risk
- How to use (inputs): - FMP API key (set `FMP_API_KEY` environment variable or pass `--api-key`) / - Free tier (250 calls/day) is sufficient for default screening (top 100 candidates) / - Paid tier recommended for full S&P 500 screening (`--full-sp500`)
- Process summary: ### Step 1: Prepare and Execute Screening / Run the VCP screener script: / ```bash
- Expected effect: - `vcp_screener_YYYY-MM-DD_HHMMSS.json` - Structured results / - `vcp_screener_YYYY-MM-DD_HHMMSS.md` - Human-readable report
- Example call: `$vcp-screener run with US/JP scope and explicit constraints`

