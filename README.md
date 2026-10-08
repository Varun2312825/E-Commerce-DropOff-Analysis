# E-COMMERCE DROP-OFF ANALYSIS — POWER BI

Problem(Hypothetical): An online electronics retailer's revenue was not keeping pace with its traffic, and nobody knew where shoppers were abandoning the journey.

Objective: Find the biggest leak in the view → cart → purchase funnel, identify the catalogue segments losing the most value, and recommend measurable fixes.

Dataset: [eCommerce events history in electronics store](https://www.kaggle.com/datasets/mkechinov/ecommerce-events-history-in-electronics-store) (Kaggle). 885,129 events, 24 Sep 2020 – 28 Feb 2021, with session IDs, products, categories, brands and prices.

Tools: Power BI Desktop only: Power Query (M) for cleaning and shaping, DAX for all analysis. No external database.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


## Key findings

| # | Finding |
|---|---|
| 1 | **The biggest leak is view → cart:** 91.55% of viewing sessions never add to cart. Once a cart exists, 58.99% purchase. |
| 2 | **Each +1 pp on view → cart ≈ 606,000 revenue** at current cart conversion and basket value. |
| 3 | **Cart completion falls with price** from 64.7% (< 50) to about 51% above 200, then levels off. |
| 4 | **Appliances converts at 2.44%** against a 4.98% site rate on 25,303 view sessions. |
| 5 | **85% of sessions end after 1–2 events** and convert at 0.61%. Sessions with 10+ events convert at 46.9%. |
| 6 | **Conversion rose from 3.94% to 5.58%** between September and February. It peaks around 10:00 UTC, and the weekday barely matters. |

## Top recommendations

| Recommendation | KPI to monitor |
|---|---|
| A/B-test product-page content and search relevance | View → Cart Rate |
| Show delivery cost early and offer instalments for carts above 200 | Cart → Purchase Rate (bands c–d) |
| Add related-product modules to deepen sessions | Share of sessions with 3+ events |

Full analysis: [insights and recommendations](documentation/insights_and_recommendations.md).

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Method

Business requirements → data profiling → Power Query cleaning (staged raw → clean) → star schema → DAX measures and funnel logic → dashboard → internal validation → recommendations.

Data model: star schema: fact `events_clean`, plus dimensions `dim_product` and `Dim_Date` (both many-to-one, single direction). Two calculated tables support a strict time-ordered funnel and session-depth segmentation.

[Data model](documentation/data_model.png)

Cleaning: 885,129 → 884,302 rows: 165 session-less rows and 662 duplicate events removed, blank category and brand kept as `unknown`, taxonomy split into three levels.

Validation: Eight invariant checks on a hidden QA page, including funnel monotonicity, depth bands summing to total sessions, product-dimension completeness and revenue integrity. All figures were also recomputed independently from the raw CSV.

## Dashboard

| Page | Answers |
|---|---|
| Overview | Headline KPIs, funnel, daily conversion |
| Funnel | Where shoppers drop off; reached vs strict ordered funnel |
| Segments | Conversion by session depth and price band |
| Product | Categories and brands with traffic but weak conversion (drill-through to detail) |
| Time | Hour × weekday heatmap, daily trend, what-if revenue scenario |

[Overview](screenshots/01_overview.png)
[Funnel](screenshots/02_funnel.png)
[Segments](screenshots/03_segments.png)
[Product](screenshots/04_product.png)
[Time](screenshots/05_time.png)

## Repository

```
data/            source notes (CSV not committed: download from Kaggle)
documentation/   requirements, data and KPI dictionaries, cleaning log, validation, insights
powerbi/         Power BI report (.pbix) and project files (.pbip)
screenshots/     dashboard pages
```

## Limitations 

The data covers one store over five months: seasonality can't be separated from trend. There is no device, channel or geography data. 30.6% of view sessions lack a category. Hours are in UTC. Validation is internal to this project.


