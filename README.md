# 🛒 Ecommerce Sales Dashboard — Revenue, Profitability & Product Intelligence

> A Microsoft Power BI dashboard connected to a **PostgreSQL** backend, built to give ecommerce business leaders a real-time view of sales performance, profitability trends, product rankings, and regional distribution — enabling faster, evidence-based commercial decisions.

![Power BI](https://img.shields.io/badge/PowerBI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-Measures-blue?style=for-the-badge)
![SQL](https://img.shields.io/badge/SQL-Data%20Source-orange?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

---

## 📌 Table of Contents

- [Business Problem](#-business-problem--objective)
- [Dashboard Preview](#-dashboard-preview)
- [Dataset Description](#-dataset-description)
- [Key Insights](#-key-insights)
- [Tools & Technologies](#️-tools--technologies)
- [DAX Measures & SQL Queries](#-dax-measures--sql-queries)
- [Dashboard Features](#-dashboard-features)
- [Project Structure](#-project-structure)
- [How to Use](#-how-to-use)
- [Future Enhancements](#-future-enhancements)
- [Author](#-author)

---

## 🎯 Business Problem & Objective

In ecommerce, the gap between **revenue and profitability** is often invisible until it's too late. A store can be growing in sales while quietly losing margin on underperforming SKUs, inefficient shipping choices, or declining regional demand.

This dashboard was built to answer the most pressing commercial questions facing ecommerce operations teams:

| Business Question | Dashboard Answer |
|---|---|
| Are we growing or declining vs. last year? | YTD vs. PYTD KPI cards with % variance indicators |
| Which product categories are driving — or dragging — revenue? | Sales by Category table with YoY trend arrows |
| Where are our most and least profitable products? | Top 5 and Bottom 5 Products by YTD Sales |
| Which regions represent the biggest opportunity? | YTD Sales by Region donut chart + US state map |
| Is our profit margin improving despite revenue softness? | YTD Profit Margin KPI — 11.35% (▲ 9.60%) |
| How are customers choosing to receive their orders? | YTD Sales by Shipping Type breakdown |
| Does performance differ across Consumer, Corporate, and Home Office? | Segment-level slicer filtering all visuals |

**Objective:** Provide sales, operations, and category management teams with a single source of truth for YTD commercial performance — surfacing risks and opportunities before they impact the bottom line.

---

## 📊 Dashboard Preview

![Ecommerce Sales Dashboard](./Ecommerce_Sales_Dashboard.png)

> **Snapshot — Current Year Performance:**
> - YTD Sales: **$2.06M** (▼ -1.93% vs. prior year)
> - YTD Profit: **$233.68K** (▲ +7.49%)
> - YTD Quantity: **#18.9K** (▼ -10.5%)
> - YTD Profit Margin: **11.35%** (▲ +9.60%)
> - Segments: Consumer | Corporate | Home Office

---

## 🗂️ Dataset Description

The dataset is sourced from a **PostgreSQL database** representing a US-based ecommerce retailer with transactions across multiple product categories, regions, and customer segments.

| Column | Description | Type |
|---|---|---|
| `order_id` | Unique order identifier | VARCHAR |
| `order_date` | Date of transaction | DATE |
| `customer_id` | Unique customer identifier | VARCHAR |
| `customer_segment` | Consumer / Corporate / Home Office | CATEGORICAL |
| `customer_region` | Central / East / South / West | CATEGORICAL |
| `state` | US state of delivery | VARCHAR |
| `category_name` | Furniture / Technology / Office Supplies | CATEGORICAL |
| `product_name` | Individual product name | VARCHAR |
| `sales` | Revenue from the transaction (USD) | DECIMAL |
| `quantity` | Units sold | INTEGER |
| `discount` | Discount applied (0.0–1.0) | DECIMAL |
| `profit` | Net profit after costs and discounts | DECIMAL |
| `ship_mode` | Standard / Second / First Class / Same Day | CATEGORICAL |

**Data Source:** PostgreSQL database (connected live via Power BI DirectQuery / Import mode)
**Scope:** Multi-year transactional data | **Current Year Records:** ~5,000+ orders

---

## 💡 Key Insights

Insights are framed as business decisions, not just data observations — the standard expected at analyst and senior analyst levels.

### 📉 Revenue vs. Profitability Divergence — The Critical Story

1. **Revenue is down (-1.93% YTD) but profit is up (+7.49%)** — This counter-intuitive dynamic signals a deliberate or emerging shift: the business is selling less but at better margins. This could indicate successful discount reduction, a mix shift toward higher-margin products, or the elimination of loss-making SKUs. **Action:** Identify which categories drove the margin expansion and replicate the strategy.

2. **Office Supplies generates the highest revenue ($1.21M) but carries the worst YoY trend (-4.67%)** — Despite being the volume leader, this category is deteriorating fastest. With Furniture (+3.23%) and Technology (+1.20%) both growing year-over-year, a portfolio rebalancing strategy toward tech and furniture could protect overall revenue. **Action:** Audit Office Supplies pricing, competition exposure, and customer churn within this category.

3. **The West region leads with 31.73% of YTD sales** — outpacing East (29.34%), Central (23.28%), and South (15.65%). The South is dramatically underrepresented relative to its US population share. **Action:** Investigate whether this is a logistics gap, marketing underinvestment, or a genuine demand signal — and size the opportunity.

### 📦 Product Portfolio Insights

4. **Easy-staple paper ($14K) leads Top 5 by a wide margin** — a low-cost consumable commodity driving volume. This is likely a high-frequency, low-margin product. Its dominance in the top 5 suggests the assortment may be over-indexed on commodity items. **Action:** Cross-sell higher-margin products to frequent commodity buyers.

5. **The Bottom 5 products collectively generate under $1K in YTD sales** — Products like Fellowes Super St. ($0.11K) and Tennsco Stur-D-St. ($0.12K) are dead weight in the catalog. Carrying, marketing, and warehousing these SKUs has a real cost. **Action:** Flag for discontinuation or promotional clearance.

### 🚚 Shipping & Operational Insights

6. **Standard Class shipping dominates at 60.9%** — confirming customers prioritize cost over speed. However, Same Day (4.94%) and First Class (15.57%) together represent 20%+ of orders. **Action:** Analyze whether premium shipping customers have higher average order values or margins — if yes, they warrant a loyalty or upsell program.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **Microsoft Power BI Desktop** | Dashboard design, data modeling, and interactive visualizations |
| **PostgreSQL** | Primary data source — transactional ecommerce data |
| **Power Query (M Language)** | Data transformation, joins, and type casting post-SQL extraction |
| **DAX (Data Analysis Expressions)** | YTD, PYTD, YoY variance, profit margin calculations |
| **Bing Maps (Power BI)** | Geographic bubble map for state-level sales distribution |
| **Power BI Service** *(optional)* | Cloud publishing, scheduled refresh, and sharing |

---

## 🧮 DAX Measures & SQL Queries

### Core DAX Measures

```DAX
-- ─────────────────────────────────────────
-- 1. Year-to-Date Sales
-- ─────────────────────────────────────────
YTD Sales =
TOTALYTD(
    SUM(Orders[Sales]),
    'Date'[Date]
)

-- ─────────────────────────────────────────
-- 2. Prior Year-to-Date Sales
-- ─────────────────────────────────────────
PYTD Sales =
CALCULATE(
    [YTD Sales],
    SAMEPERIODLASTYEAR('Date'[Date])
)

-- ─────────────────────────────────────────
-- 3. Year-over-Year Sales Variance (%)
-- ─────────────────────────────────────────
YoY Sales % =
DIVIDE(
    [YTD Sales] - [PYTD Sales],
    [PYTD Sales],
    0
)

-- ─────────────────────────────────────────
-- 4. YTD Profit
-- ─────────────────────────────────────────
YTD Profit =
TOTALYTD(
    SUM(Orders[Profit]),
    'Date'[Date]
)

-- ─────────────────────────────────────────
-- 5. YTD Profit Margin (%)
-- ─────────────────────────────────────────
YTD Profit Margin =
DIVIDE(
    [YTD Profit],
    [YTD Sales],
    0
)

-- ─────────────────────────────────────────
-- 6. YTD Quantity Sold
-- ─────────────────────────────────────────
YTD Quantity =
TOTALYTD(
    SUM(Orders[Quantity]),
    'Date'[Date]
)

-- ─────────────────────────────────────────
-- 7. YoY Profit Margin Variance
-- ─────────────────────────────────────────
YoY Margin % =
VAR CurrentMargin = [YTD Profit Margin]
VAR PriorMargin =
    CALCULATE(
        [YTD Profit Margin],
        SAMEPERIODLASTYEAR('Date'[Date])
    )
RETURN
    DIVIDE(CurrentMargin - PriorMargin, ABS(PriorMargin), 0)

-- ─────────────────────────────────────────
-- 8. Dynamic KPI Trend Color (Conditional)
-- ─────────────────────────────────────────
Sales Trend Color =
IF([YoY Sales %] >= 0, "Green", "Red")
```

### SQL Extraction Query (PostgreSQL)

```sql
-- Base query used to extract and load data into Power BI
SELECT
    o.order_id,
    o.order_date,
    o.ship_mode,
    c.customer_id,
    c.segment       AS customer_segment,
    c.region        AS customer_region,
    c.state,
    p.category      AS category_name,
    p.product_name,
    od.sales,
    od.quantity,
    od.discount,
    od.profit
FROM
    orders o
    JOIN customers c   ON o.customer_id = c.customer_id
    JOIN order_details od ON o.order_id = od.order_id
    JOIN products p    ON od.product_id = p.product_id
ORDER BY
    o.order_date ASC;
```

---

## ✨ Dashboard Features

| Feature | Description |
|---|---|
| **4 Sparkline KPI Cards** | YTD Sales, Profit, Quantity, and Profit Margin — each with YoY variance badge (▲/▼) and mini trend line |
| **Segment Slicer** | Filter entire dashboard by Consumer, Corporate, or Home Office segment |
| **Sales by Category Table** | YTD Sales, PYTD Sales, YoY % variance, and color-coded trend arrows per category |
| **Top 5 Products Bar Chart** | Ranked horizontal bars showing best-performing products by YTD revenue |
| **Bottom 5 Products Bar Chart** | Highlights underperforming SKUs — critical for catalog rationalization decisions |
| **YTD Sales by Region Donut** | Four-region breakdown (West, East, Central, South) with percentage labels |
| **Sales by State Bubble Map** | Geographic Bing Map with region-color-coded bubbles proportional to state-level sales |
| **Shipping Type Pie Chart** | Breakdown of Standard / Second / First Class / Same Day fulfillment share |
| **Full Cross-filtering** | All visuals respond to each other — click any element to drill into that slice |

---

## 📁 Project Structure

```
ecommerce-sales-dashboard/
│
├── 📂 data/
│   └── ecommerce_data.sql              # PostgreSQL schema + sample seed data
│
├── 📂 dashboard/
│   └── Ecommerce_Sales_Dashboard.pbix  # Power BI file (data embedded)
│
├── 📂 images/
│   └── Ecommerce_Sales_Dashboard.png   # Dashboard screenshot for README
│
├── 📂 dax/
│   └── measures.dax                    # All DAX measures in plain text
│
├── 📂 sql/
│   └── extraction_query.sql            # SQL query used to extract data
│
└── README.md                           # This file
```

---

## 🚀 How to Use

### For Recruiters & Viewers
The dashboard screenshot above provides a full visual overview. To explore the **interactive version**:

1. Download `Ecommerce_Sales_Dashboard.pbix` from the `/dashboard` folder
2. Open it using **[Power BI Desktop](https://powerbi.microsoft.com/desktop/)** (free)
3. Data is pre-embedded — no database connection required to view
4. Use the **Segment buttons** (Consumer / Corporate / Home Office) to filter all visuals
5. Click any chart element to cross-filter the entire report in real-time

> 💡 *To reconnect to a live PostgreSQL database: Go to Home → Transform Data → Data Source Settings and update the server credentials.*

### For Developers & Analysts

```bash
# 1. Clone the repository
git clone https://github.com/YOUR_USERNAME/ecommerce-sales-dashboard.git

# 2. Navigate into the project
cd ecommerce-sales-dashboard

# 3. (Optional) Load data into PostgreSQL
psql -U your_username -d your_database -f data/ecommerce_data.sql

# 4. Open dashboard in Power BI Desktop
# File → Open → dashboard/Ecommerce_Sales_Dashboard.pbix
```

---

## 🔮 Future Enhancements

- [ ] Add a **Customer Cohort & RFM Analysis** page (Recency, Frequency, Monetary segmentation)
- [ ] Build a **Discount Impact Analysis** — correlating discount depth with profit margin erosion
- [ ] Create a **Monthly Forecasting Page** using Power BI's built-in forecasting visuals
- [ ] Add **Return Rate tracking** to surface true net revenue per product
- [ ] Connect to **live PostgreSQL** with scheduled refresh via Power BI Service
- [ ] Build a **Mobile-optimized layout** for on-the-go executive review

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**[Your Full Name]**
*Data Analyst | Power BI Developer | Ecommerce Analytics*

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=for-the-badge&logo=linkedin)](https://linkedin.com/in/YOUR_PROFILE)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?style=for-the-badge&logo=github)](https://github.com/YOUR_USERNAME)
[![Portfolio](https://img.shields.io/badge/Portfolio-Visit-orange?style=for-the-badge)](https://YOUR_PORTFOLIO_SITE)

---

> 💼 *This project demonstrates the full data analyst workflow — SQL extraction from PostgreSQL, data modeling in Power Query, advanced DAX time-intelligence measures, and business-insight-driven dashboard design in Power BI.*

> ⭐ If this project helped or inspired you, please consider giving it a star!
