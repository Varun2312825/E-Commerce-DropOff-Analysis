DATA DICTIONARY

## Grain

One row in `events_clean` = one event: a single user action (view, cart or purchase) on one product, at one timestamp, within one session.

| Count this | DAX | Gives |
|---|---|---|
| Rows | `COUNTROWS(events_clean)` | Events |
| Distinct `user_session` | `DISTINCTCOUNT(events_clean[user_session])` | Sessions |
| Distinct `user_id` | `DISTINCTCOUNT(events_clean[user_id])` | Users |

A session contains several `purchase` rows: one order with several items. That is why purchase events (37,343) exceed purchasing sessions (24,344).

## Source columns (`events.csv` → `events_clean`)

| Column | Power BI type | Description | Blanks |
|---|---|---|---|
| `event_time` | Date/Time | When the event happened (UTC). The raw text ends in `" UTC"`, which is stripped in Power Query. | None |
| `event_type` | Text | `view`, `cart` or `purchase` (trimmed, lowercase) | None; exactly 3 values |
| `product_id` | Whole number | Product identifier | None |
| `category_id` | Whole number | Numeric category identifier | None |
| `category_code` | Text | Dotted taxonomy, e.g. `computers.components.cpu` | 26.7% blank → `unknown` |
| `brand` | Text | Brand name (lowercase) | 24.0% blank → `unknown` |
| `price` | Decimal number | Item price in source currency units | None; range 0.22 – 64,771.06; no purchase priced ≤ 0 |
| `user_id` | Whole number | Persistent user identifier | None |
| `user_session` | Text | Session identifier | 165 raw rows blank → removed |

## Derived columns

| Table | Column | Built in | Definition |
|---|---|---|---|
| `events_clean` | `cat_11`, `cat_12`, `cat_13` | Power Query | Category levels 1–3, split from `category_code` on `.` |
| `events_clean` | `event_date` | DAX | Date part of `event_time`; key to `Dim_Date` |
| `events_clean` | `Hour` | DAX | `HOUR(event_time)`, 0–23, UTC |
| `dim_product` | `avg_price` | Power Query | Average `price` of the product across all its events |
| `dim_product` | `Price Band` | DAX | `a <50`, `b 50-199`, `c 200-499`, `d 500+` (from `avg_price`) |

 The level columns are named `cat_11/12/13` in the model, where the digits stand for "level 1/2/3".

## Model tables

| Table | Type | One row per | Purpose |
|---|---|---|---|
| `events_raw` | Power Query staging (not loaded) | Raw CSV row | Untouched source |
| `events_clean` | Fact (Power Query) | Event | All measures |
| `dim_product` | Dimension (Power Query, grouped from `events_clean`) | Product | Category, brand, average price, price band |
| `Dim_Date` | Dimension (DAX `CALENDAR`, marked as date table) | Date | Daily trend, weekday (sorted by `WeekdayNo`) |
| `Session Funnel` | Calculated table | Session | First view, cart and purchase time for the strict ordered funnel |
| `Session Stats` | Calculated table | Session | Event count, converted flag (0/1), depth band |
| `Uplift %` | What-if parameter | Value 0–20% | Revenue scenario |

Relationships: `events_clean[product_id]` → `dim_product[product_id]` and `events_clean[event_date]` → `Dim_Date[Date]`. Both are many-to-one with single-direction filtering. `Session Funnel` and `Session Stats` are standalone, so they don't respond to slicers.
