#  Maven Market Power BI Dashboard

The dashboard analyzes retail data from **Maven Market** to explore business performance using Microsoft Power BI.

---

##  Objective

The goal of this project is to analyze Maven Market’s 1997–1998 transactions to:
- Calculate key performance indicators (KPIs),
- Identify profit and revenue trends,
- Evaluate return rates,
- Visualize sales by region, product, and time period.

---

##  1. Data Preparation (Power Query)

**Data Sources:**
- `MavenMarket_Customers.csv`
- `MavenMarket_Products.csv`
- `MavenMarket_Stores.csv`
- `MavenMarket_Regions.csv`
- `MavenMarket_Calendar.csv`
- `MavenMarket_Returns.csv`
- `MavenMarket_Transactions_1997.csv`
- `MavenMarket_Transactions_1998.csv`

**Main steps:**
- Regional Settings → `English (United States)`
- Correct data types for each column
- Created new columns:
  - `full_name`, `birth_year`, `has_children`
  - `discount_price`, `full_address`, `area_code`
  - `Start of Week`, `Day Name`, `Quarter of Year`, `Year`, etc.
- Replaced null values with `0`
- Combined transaction files from a folder
- Disabled “Include in Report Refresh” for lookup tables

---

##  2. Data Modeling

Model organized with **lookup tables on top** and **data tables at the bottom**.

**Relationships:**
- `Transaction_Data` ↔ `Customers`, `Products`, `Stores`, `Calendar`
- `Return_Data` ↔ `Products`, `Stores`, `Calendar`
- `Stores` ↔ `Regions` (snowflake model)

All relationships are **1:* (single direction)**.  
Date columns formatted as `M/d/yyyy`; price columns formatted as **Currency**.

---

##  3. DAX Calculations

###  Calculated Columns
| Table | Column | Description |
|--------|---------|-------------|
| **Calendar** | Weekend, End of Month | Flags weekends and month-ends |
| **Customers** | Current Age, Priority, Short_Country, House Number | Customer demographic logic |
| **Products** | Price_Tier | Classifies products by retail price (High / Mid / Low) |
| **Stores** | Years_Since_Remodel | Calculates years since the last remodel |

---

###  Measures (KPIs)
- **Quantity Sold:** 833,489  
- **Quantity Returned:** 8,289  
- **Total Transactions:** 269,720  
- **Total Returns:** 7,087  
- **Return Rate:** 0.99%  
- **Weekend Transactions:** 76,608  
- **% Weekend Transactions:** 28.4%  
- **Total Revenue:** \$1,764,546  
- **Total Cost:** \$711,728  
- **Total Profit:** \$1,052,819  
- **Profit Margin:** 59.67%  
- **Unique Products:** 1,560  
- **YTD Revenue:** \$872,924 (as of Sep 1998)  
- **60-Day Revenue:** \$97,570 (on 14-Apr-1997)  
- **Revenue Target:** Last Month Revenue × 1.05  

---

##  4. Dashboard Design

**Report name:** `Topline Performance`

**Visual Elements:**
-  **Matrix:** Product Brand vs Transactions, Profit, Margin, Return Rate  
-  **KPI Cards:** Current Month Transactions, Profit, Returns (vs previous month)  
-  **Map:** Total Transactions by Store City  
-  **Treemap:** Country → State → City drill-down  
-  **Clustered Column Chart:** Weekly Revenue Trending (1998)  
-  **Gauge:** Revenue vs Target  
-  **Bookmarks:** “Portland 1000 Sales” + additional insights  

---

##  5. Tools & Technologies

- **Microsoft Power BI Desktop**
- **Power Query (M Language)**
- **DAX (Data Analysis Expressions)**
- **Data Modeling & Relationships**
- **Data Visualization & KPI Design**

---

##  Project Structure

# MavenMarket-Analysis
