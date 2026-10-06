# Insights and Recommendations

Data: 24 Sep 2020 – 28 Feb 2021 · 884,302 cleaned events · 490,398 sessions · 407,229 users · 53,452 products
Conventions: sessions are distinct `user_session` values · rates are percentages · money is in the dataset's own currency units (the source does not state a currency) · hours are UTC · every figure below was checked against the QA page.

## Executive summary

Shoppers are lost before they ever reach the cart. Only 8.45% of viewing sessions add an item to the cart (a 91.55% drop-off). Once a cart exists, 58.99% of those sessions go on to purchase. Overall conversion is 4.98%, producing 5,125,114 in revenue.

The largest opportunities are:
- View → cart conversion: each +1 percentage point is worth about 606,000.
- Checkout for carts with products above 200: these complete about 7 points less often than mid-priced carts.
- The appliances category: it converts at half the site rate on more than 25,000 view sessions.

Top recommendation: test product-page and discovery improvements first, and track View → Cart rate weekly.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Headline KPIs

| KPI | Value |
|---|---|
| View / cart / purchase sessions | 488,360 / 41,270 / 24,344 |
| View → cart rate (drop-off) | 8.45% (91.55%) |
| Cart → purchase rate (cart abandonment) | 58.99% (41.01%) |
| Overall conversion (view → purchase) | 4.98% |
| Revenue | 5,125,113.92 |
| Purchase count (items, price > 0) | 37,343 |
| AOV (revenue per purchased item) | 137.24 |
| Revenue per purchasing session | 210.53 (1.53 items per purchasing session) |
| Revenue per view session | 10.49 |

AOV in this project divides revenue by purchased items, as defined in the KPI dictionary. Revenue per purchasing session is reported separately and always labelled as such.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Insight 1: The biggest leak is view → cart

- FACT: View → cart drop-off is 91.55%. Cart → purchase drop-off is 41.01%. 447,090 view sessions end without any cart activity.
- INFERENCE: Purchase intent is low at the browsing stage. Once intent forms, most shoppers complete the purchase.
- HYPOTHESIS: Product pages or search results do not persuade enough (price visibility, imagery, reviews, relevance). Not provable from this data; investigate.
- IMPACT: +1 pp on view → cart ≈ 4,884 more cart sessions → ≈ 2,881 more purchasing sessions at the current 58.99% → ≈ 606,000 extra revenue. This is a modelled estimate that    assumes new carts convert like existing ones.
- RECOMMENDATION: Prioritise product-page and discovery experiments over checkout changes.

## Insight 2: Appliances attracts traffic but converts at half the site rate

- FACT: Appliances converts at 2.44% on 25,303 view sessions, against a site rate of 4.98%. It earns 105,300 from 617 purchasing sessions, which is 170.66 revenue per purchasing session.
  - Lower rates exist only at much smaller volume: country_yard 0.98% (1,831) and accessories 2.91% (1,308).
  - Electronics, the next big category, converts at 4.53% on 103,281 sessions, close to average.
- INFERENCE: Appliances is the clearest "popular but leaking" category. Electronics carries four times the traffic but needs far less improvement.
- HYPOTHESIS: Long consideration cycles, comparison shopping, or delivery and installation concerns. Investigate.
- IMPACT: Raising appliances to the site rate ≈ 644 more purchasing sessions ≈ 110,000 revenue.
- RECOMMENDATION: Audit appliances product pages and the category landing page (specifications, delivery and installation information, comparison tools).

## Insight 3: Cart completion falls as price rises, then levels off above 200

| Price band (product average price) | Cart sessions | Cart → purchase |
|---|---|---|
| a < 50 | 16,611 | 64.69% |
| b 50–199 | 13,147 | 58.01% |
| c 200–499 | 11,148 | 50.73% |
| d 500+ | 2,108 | 51.47% |

- FACT: The rate drops about 6–7 points per band up to 200, then stays flat (c and d are within 1 point).
  - Band cart sessions add up to 43,014, more than the 41,270 unique cart sessions, because one session can cart products in several bands. The bands overlap and should not be added together.
- INFERENCE: Price is linked to abandonment up to about 200. Above that, the level stays lower but does not keep falling.
- HYPOTHESIS: Shipping costs, payment limits or financing needs become decisive for higher-value baskets. Investigate.
- IMPACT: Lifting bands c and d to band b's 58.01% ≈ 949 more purchasing sessions ≈ 489,000 revenue, valued at each band's revenue per purchasing session. This is a rough estimate because the bands overlap.
- RECOMMENDATION: Test checkout support for carts above 200: visible delivery cost, instalment or financing options, and reassurance on returns.

## Insight 4: Conversion follows the time of day; the day of the week barely matters

- FACT (hours in UTC): Conversion peaks at 10:00 (5.48%, 32,659 view sessions) and is lowest at 00:00 (3.67%, 6,484 view sessions).
  - The hours 00:00–04:59 carry only 8.1% of hourly view sessions; 07:00–18:59 carry 68.8%.
  - By weekday, conversion ranges only from 4.76% (Sunday) to 5.01% (Tuesday and Wednesday).
- INFERENCE: The best-converting hours are also the busiest, so the time-of-day effect matters in practice. The weak night hours have little traffic, so improving them adds little. Day of week is not a useful lever.
- HYPOTHESIS: Daytime visitors arrive with clearer purchase intent. The store's local time zone is not documented; if it is UTC+3, the peak is around 13:00 local time.
- RECOMMENDATION: Schedule campaigns and promotions for roughly 06:00–12:00 UTC, and don't segment by weekday.

## Insight 5: A few well-known brands convert poorly, but the money at stake is modest

- FACT: Among brands with at least 4,000 view sessions, the lowest converters are:
  - philips 1.35% (4,076 sessions)
  - sony 1.80% (4,995)
  - lg 1.98% (4,797)
  - bbk 2.24% (4,992)

  The site rate is 4.98%. The dashboard's brand table keeps brands with more than 1,000 view sessions (92 of 1,000 brands), including the `unknown` brand bucket (137,188 view sessions). Its lower session total compared with the category table comes from removing smaller brands, not from unbranded activity. hammer (1,689 view sessions) has no purchases at all, which the table shows as blank.
- INFERENCE: These brands underperform by roughly 3 points each, but none has enough traffic to rival the category-level opportunities.
- HYPOTHESIS: Customers compare prices for well-known brands with other retailers. Investigate.
- IMPACT: Bringing all four to the site rate ≈ 590 more purchasing sessions ≈ 150,000 revenue.
- RECOMMENDATION: Use brand as a diagnostic view (price-competitiveness check for these four), not a primary lever.

## Insight 6: Engagement depth is the strongest predictor of purchase

| Events in session | Sessions | Share of sessions | Conversion |
|---|---|---|---|
| 1–2 | 418,324 | 85.3% | 0.61% |
| 3–9 | 65,403 | 13.3% | 28.56% |
| 10+ | 6,671 | 1.4% | 46.90% |

- FACT: 85% of sessions end after one or two events and almost never convert. Sessions with three or more events convert 47–77 times more often.
- INFERENCE: Most losses are single-page visits. Moving a visitor to a second or third interaction is the key step.
- HYPOTHESIS: Weak related-product suggestions or landing-page mismatch. Depth is also partly a result of intent, so this is correlation, not proven cause.
- RECOMMENDATION: Test "similar items" and "frequently bought together" modules on product pages. Track the share of sessions with 3+ events.

## Insight 7: Conversion improved steadily across the period

| Month | View sessions | Conversion |
|---|---|---|
| Sep 2020 (from 24 Sep) | 16,935 | 3.94% |
| Oct 2020 | 95,394 | 4.34% |
| Nov 2020 | 108,202 | 4.53% |
| Dec 2020 | 85,295 | 5.09% |
| Jan 2021 | 97,857 | 5.57% |
| Feb 2021 | 88,572 | 5.58% |

- FACT: Conversion rose from 3.94% to 5.58% while traffic peaked in November.
- INFERENCE: Overall figures mix a weaker autumn with a stronger winter. Compare segments within the same months before drawing conclusions.
- HYPOTHESIS: Holiday-season intent, changes in the traffic mix, or site changes. It is not possible to tell these apart with only five months of data.
- RECOMMENDATION: Track conversion monthly and set targets against the latest months, not the full-period average.

## Insight 8: About 1 in 7 purchases skips the cart step

- FACT: The reached-stage funnel is 488,360 → 41,270 → 24,344. The strict time-ordered funnel (view, then cart, then purchase in that order) is 488,360 → 41,214 → 20,506. 3,582 purchasing sessions (14.7%) record no cart event at all.
- INFERENCE: Part of the purchase flow goes around the cart, for example a "buy now" path, or cart events are not always logged.
- RECOMMENDATION: Confirm with the tracking team whether a direct-purchase path exists. Report both funnels until cart tracking is confirmed complete.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Data-quality notes

- Missing category: `unknown` covers 149,524 view sessions (30.6%) and 493,897 revenue (9.6%), converting at 3.53%. Category conclusions describe the labelled 69% only.
- Revenue concentration: computers generate 3,728,836 (72.8% of revenue) from 30.4% of view sessions and convert at 7.38%, the best of any category. Small changes in computers outweigh large changes elsewhere.
- Cleaning: 885,129 raw rows → 884,302 clean rows. 827 rows were removed (0.09%): 165 had no session and 662 were duplicate events. No purchase has a price of zero or less.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


## Recommendations (ranked by impact × feasibility)

| # | Finding | Impact | Recommendation | Priority | Expected outcome | KPI to monitor |
|---|---|---|---|---|---|---|
| 1 | View → cart drop-off 91.55% (Insight 1) | ≈ 606,000 per +1 pp | A/B-test product-page content and search/discovery relevance | High | Higher add-to-cart rate | View → Cart Rate |
| 2 | Carts above 200 complete about 7 pts less (Insight 3) | ≈ 489,000 if bands c–d match band b | Show delivery cost early; offer instalments and returns reassurance | High | Fewer abandoned high-value carts | Cart → Purchase Rate, bands c–d |
| 3 | 85% of sessions end after 1–2 events (Insight 6) | Largest pool of lost visitors | Add related-product and bundle modules | Medium | More multi-step sessions | Share of sessions with 3+ events |
| 4 | Appliances converts at 2.44% vs 4.98% (Insight 2) | ≈ 110,000 | Audit appliances pages: specifications, delivery, installation info | Medium | Category conversion toward site average | Appliances Overall Conversion |
| 5 | 30.6% of view sessions lack a category (data notes) | Hides category-level leaks | Fix product tagging at source | Medium | Fuller category analysis | % view sessions with `unknown` category |
| 6 | Conversion peaks 06:00–12:00 UTC (Insight 4) | Better campaign timing | Schedule promotions in peak-converting hours | Low | Higher campaign conversion | Conversion by hour |

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


## Limitations

- One store, five months: a single electronics retailer, 24 Sep 2020 – 28 Feb 2021. The window includes the holiday season, so seasonal effects are present but cannot be separated from the trend (no second year to compare).
- Sparse cart data: cart events are few compared with views, so cart-stage rates for small segments are directional.
- No context columns: there is no device, marketing channel or geography data, so drop-off cannot be attributed to those factors.
- Sessions approximate visits: 14.7% of purchasing sessions have no cart event, so two funnel versions are reported.
- Missing labels: 30.6% of view sessions have no category and 28.1% have no brand (`unknown`). Category and brand totals are understated.
- Price bands are directional: they use each product's average price across all its events, not the price paid.
- Hours are UTC: the store's local time zone is not documented.
- Internal validation only: checks were made inside Power BI (profiling and invariant checks) and independently recomputed from the raw CSV, but not against a production source system.
