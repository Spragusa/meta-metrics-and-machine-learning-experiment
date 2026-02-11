# v2 Roadmap – Model Redesign Plan

The original version (v1) used linear regression with both raw and derived metrics.
It exposed issues around leakage, multicollinearity, and non-linearity.

This document outlines how the model would be redesigned.

---

## 1. Narrow the Objective

Select a single dependent variable:

- revenue
OR
- purchases

Avoid predicting multiple targets simultaneously.

---

## 2. Use Raw Drivers Only

Inputs should include:

- spend
- impressions
- reach
- clicks
- landing_page_views
- add_to_cart
- initiate_checkout
- frequency

Exclude derived metrics such as ROAS, CPC, CTR, CVR, AOV, and RPV.

---

## 3. Introduce Lag Features

Ad systems are not instant-response systems.

Add:
- spend_t-1
- spend_t-3
- clicks_t-1
- purchases_t-1

This better reflects delayed conversion behavior.

---

## 4. Model Comparison

Instead of relying on linear regression alone:

Compare:
- Linear Regression (baseline)
- Random Forest
- Gradient Boosting (XGBoost / LightGBM)

Evaluate using:
- MAE (Mean Absolute Error)
- MAPE (Mean Absolute Percentage Error)

Use time-based splits instead of random splits.

---

## 5. Expected Outcome

The goal is not perfect prediction.

The goal is:
- Reduced leakage
- Improved generalization
- Clear feature importance
- More stable performance across time

---

This redesign shifts the experiment from a simple regression attempt
to a more disciplined modeling workflow aligned with real-world ML practices.
