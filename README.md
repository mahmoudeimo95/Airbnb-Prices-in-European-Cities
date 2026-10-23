# Airbnb Prices in European Cities

End-to-end data analytics project: raw Airbnb listing data → cleaned and modeled data layers (bronze / silver / gold) → interactive dashboard.

Built as part of the **AI & Data Science** program at **Instant Academy**.

## Overview

The dataset covers **51,707 Airbnb listings** across **10 European cities** (Amsterdam, Athens, Barcelona, Berlin, Budapest, Lisbon, London, Paris, Rome, Vienna), split by weekday and weekend prices. The goal is to understand what drives Airbnb prices in Europe.

## Key Findings

- Average price is about **€130 per night** (price outliers excluded).
- **Amsterdam** is the most expensive city (~€270/night) and **Athens** the cheapest (~€70/night).
- Weekend prices are slightly higher in most cities.
- **Size drives price more than location**: a 4-bedroom listing averages ~€252/night vs ~€115 for 1 bedroom, while distance to the city center has a weak effect.
- The attractions index (0.43), guest capacity (0.29) and bedrooms (0.26) have the strongest correlation with price.
- Superhosts are not more expensive (~€120 vs ~€134), so their advantage is satisfaction rather than price.

## Pipeline Architecture

| Layer | Output | What happens |
|-------|--------|--------------|
| **Bronze** | `bronze_listings.csv` | All 20 raw CSVs combined, with city and day type taken from the file names. Nothing is altered. |
| **Silver** | `silver_listings.csv` | Cleaned and standardized columns, data types fixed, country added, and derived fields created: price per night, price per person, price per bedroom, studio flag, price outlier flag, price / distance / satisfaction bands. |
| **Gold** | 14 files | Star schema (`fact_listings`, `dim_city`, `dim_room_type`, `dim_day_type`) plus pre-aggregated tables for the dashboard. |

**Data quality:** no null values and no duplicates in the raw data, so no imputation was required. The only nulls in silver are `price_per_bedroom_night` for studios (0 bedrooms), which is intentional. 826 listings are flagged as price outliers and excluded from averages.

## Dashboard

Three pages: **Market Overview**, **City Deep Dive** and **Price Drivers**, with slicers for city, room type and day type. Built in Power BI using the gold layer.

Design: coral `#FF5A5F` and teal `#00A699` on a light grey background. The Power BI theme is in `dashboard/airbnb_theme.json`, and an interactive web preview is in `dashboard/airbnb_dashboard.html`.

## Repository Structure

```
├── data/                    # raw CSV files
├── notebooks/
│   └── Airbnb_Full_Pipeline.ipynb
├── bronze/
├── silver/
├── gold/
├── dashboard/
│   ├── airbnb_theme.json
│   └── airbnb_dashboard.html
└── README.md
```

## How to Run

1. Clone the repository and place the raw CSV files in `data/`.
2. Install dependencies: `pip install pandas numpy matplotlib seaborn`
3. Run `notebooks/Airbnb_Full_Pipeline.ipynb` top to bottom. It generates the `bronze/`, `silver/` and `gold/` folders.
4. In Power BI Desktop, load the gold tables, import `dashboard/airbnb_theme.json`, and build the report.

## Tools

Python (Pandas, NumPy, Matplotlib, Seaborn) · Power BI · Chart.js

## Author

**Mahmoud**: Data Analyst
GitHub: [mahmoudeimo95](https://github.com/mahmoudeimo95)
