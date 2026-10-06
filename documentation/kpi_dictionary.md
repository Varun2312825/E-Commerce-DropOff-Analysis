# KPI DICTIONARY

Grain matters: event measures count rows, session measures count distinct `user_session`. Names below match the measures in the Power BI model.

## Volume

| Measure | Definition | Grain | Value |
|---|---|---|---|
| Total Events | Count of rows | Event | 884,302 |
| Unique Users | Distinct `user_id` | User | 407,229 |
| Unique sessions | Distinct `user_session` | Session | 490,398 |
| Unique Products | Distinct `product_id` in the fact | Product | 53,452 |

## Funnel

| Measure | Definition | Value |
|---|---|---|
| View Sessions | Sessions with ≥ 1 `view` | 488,360 |
| Cart Sessions | Sessions with ≥ 1 `cart` | 41,270 |
| Purchase Sessions | Sessions with ≥ 1 `purchase` | 24,344 |
| View to Cart Rate | Cart Sessions ÷ View Sessions | 8.45% |
| Cart to Purchase Rate | Purchase Sessions ÷ Cart Sessions | 58.99% |
| Overall Conversion | Purchase Sessions ÷ View Sessions | 4.98% |
| Cart Abandonment Rate | 1 − Cart to Purchase Rate | 41.01% |
| Dropoff View to Cart / … rate | View − Cart Sessions / 1 − View to Cart Rate | 447,090 / 91.55% |
| Dropoff Cart to Purchase / … rate | Cart − Purchase Sessions / 1 − Cart to Purchase Rate | 16,926 / 41.01% |
| Ordered Viewed / Carted / Bought | Sessions whose first view, cart, purchase happen in that time order | 488,360 / 41,214 / 20,506 |

## Revenue

| Measure | Definition | Value |
|---|---|---|
| Revenue | Sum of `price` where `event_type = purchase` and `price > 0` | 5,125,113.92 |
| Purchase Count | Purchase rows with `price > 0` (items) | 37,343 |
| AOV | Revenue ÷ Purchase Count (per item, not per order) | 137.24 |
| Revenue per Session | Revenue ÷ View Sessions | 10.49 |

## Segments and scenario

| Measure | Definition |
|---|---|
| total depth Sessions | Rows in `Session Stats` (sessions per depth band) |
| Depth Conversion rate | Average of the 0/1 `Converted` flag in `Session Stats` |
| Uplift % Value | Selected uplift (default 5%) |
| Projected Extra Purchases | Cart Sessions × Cart to Purchase Rate × Uplift % |
| Projected Extra Revenue | Projected Extra Purchases × AOV (hypothetical) |

Rules: every rate is a measure, never a calculated column, so it re-evaluates under any filter. Every division uses `DIVIDE` to guard against divide-by-zero. Revenue and AOV always apply the `price > 0` rule.
