# 🛒 Blinkit Grocery Sales & Marketing Analytics Dashboard

> **Project Status:** Completed (January 22, 2025) | **Maintainer:** R Vikram

## 1. Project Title & Overview
**Blinkit Grocery Sales & Marketing Analytics** is an end-to-end quick commerce analytics solution delivering 360° visibility into commercial performance, fulfillment logistics, customer sentiment, and marketing acquisition efficiency. The project analyzes ₹4.97M in gross revenue across 5,000 orders using an 8-table relational Star Schema modeled in Power BI.

---

## 2. Business Problem
In the hyper-competitive quick commerce sector (10–15 minute delivery promises), profitability hinges on tight unit economics, route-level delivery punctuality, and marketing capital allocation. Blinkit decision-makers required answers to four strategic questions:
1. Where are order fulfillment delays occurring, and how severely do delivery delays depress customer satisfaction (CSAT)?
2. Which grocery categories generate sustainable gross margins versus high warehouse spoilage/damage rates?
3. What is the true return on advertising spend (ROAS) across paid marketing channels?
4. How can dark stores balance inventory stock levels against constrained product shelf-lives?

---

## 3. Project Objectives
* Design and implement an 8-table relational Star Schema model optimized for rapid DAX aggregation.
* Standardize dirty timestamps, fill null delivery delay reasons, and clean whitespace using Python (Pandas).
* Validate key commercial KPIs using pure SQL queries (`blinkit_queries.sql`).
* Build a 4-page executive Power BI dashboard with a custom dark-mode neon green palette.
* Provide actionable merchandising, logistics, and paid media recommendations.

---

## 4. Dataset Description
* **Source:** [Kaggle - Blinkit Sales Dataset](https://www.kaggle.com/datasets/akxiit/blinkit-sales-dataset)
* **Tables:** 8 Normalized CSV Files (`Customers`, `Orders`, `OrderItems`, `Products`, `Delivery`, `Feedback`, `Marketing`, `Inventory`) + 2 Excel Icon Lookup Tables.
* **Total Records:** 98,000+ rows across all operational entities.
* **Timeframe:** Multi-month operational log across dark store fulfillment hubs.

---

## 5. Tools & Technologies
* **Power BI Desktop:** Multi-page dashboard, Star Schema relationship modeling, custom theme JSON.
* **DAX:** 13+ advanced measures (`SUMX`, `DIVIDE`, `CALCULATE`, `FILTER`).
* **Python (Pandas, Pillow):** Multi-table data cleaning pipeline and custom 1080p canvas background generation.
* **SQL (ANSI SQL / MySQL):** Relational schema DDL, KPI validation queries, and channel attribution logic.
* **Excel:** Category and rating visual iconography lookup tables.

---

## 6. Data Architecture (Star Schema)
```
                          ┌────────────────────────┐
                          │       Customers        │
                          └───────────┬────────────┘
                                      │ 1
                                      │
                                      │ N
┌─────────────────┐ 1             N ┌─┴──────────────────────┐ 1             N ┌─────────────────┐
│    Products     ├─────────────────┤        Orders          ├─────────────────┤    Delivery     │
└────────┬────────┘                 └─┬──────────────────────┘                 └─────────────────┘
         │ 1                          │ 1
         │                            │
         │ N                          │ N
┌────────┴────────┐                 ┌─┴──────────────────────┐
│   OrderItems    │                 │       Feedback         │
└─────────────────┘                 └────────────────────────┘
```

---

## 7. Data Cleaning Methodology
Data processing is automated via [process_blinkit_data.py](process_blinkit_data.py):
1. **String Normalization:** Stripped carriage returns (`\r`), newlines (`\n`), and extraneous whitespace from all text attributes.
2. **Date Standardization:** Converted heterogeneous date formats (`DD-MM-YYYY` and `YYYY-MM-DD HH:MM:SS`) to standard ISO timestamps.
3. **Missing Value Imputation:** Imputed missing values in `reasons_if_delayed` with `'On Time'` to prevent reporting biases.
4. **Relational Integrity:** Verified zero orphan order items or missing product IDs.

---

## 8. SQL Analysis
The project includes a complete production-grade SQL script in [blinkit_queries.sql](blinkit_queries.sql) containing:
* Database DDL table definitions and primary key constraints.
* KPI validation queries (Gross Revenue, AOV, Delivery Punctuality Rate).
* Category profitability rankings and warehouse damage rates.
* Marketing channel ROAS calculations and sentiment distribution.

---

## 9. Python Implementation
* **[process_blinkit_data.py](process_blinkit_data.py):** Automated multi-table ETL pipeline.
* **[generate_blinkit_bg.py](generate_blinkit_bg.py):** Generates 1920x1080 dark charcoal canvas with Blinkit neon green divider accents.

---

## 10. Power BI Dashboard
The dashboard [Blinkit Sales Analytics.pbix](Blinkit%20Sales%20Analytics.pbix) comprises four dedicated analytical views:
1. **Business Overview:** Top-level revenue KPIs, monthly order trajectory, payment mix, and delivery status breakdown.
2. **Product Analysis:** Category revenue breakdown, top brands treemap, and profit margin vs sales volume matrix.
3. **Delivery & Feedback:** On-time fulfillment %, delay driver analysis, CSAT by customer segment, and review categories.
4. **Revenue & Marketing:** Channel spend vs attributed revenue, campaign ROAS comparison, and impression-to-conversion funnel.

---

## 11. Dashboard Screenshots
Dashboard preview assets are located in the [Screenshots/](Screenshots/) directory:

![Dashboard Theme Preview](Screenshots/01_dashboard_canvas_theme.png)

*The complete interactive dashboard can be explored via [Blinkit Sales Analytics.pbix](Blinkit%20Sales%20Analytics.pbix).*

---

## 12. Key Performance Indicators (KPIs)
| KPI | Value | Business Significance |
|:---|:---:|:---|
| **Total Revenue** | ₹4.97M | Gross merchandise sales volume |
| **Total Orders** | 5,000 | Total customer fulfillment cycles |
| **Total Customers** | 2,500 | Unique transacting user base |
| **Average Order Value (AOV)** | ₹994.48 | Mean basket expenditure |
| **On-Time Delivery %** | 69.40% | Quick-commerce 15-minute SLA fulfillment |
| **Average CSAT Rating** | 3.34 ⭐ | Customer feedback score out of 5 stars |
| **Average Gross Margin** | 27.78% | Catalog profitability margin |
| **Marketing Campaign ROAS** | 1.97x | Revenue return per advertising rupee |

---

## 13. Business Insights
*Detailed insights available in [Documentation/Blinkit_Analytics_Insights.md](Documentation/Blinkit_Analytics_Insights.md).*
* **SLA Delay Penalty:** On-time deliveries average **4.45 ⭐**, while late deliveries crash to **1.85 ⭐**, driving overall CSAT down to 3.34.
* **Peak Bottlenecks:** 42% of late deliveries occur during the 7 PM – 10 PM dinner rush due to temporary rider shortages.
* **Marketing Efficiency:** Google Search Ads deliver 2.45x ROAS (high-intent), whereas Meta Social Ads achieve 1.65x ROAS (awareness).

---

## 14. Strategic Recommendations
1. **Peak Dynamic Surcharging:** Introduce dynamic delivery fee surcharges during dinner rush and heavy rainfall to subsidize extra rider incentives.
2. **High-Margin Bundles:** Bundle low-margin perishables (Dairy) with high-margin items (Personal Care/Snacks) to lift AOV beyond ₹1,200.
3. **Inventory Reorder Automation:** Implement automated safety stock triggers for Dairy & Bakery SKUs with under 3 days of shelf life.

---

## 15. Project Folder Structure
```
Blinkit Grocery Analytics/
│
├── Blinkit Sales Analytics.pbix         # Interactive Power BI report
├── Blinkit_Theme.json                   # Custom visual palette theme
├── Blinkit_Background.png               # High-res canvas background
├── blinkit_queries.sql                  # Comprehensive SQL query suite
├── process_blinkit_data.py              # Automated data cleaning pipeline
├── generate_blinkit_bg.py               # Background generation script
├── requirements.txt                     # Python dependencies
├── Customers.csv                        # Cleaned Customers entity
├── Orders.csv                           # Cleaned Orders fact table
├── OrderItems.csv                       # Order line item junction table
├── Products.csv                         # Products dimension table
├── Delivery.csv                         # Delivery performance table
├── Feedback.csv                         # Customer reviews & CSAT ratings
├── Marketing.csv                        # Paid campaign performance
├── Inventory.csv                        # Stock levels & damaged units
├── Documentation/
│   ├── DAX_Measures.md                  # Comprehensive DAX catalog
│   └── Blinkit_Analytics_Insights.md    # Analytical business findings
└── Screenshots/
    └── 01_dashboard_canvas_theme.png    # Dashboard canvas preview
```

---

## 16. Installation Instructions
```bash
# Clone the repository
git clone https://github.com/vikramr-1318/Data-Analyst-Portfolio.git
cd "Data-Analyst-Portfolio/Blinkit Grocery Analytics"

# Install required Python dependencies
pip install -r requirements.txt
```

---

## 17. Execution Instructions
```bash
# Execute data cleaning pipeline:
python process_blinkit_data.py

# Regenerate dark-mode canvas background:
python generate_blinkit_bg.py
```

---

## 18. Dataset Download Instructions
Raw files can be re-acquired from [Kaggle - Blinkit Sales Dataset](https://www.kaggle.com/datasets/akxiit/blinkit-sales-dataset). Place the raw CSVs into this folder and execute `python process_blinkit_data.py`.

---

## 19. Limitations & Future Work
* **Geospatial Route Data:** Dataset lacks live GPS coordinates for route latency optimization.
* **Future Work:** Integrate real-time weather and traffic telemetry to dynamically predict delivery SLA times.

---

## 20. Contact & Maintainer
* **Developer & Maintainer:** R Vikram
* **GitHub:** [vikramr-1318](https://github.com/vikramr-1318)
* **Email:** `rv367629@gmail.com`
