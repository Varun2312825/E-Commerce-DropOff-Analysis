DATA SOURCE

| Item | Detail |
|---|---|
| Dataset | eCommerce events history in electronics store (Kaggle, `mkechinov`) |
| URL | https://www.kaggle.com/datasets/mkechinov/ecommerce-events-history-in-electronics-store |
| File used | `events.csv` (renamed from the downloaded file; ~106 MB uncompressed) |
| Downloaded | 15 September 2026 |
| Raw rows | 885,129 (884,302 after cleaning) |
| Period | 24 Sep 2020 – 28 Feb 2021 (timestamps in UTC) |
| Grain | One row = one event (view, cart or purchase) |

Why this dataset: it records every step of the shopping journey (view → cart → purchase), with session IDs, readable categories and brands, and item prices. That is everything a drop-off analysis needs, in a file small enough to import whole into Power BI.

What it cannot answer: device, marketing channel, geography and individual checkout steps. None of these are recorded.

Scope note: a single online store. The catalogue is mostly computers and electronics, plus smaller categories (appliances, auto, construction, stationery and others). Currency is not stated in the source.

Tooling: cleaned and modelled entirely in Power BI (Power Query + DAX). No external database.

`events.csv` is not committed to the repository: at ~106 MB it exceeds GitHub's 100 MB file limit. Download it from the URL above and place it in this folder as `events.csv`.
