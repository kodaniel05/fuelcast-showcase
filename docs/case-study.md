# FuelCast Case Study

## Background

FuelCast is a private full-stack data product that creates a daily energy intelligence snapshot for U.S. gasoline prices. It combines public fuel-price data, crude oil context, market signals, forecasting models, operational metadata, and a frontend analytics dashboard.

The project was built to demonstrate how a production-style analytics workflow can move beyond a notebook into a repeatable, inspectable system.

## Motivation

Gas prices are an accessible but non-trivial forecasting domain. They are affected by seasonality, crude prices, regional differences, market expectations, and data-source cadence. That made the project a useful way to practice real-world tradeoffs: data quality, source reliability, forecast uncertainty, API limits, and user-facing communication.

## Problem

Fuel-price information is public, but it is not always easy to use. A user typically has to gather data from separate sources, clean it, align daily and weekly series, decide which indicators are relevant, evaluate forecast quality, and communicate uncertainty responsibly.

FuelCast addresses that fragmentation by turning the workflow into a daily pipeline and dashboard.

## Solution

FuelCast ingests public energy and market data, validates the observations, stores raw and processed outputs, builds weekly modeling features, trains separate models for multiple forecast horizons, generates an explanation, and exports dashboard-ready JSON artifacts.

The frontend presents the output as a polished analytics command center: national KPIs, state-level map views, forecast cards, rankings, top movers, market signals, model metrics, and pipeline health.

## Main Features

- National gasoline and crude-price overview
- 1-week, 2-week, and 4-week gasoline price forecasts
- U.S. state choropleth map for price and change views
- Searchable state rankings and state-specific forecast estimates
- Top daily, weekly, and monthly movers
- Model accuracy metrics by horizon
- AI-assisted analyst summary with fallback explanation mode
- Refresh status that distinguishes live updates from cached daily snapshots
- Validation status and source health metadata

## Design Decisions

The dashboard is designed for scanning. Forecasts, state comparisons, and pipeline status are visible without requiring users to inspect logs or raw files. The product language avoids overstating precision: market signals are framed as context, and forecast views are labeled as model estimates.

State-level views are included because national averages hide regional variation. The map gives a fast geographic read, while rankings support comparison and search.

The AI explanation is positioned as an analyst takeaway, not as a source of truth. It summarizes generated metrics and signals rather than inventing external causes.

## Technical Decisions

FuelCast uses a batch pipeline because source data changes daily or weekly and does not require constant polling. A daily refresh guard protects API limits and keeps repeated demos reproducible.

Raw observations are preserved before transformation so validation and modeling decisions remain auditable. Processed artifacts are generated separately for the dashboard, keeping the frontend simple and deployable.

Forecasting is split by horizon. A 1-week forecast and a 4-week forecast have different uncertainty profiles, so separate models and metrics make the product more honest and easier to evaluate.

The system supports graceful degradation. If PostgreSQL is unavailable, local artifacts can still support the pipeline. If AI services are unavailable, the product can generate a deterministic rule-based explanation.

## Challenges

The hardest part was not just building a model; it was making the system operationally trustworthy. API cadence, free-tier limits, inconsistent data availability, and stale refreshes all had to be represented clearly.

Another challenge was aligning daily market data with weekly fuel-price series without introducing time leakage. The project uses time-aware feature construction and evaluation to keep the modeling story defensible.

Finally, the dashboard had to balance density and clarity. It needed enough information to feel like a real analytics tool while still being understandable in a short recruiter or interview walkthrough.

## Lessons Learned

- Forecast products need careful communication around uncertainty.
- A simple refresh-status panel can dramatically improve trust in an automated dashboard.
- Baselines are essential; model metrics are less meaningful without a simple comparison.
- AI summaries are most useful when grounded in structured outputs and paired with fallback behavior.
- Public portfolio projects can be impressive without exposing private implementation details.

## Impact

FuelCast demonstrates an end-to-end data product: ingestion, validation, storage, feature engineering, modeling, explainability, orchestration, testing, CI, and frontend presentation. It gives interviewers a concrete system to discuss while preserving the private project’s implementation and intellectual property.

## Future Roadmap

- Rolling-window backtesting and model drift monitoring
- Model registry or version-comparison workflow
- Scenario forecasts for crude-price shocks
- Broader EIA coverage and richer regional analysis
- Authenticated API layer for production dashboard reads
- Managed deployment, observability, and alerting
