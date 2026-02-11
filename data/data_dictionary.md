# Data Dictionary

This dataset mirrors a weekly ad set level export from Meta Ads Manager.
All data in this repo is synthetic/sanitized.

---

## Raw Performance Drivers (Recommended Inputs for v2)

| Variable | Description | Type |
|----------|-------------|------|
| spend | Ad spend for the week | numeric |
| impressions | Total ad impressions | numeric |
| reach | Unique users reached | numeric |
| clicks | Link clicks | numeric |
| landing_page_views | Users who landed on site | numeric |
| add_to_cart | Add-to-cart events | numeric |
| initiate_checkout | Checkout started events | numeric |
| purchases | Completed purchases | numeric |
| revenue | Purchase conversion value | numeric |
| frequency | Impressions / Reach | numeric |

---

## Derived Metrics (Used in v1 – Not Recommended as Inputs)

| Variable | Formula | Issue |
|----------|---------|-------|
| cpm | spend / (impressions / 1000) | derived from spend + impressions |
| cpc | spend / clicks | derived from spend + clicks |
| ctr | clicks / impressions | ratio of two predictors |
| cvr | purchases / clicks | contains dependent signal |
| aov | revenue / purchases | contains dependent signal |
| roas | revenue / spend | directly contains dependent signal |
| rpv | revenue / clicks | contains dependent signal |

These derived metrics introduced leakage and multicollinearity when used as independent variables.

---

## Target Variable (Model Prediction Target)

One of the following should be selected:

- purchases
OR
- revenue

Not both simultaneously.
