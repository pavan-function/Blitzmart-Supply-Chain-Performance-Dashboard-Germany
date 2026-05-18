# BlitzMart Analytics: German E-Commerce Supply Chain

End-to-end analytics project on a fictional German e-commerce retailer. The data is synthetic but the patterns are modeled after companies like Zalando, Otto, and Amazon DE.

**6.6M rows, 8 tables, built with SQL, Python and Tableau.**

[![Tableau](https://img.shields.io/badge/Tableau-Live_Dashboard-E97627?logo=tableau&logoColor=white)](https://public.tableau.com/app/profile/pavan.raj.kotagiri)
[![Python](https://img.shields.io/badge/Python-pandas_·_numpy-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![SQL](https://img.shields.io/badge/SQL-DuckDB-FFF000?logo=duckdb&logoColor=black)](https://duckdb.org/)

---

## Live Interactive Dashboards

| Dashboard | What's in it | Link |
|---|---|---|
| Sales & Customer Performance | Revenue, AOV, category mix, geography | [Open](https://public.tableau.com/app/profile/pavan.raj.kotagiri/viz/BlitzMartAnalytics-GermanE-CommerceSupplyChain/SalesCustomerPerformance) |
| Supply Chain Operations | Carrier OTIF, warehouse performance, returns | [Open](https://public.tableau.com/app/profile/pavan.raj.kotagiri/viz/BlitzMartAnalytics-GermanE-CommerceSupplyChain/SupplyChainOperation) |

![Sales Dashboard](Images/dashboard_sales.png)
![Supply Chain Dashboard](Images/dashboard_supplychain.png)

---

## Project Overview

BlitzMart is a made-up German online retailer. I took raw transactional data through a full analytics pipeline: data generation, cleaning, SQL analysis, Python analysis, then two Tableau dashboards with business recommendations on top.

The dataset spans 2022 to 2024. About 1.5M orders generated (1.39M delivered), roughly 200K customers, 5,000 products across 8 categories, 6 warehouses, 5 shipping carriers, and customers spread across 15 German cities.

---

## Key Findings

| # | Finding | What to do about it |
|---|---|---|
| 1 | €2.16B revenue, AOV €1,548. Nov/Dec runs 3× higher than off-season months | Q4 is the make or break quarter. Plan capacity for 3× scale |
| 2 | 36% of products drive 80% of revenue (classic ABC pattern) | Tight stock control on the A-class SKUs, lean inventory on the rest |
| 3 | Top 20% of customers generate 38% of revenue | Retention budget should skew heavily to this group |
| 4 | DHL hits 76.5% on-time, GLS only 44.8%. A 31.7 point gap | Shifting GLS volume to DHL avoids around 10,000 late deliveries per year |
| 5 | Leipzig warehouse runs at 45.4% OTIF. Other 5 hubs cluster around 72% | Either invest in Leipzig or reroute East orders through Berlin |
| 6 | Fashion returns at 15.6% vs Books at 6.7%. "Wrong size" is 23% of all returns | Size guide or virtual try-on tackles the biggest cost driver |
| 7 | Forecast accuracy sits at 91-94% across all categories | Forecasting isn't the problem. Fix fulfilment instead |
| 8 | Berlin, Hamburg, München together = 47% of revenue | Concentrate marketing and warehouse capacity accordingly |

Full breakdown: [BUSINESS_INSIGHTS.md](BUSINESS_INSIGHTS.md)

---

## Tech Stack

| Layer | Tools |
|---|---|
| Data generation, cleaning | Python, pandas, NumPy, Faker |
| SQL analysis | DuckDB (PostgreSQL compatible) |
| Python analysis | pandas, matplotlib, seaborn |
| Dashboards | Tableau Public |
| Environment | Google Colab |

---

## Repository Structure

```
blitzmart-analytics/
├── README.md
├── BUSINESS_INSIGHTS.md
├── notebooks/
│   ├── BlitzMart_01_DataGeneration.ipynb
│   ├── BlitzMart_02_SQL_Analysis.ipynb
│   └── BlitzMart_03_Python_Analysis.ipynb
├── sql/
│   └── analysis_queries.sql
├── images/
│   ├── dashboard_sales.png
│   └── dashboard_supplychain.png
└── data/
    └── README.md
```

---

## Methodology

### 1. Data Generation
6.6M rows across 8 relational tables. The data isn't purely random. I baked in patterns based on real German market data:
- Customers distributed by real population shares (Destatis 2024)
- Carrier performance profiles modeled on actual German parcel market (DHL premium, GLS budget)
- Category-specific return rates (Fashion high because of sizing, Books low)
- Seasonal demand with a 3× Nov/Dec spike

### 2. ETL & Cleaning
Built a pipeline that detected and fixed around 29,000 data quality issues:
- Missing values handled by median imputation
- Duplicate orders deduplicated (kept first occurrence)
- Invalid quantities and zero prices removed
- Impossible delivery dates (delivery before ship) removed
- Outlier refunds capped using IQR
- Orphan supplier references repaired with an Unknown placeholder

Every fix is logged in an audit CSV.

### 3. SQL Analysis (15 queries)
CTEs, window functions (LAG, NTILE, ROW_NUMBER, RANK), RFM customer segmentation, and monthly cohort retention. All running on DuckDB against the cleaned CSVs.

### 4. Python Analysis (12 techniques)
ABC analysis for products and customers, OTIF carrier scorecard, demand seasonality, forecast accuracy, return root cause, geographic concentration.

### 5. Tableau Dashboards
Two dashboards. One for commercial stakeholders (revenue, AOV, categories, geography), one for operations (OTIF, warehouses, returns).

---

## Sample Insights

**Carrier performance gap.** DHL at 76.5% on-time, GLS at 44.8%. That's a 31.7 point gap across 1.4M shipments. GLS sits well below the 70% benchmark most retailers use.

**Leipzig warehouse outlier.** Five warehouses cluster around 71-73% OTIF. Leipzig is alone at 45.4%, dragging down the entire East region.

**Fashion returns.** 15.6% return rate vs 6.7% for Books. "Wrong size" alone accounts for 23% of every return. Clear, actionable case for sizing tools.

---

## Author

**Pavan Raj Kotagiri**
Data Analyst | Business Analyst | Supply Chain Analytics

- [Tableau Public](https://public.tableau.com/app/profile/pavan.raj.kotagiri)
- [LinkedIn](https://www.linkedin.com/in/pavanrajkotagiri/)

---

## Notes

Raw CSV files aren't committed (about 250 MB total, hits GitHub's limits). The data generation notebook rebuilds the full dataset from scratch in around 5 minutes. Schema details: [data/README.md](Data/README.md).

This is a portfolio project on synthetic data. BlitzMart is fictional. The business patterns are benchmarked against publicly known German e-commerce and logistics operations.
