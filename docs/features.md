# Features

## Daily Intelligence Snapshot

FuelCast creates a daily snapshot of U.S. gasoline-price trends, forecasts, market context, model quality, and pipeline health.

## Multi-Horizon Forecasting

The system produces separate forecasts for:

- Next week
- Two weeks ahead
- Four weeks ahead

Each horizon has its own evaluation metrics so users can see how uncertainty changes over time.

## State-Level Analytics

The dashboard includes a U.S. map, state rankings, selected-state detail, and top-mover views. This makes regional differences visible without requiring users to inspect raw data.

## Market And Energy Signals

FuelCast incorporates crude-oil and market-context signals to support interpretation. These are presented as context, not causal proof.

## AI Analyst Takeaway

The explanation layer summarizes the forecast using generated FuelCast outputs. When AI services are unavailable, a rule-based explanation keeps the dashboard complete.

## Pipeline Health

The dashboard surfaces refresh state, source status, validation status, row counts, and last-run metadata so users can judge whether the current snapshot is fresh and reliable.

## Graceful Degradation

The private system is designed to keep useful outputs available when optional services are unavailable, including database and AI service fallbacks.
