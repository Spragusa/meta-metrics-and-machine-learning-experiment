# Lessons Learned – v1 Predictive Modeling Attempt

This document outlines what worked, what failed, and what I would redesign.

## Original Objective

Build a multi-variable regression model to predict downstream ecommerce outcomes 
(purchases or revenue) from Meta ads performance data at the weekly ad set level.

The idea was to use a large number of performance metrics to reduce bias and improve prediction accuracy.

---

## What Worked

- Structured multi-account data into a consistent weekly format.
- Cleaned exported Meta data into numeric-only datasets.
- Built a repeatable modeling pipeline (data → model → evaluate → deploy conceptually).
- Identified key modeling assumptions.

---

## What Failed (Technically)

### 1. Data Leakage

Several independent variables were mathematically derived from the dependent variable.

Examples:
- ROAS = Revenue / Spend
- CVR = Purchases / Clicks
- RPV = Revenue / Clicks

Using these as inputs to predict revenue or purchases created circular logic.

The model was indirectly “seeing” the answer.

---

### 2. Multicollinearity

Metrics like CTR, CPC, CVR, AOV, and ROAS are highly entangled.

This caused unstable regression coefficients and poor generalization.

Linear regression assumes independent predictors — this dataset violated that assumption.

---

### 3. Non-Linearity of Ad Auctions

Meta ad performance is influenced by:
- Auction dynamics
- Creative fatigue
- Budget scaling thresholds
- Seasonality

Linear regression assumes proportional change.
Ad systems behave in nonlinear ways.

---

### 4. Aggregation Smoothing

Weekly aggregation may have reduced variance and masked short-term performance shifts.

A time-based modeling approach with lag features would likely perform better.

---

## Key Takeaways

- Use raw drivers (spend, impressions, clicks, funnel events) instead of derived ratios.
- Separate training and evaluation by time (avoid leakage across weeks).
- Tree-based models (Random Forest / Gradient Boosting) are better suited than simple linear regression.
- Failure analysis is as valuable as model accuracy.

---

## What I Would Build Now (v2 Direction)

- Target one dependent variable (Revenue OR Purchases).
- Use only raw independent inputs.
- Add lag features (t-1, t-3) to reflect delayed conversions.
- Compare baseline linear regression to a tree-based model.
- Evaluate using MAE / MAPE on time-based splits.

---

This project was an early applied ML experiment using real-world marketing data.  
The primary value was not model accuracy, but understanding system design flaws and improving modeling discipline.
