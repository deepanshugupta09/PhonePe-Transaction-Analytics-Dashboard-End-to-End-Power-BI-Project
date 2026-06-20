# 📱 PhonePe Payment Insights Dashboard

### Payment insights, powering Bharat — Secure. Simple. Seamless.

An end-to-end **Power BI** dashboard built on a simulated PhonePe transactions dataset, covering the complete analytics workflow: data cleaning → data modeling (DAX) → KPI design → dashboarding → business insights.

![Dashboard Preview]([./screenshots/dashboard_overview.png](https://github.com/deepanshugupta09/PhonePe-Transaction-Analytics-Dashboard-End-to-End-Power-BI-Project/blob/main/Dashboard%20JPG.JPG)

---

## 🎯 Project Objective

To analyze digital payment behavior across PhonePe's user base and uncover patterns in transaction volume, value, service usage, and customer demographics — and translate them into actionable business insights for improving transaction success rates and service adoption.

---

## 🗂️ Dataset Overview

The project uses two core tables:

| Table | Description | Key Fields |
|---|---|---|
| **All_Users** | ~108K unique PhonePe users | User_ID, Name, Age, Age Segment, Join_Date |
| **All_Transactions** | ~300K transaction records | Transaction_ID, Amount, User_ID, Service, Service Type, Payment_Status, Reason, Date |

A custom **Date_Table** was built using DAX to support time-intelligence calculations (Year, Quarter, Month, Weekday/Weekend flags, etc.).

---

## 🧹 Data Cleaning & Preparation

- Corrected spelling and formatting inconsistencies across categorical fields (Service, Service Type, Payment Status, Reason)
- Standardized date formats and removed duplicate/null records
- Created age-based segmentation (Gen Z, Millennials, Gen X, Boomers)
- Built a clean star-schema relationship between Users, Transactions, and Date tables

---

## 🛠️ Data Modeling (DAX)

A custom calendar table was created to power all time-based KPIs:

```dax
Date_Table = ADDCOLUMNS(
    CALENDAR(MIN(ALL_Transactions[Date]), MAX(ALL_Transactions[Date])),
    "YEAR", YEAR([Date]),
    "Month No.", MONTH([Date]),
    "Month", FORMAT([Date], "MMM"),
    "Quater", "Q" & FORMAT([Date], "Q"),
    "Weekday", FORMAT([Date], "dddd"),
    "Day No.", WEEKDAY([Date], 2),
    "Weekend", IF(WEEKDAY([Date], 2) >= 6, "Weekend", "Weekday")
)
```

**Relationships:** A clean star schema connects `All_Users` → `All_Transactions` → `Date_Table` (one-to-many), with a dedicated `Measures` table holding all DAX calculations for easy management.

**Key Measures Built:**
- Total Transaction / Total Transaction Value
- Successful Transaction / Success Rate
- Total Transaction MoM% (Month-over-Month growth)
- Total Transaction PM (Previous Month)
- Unique Users

---

## 📊 Dashboard Features

| Section | Description |
|---|---|
| **KPI Cards** | Total Transactions, Total Value, Unique Users, Success Rate (with MoM % change) |
| **Transactions Over Time** | Dual-axis trend of transaction count vs. transaction value by month |
| **Age Segment Contribution** | Donut chart breaking down transaction share by Gen X, Millennials, Gen Z, Boomers |
| **Service Transaction Value Analysis** | Bar chart comparing Loans, Insurance, Money Transfer, and Recharge & Bills |
| **Top 5 Users (By Transaction Value)** | Ranks highest-value customers |
| **Weekday vs Weekend Usage** | Donut chart comparing transaction split |
| **Dynamic Filters** | Month and Payment Status slicers for interactive exploration |
| **Insights Panel** | Auto-summarized narrative insights for quick business takeaways |

---

## 💡 Key Insights

- Transaction performance is **stable**, with **300K transactions** worth **₹3.47B** in value and a **96% success rate**.
- **Loans** dominate service transaction value, far ahead of Insurance, Money Transfer, and Recharge & Bills.
- **Millennials and Gen X** drive the majority (74.6%) of transaction activity, while **Gen Z and Boomers** remain underrepresented — a clear growth opportunity.
- **Weekday usage (71.6%)** significantly outweighs weekend usage (28.4%), suggesting payment behavior is tied to routine/work-day activity.
- There is room to **reduce failed transactions** and **expand Insurance and Money Transfer adoption** through targeted engagement.

---

## 🧰 Tools & Techniques Used

- **Power BI** (Power Query, Data Modeling, DAX, Visualization)
- **DAX** for calculated columns, custom date table, and KPI measures
- **Star Schema** data modeling
- **Data Cleaning** (Power Query)

---

## 📁 Repository Contents

- `PhonePe_Dashboard.pbix` — Power BI project file
- `Phonepe-Final-Dataset.xlsx` — Cleaned source dataset
- `/screenshots` — Dashboard preview images

---

## 🔗 Connect With Me

- **GitHub:** [github.com/deepanshugupta09](https://github.com/deepanshugupta09)
- **LinkedIn:** [linkedin.com/in/deepanshu-gupta-analyst](https://www.linkedin.com/in/deepanshu-gupta-analyst/)

---

⭐ If you found this project useful, consider giving it a star!
