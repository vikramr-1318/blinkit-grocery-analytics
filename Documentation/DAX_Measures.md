# 🛒 Blinkit Grocery Analytics — DAX Measures Reference Guide

This document catalogs the verified DAX calculations used in the **Blinkit Grocery Sales & Marketing Analytics Dashboard** (`Blinkit Sales Analytics.pbix`).

---

## 📐 Measure Catalog

### 1. Total Revenue
* **DAX Formula:**
  ```dax
  Total Revenue = SUM(Orders[order_total])
  ```
* **Business Definition:** Gross sales revenue generated from all customer orders across the platform.
* **Calculation Logic:** Simple additive aggregation over the `order_total` column in the Orders fact table.
* **Interpretation:** Core top-line growth metric. Current value: **₹4.97M** across 5,000 orders.
* **Use Case:** Executive KPI card and monthly trend analysis.

---

### 2. Total Orders
* **DAX Formula:**
  ```dax
  Total Orders = COUNTROWS(Orders)
  ```
* **Business Definition:** Total number of customer order fulfillment requests placed on Blinkit.
* **Calculation Logic:** Row count of the primary Orders fact table.
* **Interpretation:** Measures platform transaction volume (**5,000 orders**).
* **Use Case:** Operational capacity planning and volume trend tracking.

---

### 3. Total Customers
* **DAX Formula:**
  ```dax
  Total Customers = DISTINCTCOUNT(Orders[customer_id])
  ```
* **Business Definition:** Count of unique transacting individuals during the analysis period.
* **Calculation Logic:** Distinct count of foreign keys (`customer_id`) in the Orders table.
* **Interpretation:** Total unique transacting customer base (**2,500 active customers**).
* **Use Case:** Customer acquisition, repeat purchase rate, and retention analysis.

---

### 4. Average Order Value (AOV)
* **DAX Formula:**
  ```dax
  Avg Order Value = DIVIDE([Total Revenue], [Total Orders], 0)
  ```
* **Business Definition:** Average rupee expenditure per completed order basket.
* **Calculation Logic:** Total Revenue divided by Total Orders with zero-division protection via `DIVIDE()`.
* **Interpretation:** Average basket size is **₹994.48**.
* **Use Case:** Basket-building promotions, minimum order threshold optimization, and pricing strategy.

---

### 5. On-time Delivery %
* **DAX Formula:**
  ```dax
  On-time Delivery % = 
  DIVIDE(
      CALCULATE(COUNTROWS(Orders), Orders[delivery_status] = "On Time"),
      COUNTROWS(Orders),
      0
  )
  ```
* **Business Definition:** Percentage of customer orders fulfilled and delivered on or before the promised delivery timestamp.
* **Calculation Logic:** Count of orders where `delivery_status = "On Time"` divided by total order count.
* **Interpretation:** Current delivery SLA reliability is **69.40%** (30.6% delayed).
* **Use Case:** Quick commerce SLA enforcement, rider fleet allocation, and delivery partner evaluations.

---

### 6. Average Customer Rating (CSAT)
* **DAX Formula:**
  ```dax
  Avg Rating = AVERAGE(Feedback[rating])
  ```
* **Business Definition:** Mean customer satisfaction rating awarded out of 5 stars.
* **Calculation Logic:** Mathematical mean of the `rating` column in the Customer Feedback table.
* **Interpretation:** Overall platform rating is **3.34 ⭐**, indicating operational friction in late deliveries.
* **Use Case:** Customer feedback monitoring, store performance rankings, and quality control.

---

### 7. Campaign Return on Ad Spend (ROAS)
* **DAX Formula:**
  ```dax
  Campaign ROAS = DIVIDE(SUM(Marketing[revenue_generated]), SUM(Marketing[spend]), 0)
  ```
* **Business Definition:** Revenue efficiency multiple generated per rupee of marketing advertising spend.
* **Calculation Logic:** Total marketing revenue divided by total marketing campaign spend.
* **Interpretation:** Platform achieves an aggregate **1.97x ROAS** across acquisition channels.
* **Use Case:** Marketing budget reallocation towards high-efficiency channels (e.g., Google Ads vs Meta).

---

### 8. Average Margin %
* **DAX Formula:**
  ```dax
  Avg Margin % = AVERAGE(Products[margin_percentage])
  ```
* **Business Definition:** Average gross profit margin percentage across cataloged grocery SKUs.
* **Calculation Logic:** Mean of product-level margin percentages.
* **Interpretation:** Average category margin is **27.78%**.
* **Use Case:** Assortment mix optimization, private-label expansion, and vendor price negotiations.

---

### 9. Items Sold
* **DAX Formula:**
  ```dax
  Items Sold = SUM(OrderItems[quantity])
  ```
* **Business Definition:** Total physical units of grocery products delivered to consumers.
* **Calculation Logic:** Sum of units in the `OrderItems` line-item table (**10,034 items**).
* **Use Case:** Warehouse pick-pack throughput, inventory turnover, and logistics capacity.
