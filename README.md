# Meta Metrics + Machine Learning Experiment

This repo documents an experiment I ran to predict downstream ecommerce outcomes from Meta (Facebook/Instagram) ads performance data.

**What this is:** predictive modeling + a real postmortem.
**What this isn’t:** “AI that prints money.”

## Goal
Predict a single target outcome (ex: Purchases or Revenue) from weekly ad set performance metrics to support forecasting and decision-making.

## Data
This repo uses **synthetic / sanitized data only** (no client exports).

## Status
- v1: baseline regression + failure analysis (documented)
- v2: roadmap for a better model (planned)

## How to run (local)

1) Install dependencies
```bash

pip install -r requirements.txt

python notebooks/01_baseline_linear_regression.py
