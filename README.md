# Retail Sales Performance Dashboard (Power BI)

## Project Overview

This project presents an **interactive Power BI dashboard** built on retail order data (*Sample Superstore dataset*).
The goal is to demonstrate end-to-end **business intelligence workflow** including:

* Data modeling with star schema
* DAX measures for KPIs and time intelligence
* Multi-page interactive dashboards for business insights

The report analyzes **sales, profitability, forecasting, and customer behavior** from **2014–2017**, with insights tailored for business stakeholders.

---

## Dataset

* **Source**: Sample Superstore Dataset (public dataset, often used for BI practice).
* **Scope**: 2014–2017 retail orders (US market).
* **Fields**:

  * Orders: Order ID, Order Date, Ship Date, Ship Mode
  * Customers: Customer ID, Name, Segment, Region, State
  * Products: Product ID, Name, Category, Sub-Category
  * Metrics: Sales, Profit, Discount, Quantity

---

## Data Model

The data model follows a **star schema**:

* **Fact_Orders**: Sales transactions (Sales, Profit, Discount, Quantity).
* **Dim_Customers**: Customer attributes (Region, Country, Segment).
* **Dim_Products**: Product attributes (Category, Sub-Category).
* **Dim_Date**: Calendar table (Year, Month, Quarter).
* **_Measures**: Central table containing calculated KPIs in DAX.

The Month Name column is sorted by Month No to force Jan–Dec order. `Discount Band` is a calculated column on `Fact_Orders` used for discount-level analysis.

<img width="2113" height="1032" alt="image" src="https://github.com/user-attachments/assets/3d7f8ba0-1c27-4a88-9e23-10748c89060e" />

---

## Key DAX Measures

Some important DAX measures used in the dashboard:

```DAX
Total Sales = SUM(Fact_Orders[Sales])

Total Profit = SUM(Fact_Orders[Profit])

Profit Margin = DIVIDE([Total Profit], [Total Sales])

Sales YTD = TOTALYTD ( [Total Sales], Dim_Date[Date] )

Sales YoY % = DIVIDE ( [Total Sales] - [Sales YoY], [Sales YoY], 0 )

Avg Order Value = DIVIDE ( [Total Sales], [Order Count], 0 )

Customer Count = DISTINCTCOUNT(Dim_Customers[Customer ID])
```

---

## Dashboard Pages

### 1. Overview

* KPIs: Total Sales, Total Profit, Profit Margin, YoY Growth %
* Line chart: Total Sales by YearMonth
* Map: Sales by State
* Bar chart: Sales by Region
* **Purpose:** Provide a high-level snapshot of sales performance.

<img width="1928" height="1097" alt="image" src="https://github.com/user-attachments/assets/6c2b29a7-4909-43fa-9875-e0344fd9d77c" />

---

### 2. Sales Analysis

* KPI: Top Selling Product, Average Order Value
* Treemap: Sales by Category & Sub-Category
* Combo chart: Sales vs Quantity by Category
* Donut chart: Sales share by Category
* **Purpose:** Compare product performance and identify best sellers.
  
The “Top Selling Product” title is driven by a DAX measure that returns the highest-selling product for the current filter context.

<img width="1927" height="1095" alt="image" src="https://github.com/user-attachments/assets/cb56f76c-7af2-4d2e-a90a-3d31d462550a" />

---

### 3. Profitability

* KPIs: Total Profit, Profit Margin
* Matrix: Profit by Category & Region
* Scatter chart: Discount vs Profit Margin
* Bar chart: Top 10 Products by Profit
* **Purpose:** Analyze profit drivers and impact of discounts.

<img width="1930" height="1098" alt="image" src="https://github.com/user-attachments/assets/518b4182-5530-42e3-a4d4-700cedf3b50f" />

---

### 4. Trend & Forecast

* KPIs: Sales YTD, Sales MoM %
* Line chart: Sales Forecast (Analytics → Forecast enabled)
* Area chart: Cumulative Sales (YTD) by YearMonth
* Slicers: Year, Month Name (Jan–Dec order)
* **Purpose:** Identify sales patterns and forecast future performance.

<img width="1921" height="1092" alt="image" src="https://github.com/user-attachments/assets/6055d989-bf70-441a-baf8-26bf7a1cfad6" />

---

### 5. Customer Analysis

* KPIs: Customer Count, Avg Sales per Customer
* Pie chart: Sales by Customer Name
* Scatter plot: Sales vs Profit by Customer
* **Purpose:** Understand customer contribution and segmentation.

<img width="1921" height="1092" alt="image" src="https://github.com/user-attachments/assets/7c6cde44-42ce-4303-86dd-7f7a698f09ae" />

---

## How to Use

* Use **slicers** to filter data by Year, Month, Region, Category, or Segment.
* Hover over visuals to see **tooltips** with additional details.
* Interact with charts to **cross-filter** other visuals dynamically.

**Example:** Select **2017** in the *Year* slicer → all KPIs, charts, and tables update to reflect **2017 only**.

---

### Interactivity Details

This dashboard is fully interactive:

* **Year / Month slicers**

  * Selecting a year updates all KPIs and visuals for that period.
  * Month slicer is ordered **Jan → Dec** to follow calendar logic.

* **Region & State filters**

  * Map and bar charts respond to regional selections.
  * Useful for identifying geographic performance differences.

* **Category & Sub-Category slicers**

  * Treemap, donut, and combo charts update instantly to show selected product categories.
  * Helps drill down from high-level categories (Technology, Furniture, Office Supplies) to specific products.

* **Discount Range filter**

  * Scatter plot (Discount vs Profit Margin) and Profit KPIs recalculate based on discount bands.
  * Demonstrates impact of discounting strategy on profitability.

* **Cross-filtering**

  * Clicking a bar, pie slice, or scatter point filters the other visuals automatically.
  * Example: Clicking **Technology** in Sales by Category → all visuals update to show only Technology-related data.

This interaction design ensures the dashboard is not static but serves as an **exploratory analysis tool**.

---

## Key Insights

* Discounting strategy impacts profitability: Profit margins drop sharply when discounts exceed 40%, highlighting the need for careful pricing policies.

* Technology as growth driver: The Technology category demonstrates the highest sales growth trend, especially in 2017, indicating strong market demand and potential for expansion.

* Customer concentration effect: A small group of customers (top ~20%) contributes a disproportionately large share of total sales (Pareto principle), suggesting opportunities for targeted retention strategies.

* Regional performance variation: The West region consistently outperforms others in total sales, positioning it as a critical market to focus on for resource allocation and sales strategies.

---

## Files in Repository

* `Sample_Superstore_Analysis.pbix` → Power BI dashboard file
* `Sample - Superstore.csv` → Dataset used in this project
* `README.md` → Project documentation

---

## Next Steps

* Add advanced DAX for dynamic KPI switching (Sales, Profit, Margin).
* Integrate external datasets (e.g., population, economic indicators).
* Deploy online with Power BI Service (Publish to Web).

---

## Author

**Dorothea Gao**
Bachelor of Science in Mathematics & Data Science (University of Sydney)
Power BI PL-300 Certified
