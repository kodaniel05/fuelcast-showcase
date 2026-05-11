# Engineering Decisions

## Batch Workflow Over Live Polling

FuelCast uses a daily batch workflow because the underlying data sources update daily or weekly. This reduces unnecessary API calls, improves reproducibility, and makes demo behavior predictable.

## Refresh Guard

A once-per-day refresh guard prevents accidental repeated live API usage. The dashboard explicitly shows whether the current snapshot came from live APIs or cached outputs.

## Separate Raw And Processed Data

Raw normalized observations are preserved before transformation. Processed datasets are built separately for modeling and dashboard consumption, which keeps the pipeline auditable.

## Horizon-Specific Models

The project trains separate models for 1-week, 2-week, and 4-week forecasts because relationships between current signals and future prices change by horizon.

## Time-Series-Safe Evaluation

Model evaluation uses chronological splits rather than shuffled data. This avoids leaking future information into training and keeps the forecast metrics more realistic.

## Baseline Comparison

The system tracks a naive baseline so model performance can be judged against a simple alternative instead of being interpreted in isolation.

## AI With Fallback

AI-generated explanations are useful for readability, but they should not be a single point of failure. FuelCast includes a deterministic fallback summary path.

## Static Dashboard Artifacts

The dashboard reads generated JSON artifacts. This choice simplifies deployment, makes demos stable, and keeps the frontend decoupled from private pipeline internals.

## Public Showcase Boundary

This showcase repository documents the system without exposing source code, schema details, API integration logic, raw data, or reusable proprietary implementation.
