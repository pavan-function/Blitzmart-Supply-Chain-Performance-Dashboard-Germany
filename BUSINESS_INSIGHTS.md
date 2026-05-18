# BlitzMart Analytics: Business Insights

End-to-end analysis of a fictional German e-commerce retailer. Modeled after Zalando, Otto, and Amazon DE.

**6.6M rows analyzed across 8 relational tables.** Stack: SQL (DuckDB) + Python (pandas).

---

## Executive Summary

BlitzMart processed **€2.16 billion in revenue across 1.39M delivered orders** from roughly 200K active customers between 2022 and 2024, at an average order value of **€1,548**. The analysis points at three things worth acting on: a **31.7-point carrier performance gap**, a **Leipzig warehouse that's clearly underperforming**, and a **Fashion returns problem** that's pulling refund costs higher than they need to be.

---

## Top 8 Findings

### 1. €2.16B revenue, heavily concentrated in November and December

Across the full 3-year period, revenue hit €2.16B on 1.39M orders. The peak months (Nov-Dec) deliver around €126.6M each, versus €42.3M in normal months. That's roughly a 3× holiday surge.

Q4 is when the year is won or lost. Inventory planning, hiring, and logistics capacity all need to scale 3× for those two months, otherwise operational weaknesses compound right when volume is highest.

---

### 2. 36% of SKUs drive 80% of revenue (classic ABC distribution)

1,805 out of 5,000 products sit in the A-class and generate 80% of revenue. The remaining 64% of catalog SKUs share just 20%.

This is the textbook Pareto pattern, and it has direct inventory implications. A-class products need tight stock control, premium carrier service, and zero stockout tolerance. C-class can run on lean inventory with fewer review cycles. Treating all SKUs the same way wastes working capital.

---

### 3. Top 20% of customers generate 38% of revenue

39,959 customers (the top 20%) drive 37.9% of total revenue. The "Champions" RFM segment is the densest concentration of value.

Retention spend should be heavily skewed toward this group. Holding onto these customers is worth far more than acquiring an equivalent number of average ones.

---

### 4. 31.7 point OTIF gap between best and worst carrier

DHL delivers 76.5% of shipments on-time. GLS delivers only 44.8%. That's a 31.7 point gap across 1.4M total shipments. UPS sits at 70%, DPD at 67%, Hermes at 54%.

Every GLS shipment is basically a coin flip. Moving that volume to DHL would lift customer experience without changing prices. Estimated impact: around 10,000 fewer late deliveries per year (about 30,000 across the full analysis period).

---

### 5. Leipzig Distribution is the operational outlier

Leipzig Hub runs at 45.4% OTIF with 3.64 day average delivery. Berlin Hub by comparison is at 72.8% OTIF, 3.2 days. The other four warehouses cluster within 2 points of Berlin.

So Leipzig isn't just slightly worse, it's an isolated problem. Either invest in its capacity (staffing, layout, automation) or reroute East German orders through Berlin Hub. A single hub means a single owner can fix it.

---

### 6. Fashion returns 2.3× more than Books, and sizing is the cause

Fashion return rate is 15.6% (highest). Books at 6.7% (lowest). Across all categories, "Wrong size" alone accounts for 23% of every return.

A virtual try-on tool or better size charts would attack the biggest cost lever directly. Even a 20% reduction in size-driven returns would save roughly 12,700 Fashion returns per year.

---

### 7. Demand forecasting is healthy at 91-94% accuracy

Forecast accuracy by category ranges from 91.4% (Home & Kitchen) to 94.1% (Toys). No category falls below 90%.

The takeaway here is what *not* to do. Don't waste resources improving demand forecasts when fulfilment is the actual bottleneck. The supply side (carriers, Leipzig) is where the leverage is.

---

### 8. Berlin + Hamburg + München = 47% of revenue

Berlin alone drives 22% of revenue. The top 3 cities concentrate nearly half of all sales. The bottom 6 cities combined contribute under 20%.

Marketing budget, regional pricing, warehouse capacity, and premium delivery options (same-day) all should reflect this skew. The economics for same-day delivery only really work in the top 3 cities.

---

## Recommended Actions

| # | Action | Driver | Expected Impact |
|---|---|---|---|
| 1 | Consolidate GLS volume into DHL | OTIF gap | ~10K fewer late deliveries per year |
| 2 | Audit Leipzig Hub OR reroute East orders | Warehouse outlier | +20pp OTIF in East region |
| 3 | Launch sizing guide / virtual try-on for Fashion | "Wrong size" 23% | Save ~12K Fashion returns per year |
| 4 | Build VIP retention program for top 20% customers | Customer concentration | Protect 38% of revenue |
| 5 | Pre-stock A-class SKUs by Oct 15 every year | Nov/Dec 3× spike | Reduce peak-season stockouts |

---

## Methodology

- **Data scale.** 6.6M records across 8 relational tables (customers, orders, order_items, products, suppliers, warehouses, shipments, returns)
- **ETL pipeline.** Built in Python with pandas. Generated data, injected ~29K realistic data quality issues, then cleaned via imputation, deduplication, outlier capping, and referential repair
- **SQL analysis.** 15 queries in DuckDB. Window functions (LAG, NTILE, ROW_NUMBER), CTEs, RFM segmentation, cohort retention
- **Python analysis.** ABC analysis for products and customers, OTIF carrier scorecard, demand seasonality, forecast accuracy, return root cause, geographic concentration
- **Tools.** Python, pandas, NumPy, DuckDB, matplotlib, seaborn, Tableau Public

---

*Analysis by Pavan Raj Kotagiri. Benchmarks drawn from publicly known German e-commerce and logistics operations (Zalando, Otto, DHL).*
