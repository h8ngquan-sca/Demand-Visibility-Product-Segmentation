# Demand Visibility & Product Segmentation

![Python|78](https://img.shields.io/badge/Python-blue) ![pandas](https://img.shields.io/badge/pandas-green) ![seaborn](https://img.shields.io/badge/seaborn-orange) ![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

> Transforming a 1M+ record manufacturing dataset into an actionable ABC-XYZ inventory segmentation framework — identifying the 4 highest-risk SKUs driving critical supply chain vulnerability.

---

## Business Context

A global manufacturing company operating 4 central warehouses and 2,160+ SKUs lacked a systematic framework to differentiate inventory management across its product portfolio. This resulted in a "one-size-fits-all" policy applied to products with vastly different demand volumes and volatility profiles, exposing the business to severe stockouts, hidden holding costs, and inefficient capital allocation.

The absence of demand visibility meant that critical high-revenue SKUs received the same planning attention as nearly inactive long-tail items — a fundamental misalignment between operational effort and business impact.

---

## Approach

1. **Data Cleaning** — Processed over 1 million records, resolved negative demand anomalies (accounting-format return orders), handled 11,239 missing date values (1.07%), and addressed data truncation issues at period boundaries to establish a reliable analytical baseline.
2. **Exploratory Data Analysis (EDA)** — Designed 5 core visualizations to uncover network-wide demand visibility: monthly demand trends (2011–2017), warehouse concentration analysis, Pareto category breakdown, demand distribution & outlier detection, and top/bottom product identification.
3. **ABC Analysis (Volume Segmentation)** — Segmented 2,160 SKUs based on cumulative demand contribution, identifying the "vital few" (Group A) versus the "trivial many" (Group C) to guide resource prioritization and service level targets.
4. **XYZ Analysis & Policy Matrix (Volatility Segmentation)** — Classified products by demand predictability using Coefficient of Variation (CV), then cross-referenced with ABC classes to produce a 9-cell matrix of differentiated inventory and forecasting policies — the core actionable deliverable of this project.

---

## Key Findings

- **Network Vulnerability:** Demand is heavily concentrated at Whse_J, which single-handedly processes **65.5% of total network volume (3.34B units)**. Any operational disruption at this facility would immediately impact the majority of supply chain output.
    
- **Hyper-Pareto Category:** Category_019 dominates the portfolio, driving **82.7% of total unit demand (4.2B out of 5.1B units)** — far exceeding the standard 80/20 Pareto rule and creating extreme single-category supply risk.
    
- **Extreme SKU Imbalance (ABC):** A mere **3.9% of SKUs (84 products, Group A)** generate **~79.8% of total demand**, while **86.8% of SKUs (Group C)** contribute only **~5% of volume** — confirming a severe "long tail" problem.
    
- **High Demand Volatility (XYZ):** **34.4% of SKUs (742 items)** fall into Group Z, characterized by highly erratic, unpredictable demand patterns that traditional statistical forecasting cannot reliably capture.
    
- **The "Danger Zone" — AZ Products:** Cross-classification identified **4 critical AZ SKUs** — products combining high revenue impact (Group A) with extreme demand unpredictability (Group Z). These 4 items represent the absolute highest risk of stockouts and working capital loss in the entire portfolio.
    

---
## ABC-XYZ Policy Matrix

|Class|SKU Count|Inventory Policy|Forecasting Method|Priority|
|---|---|---|---|---|
|**AZ**|4|High safety stock, strict manual oversight|Qualitative consensus / Scenario planning|🔴 1 — Critical|
|**AX**|57|High service level (98%+), lean safety stock|Moving Average / Simple ETS|🟠 2 — High|
|**AY**|23|High service level (98%+), seasonal buffer|Prophet / Seasonal ETS|🟠 3 — High|
|**BX**|85|Standard service level (95%), automated reorder|Moving Average / Simple ETS|🟡 4 — Medium|
|**BY**|90|Standard service level (95%), seasonal buffer|Prophet / Seasonal ETS (Automated)|🟡 5 — Medium|
|**BZ**|27|High buffer or transition to MTO|Exception-based / Qualitative inputs|🟡 6 — Medium|
|**CX**|129|Cost-driven, fully automated Reorder Point|Naive forecast / Simple Moving Average|🟢 7 — Low|
|**CY**|1,034|Minimal stock, candidate for SKU rationalization|Basic seasonal baseline (Zero-touch)|🟢 8 — Low|
|**CZ**|711|Strict Make-to-Order (MTO) or phase-out|No mathematical forecasting (Reactive)|🟢 9 — Low|

---
## Strategic Recommendations

**1. Immediately isolate and protect AZ & Group A items.** The 4 AZ products and 84 Group A SKUs represent the core revenue engine. Assign dedicated planners, implement manual oversight protocols, and maintain elevated safety stock buffers to fiercely protect service levels for this segment.

**2. Rationalize the "Long Tail" (CZ & CY items).** Stop applying standard stocking rules to the bottom 86.8% of the portfolio. Transition CZ items (711 SKUs) to a strict Make-to-Order model and initiate an SKU rationalization review to eliminate dead stock, free up warehouse racking space, and recover trapped working capital.

**3. Deploy segmented forecasting policies across all 9 classes.** Cease the one-size-fits-all algorithm approach. Automate forecasting for stable X-class items, deploy seasonal models (Prophet/ETS) for Y-class, and shift to exception-based reactive planning for erratic Z-class items — freeing planner bandwidth to focus on high-impact decisions.

---

## Output Files

| File                                         | Description                                          |
| -------------------------------------------- | ---------------------------------------------------- |
| `data/processed/demand_clean.csv`            | Cleaned dataset — input for all analysis             |
| `outputs/abc_xyz_classification.csv`         | ABC-XYZ classification per SKU (**Project 2 input)** |
| `outputs/abc_xyz_policy_table.csv`           | Full 9-class policy recommendation table             |
| `outputs/chart_01_monthly_demand_trend.png`  | Total monthly demand trend (2011–2017)               |
| `outputs/chart_02a_warehouse_bar.png`        | Warehouse demand concentration                       |
| `outputs/chart_02b_warehouse_subplots.png`   | Monthly demand trend by warehouse                    |
| `outputs/chart_03_pareto_category.png`       | Pareto analysis by product category                  |
| `outputs/chart_04_distribution_outliers.png` | Demand distribution & outlier detection              |
| `outputs/chart_05_top_bottom_products.png`   | Top 10 & Bottom 10 products by demand                |
| `outputs/chart_06_abc_classification.png`    | ABC classification results                           |
| `outputs/chart_07_abcxyz_matrix.png`         | ABC-XYZ 9-cell heatmap matrix                        |

---

## Tech Stack

```
Python      3.11
pandas      2.2.0
numpy       1.26.0
matplotlib  3.8.0
seaborn     0.13.0
```

**Dataset:** [Historical Product Demand — felixzhao](https://www.kaggle.com/datasets/felixzhao/productdemandforecasting) — 1,048,575 records · 4 Warehouses · 2,160+ SKUs · 2011–2017 · Manufacturing

---
## Project Series

| Phase | Repo                                         | Focus                            | Status         |
| ----- | -------------------------------------------- | -------------------------------- | -------------- |
| 01    | **Demand Visibility & Product Segmentation** | ABC-XYZ Framework                | ✅ Complete     |
| 02    | **Cost Diagnosis**                           | STL Decomposition + Safety Stock | 🔄 In Progress |
| 03    | **Demand Forecasting**                       | Prophet + Model Comparison       | ⏳ Planned      |

**Dataset:** All 3 projects use the same `Historical Product Demand` dataset. 

**Narrative:** Each project builds on the previous — segmentation → cost diagnosis → forecasting.

---

_Part of the Supply Chain Demand Analytics Portfolio — built to simulate real-world business impact using Python._


