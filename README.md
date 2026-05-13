# 🚖 Ola Cab — Ride Booking & Operations Analytics

<div align="center">

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Dataset](https://img.shields.io/badge/Dataset-20%2C407%20Bookings-orange?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)
![Domain](https://img.shields.io/badge/Domain-Ride--Hailing%20%7C%20Urban%20Mobility-blueviolet?style=for-the-badge)

**A full-stack data analytics project on 20,407 Bengaluru Ola ride bookings (July 2024) — combining SQL for structured querying and a 5-page interactive Power BI dashboard to surface operational, revenue, cancellation, and service quality insights.**

[🔍 Problem Statement](#-problem-statement) · [📁 Repo Structure](#-repository-structure) · [🛠️ Tech Stack](#️-tech-stack) · [📊 Dashboards](#-dashboard-previews) · [💡 Key Insights](#-key-insights) · [⚙️ Setup](#️-setup--how-to-use) · [🚀 Future Scope](#-future-scope--whats-next)

</div>

---

## 📌 Problem Statement

> **The challenge:** Ride-hailing platforms generate thousands of booking records daily — but raw transactional data across booking statuses, vehicle types, cancellation reasons, payment methods, and ride distances gives operations and product teams no immediate way to understand *what's working, what's failing, and why.*

Three core business pain points drive this analysis:

- **Cancellation blind spots** — With 5,735 cancelled bookings across a single month, the root causes (driver behaviour, vehicle issues, customer-side reasons) are buried in raw data and invisible without structured querying
- **Revenue & payment gaps** — Understanding where the ₹11.1M total booking value is being lost vs. converted, and which payment channels customers actually use, is critical for product and finance decisions
- **Service quality consistency** — Do ratings vary across vehicle tiers? Are drivers and customers rating each other equitably? Is the experience uniform or fragmented?

This project answers all three by building a **10-query SQL analytical layer** over the bookings dataset, then surfacing every finding through a **5-page interactive Power BI dashboard** — the same end-to-end workflow used by data and operations analysts at ride-hailing companies.

---

## 📁 Repository Structure

```
Ola-Cab-Analysis/
│
├── 📄 Bookings.csv               # Raw dataset — 20,407 Bengaluru Ola bookings
│                                 # July 1–30, 2024 | 19 columns
│                                 # Fields: Date, Time, Booking_ID, Booking_Status,
│                                 # Customer_ID, Vehicle_Type, Pickup_Location,
│                                 # Drop_Location, V_TAT, C_TAT,
│                                 # Canceled_Rides_by_Customer,
│                                 # Canceled_Rides_by_Driver, Incomplete_Rides,
│                                 # Incomplete_Rides_Reason, Booking_Value,
│                                 # Payment_Method, Ride_Distance,
│                                 # Driver_Ratings, Customer_Rating
│
├── 🗄️ ola-analysis.sql          # MySQL script — schema creation, data load,
│                                 # 10 analytical queries each saved as SQL Views
│
└── 📊 ola dashboard.pbix        # Power BI report — 5-page interactive dashboard
                                  # Overall · Vehicle Type · Revenue ·
                                  # Cancellation · Ratings
```

---

## 🛠️ Tech Stack

| Tool | Purpose | Why It Was Used |
|------|---------|-----------------|
| **MySQL Workbench** | Schema design, data loading & EDA | SQL is the standard for querying transactional booking data; Views allow reusable, named query results that mirror how analysts work in production environments |
| **SQL Views** | Storing 10 analytical query results | Each business question is encapsulated as a named View (e.g., `Successful_Bookings`, `Avg_ride_distance_for_each_vehicle_type`) — making queries reusable and report-ready |
| **Power BI Desktop** | 5-page interactive dashboard | Native support for KPI cards, donut charts, pie charts, bar charts, date slicers, and matrix tables — ideal for operational analytics across multiple business dimensions |
| **DAX (Data Analysis Expressions)** | Calculated measures & KPIs | Powers dynamic metrics — total booking value, successful booking count, cancelled bookings, per-vehicle aggregations — all updating live with slicer selections |
| **Power Query (M)** | ETL & data transformation | Loads and shapes `Bookings.csv` into a clean data model, handling date parsing, null treatment, and column typing before the DAX layer runs |
| **CSV (Bookings.csv)** | Raw data source | Flat-file format that is portable, version-controllable, and directly importable into both MySQL and Power BI without conversion |

---

## 🗄️ SQL Analysis — 10 Business Questions

All queries are written as **reusable SQL Views**, so each answer can be recalled with a single `SELECT * FROM <view_name>` statement.

| # | Business Question | View Name |
|---|-------------------|-----------|
| 1 | Retrieve all successful bookings | `Successful_Bookings` |
| 2 | Find average ride distance for each vehicle type | `Avg_ride_distance_for_each_vehicle_type` |
| 3 | Get total number of rides cancelled by customers | `cancelled_rides_by_the_customers` |
| 4 | List top 5 customers who booked the highest number of rides | `top_5_customers_who_booked_the_highest_number_of_rides` |
| 5 | Get rides cancelled by drivers due to personal & car related issues | `rides_cancelled_by_drivers_personal_car_related_issues` |
| 6 | Find max and min driver ratings for Prime Sedan bookings | `max_and_min_driver_ratings_for_Prime_Sedan` |
| 7 | Retrieve all rides where payment was made via UPI | `payment_made_using_UPI` |
| 8 | Find average customer rating per vehicle type | `avg_customer_rating_per_vehicle_type` |
| 9 | Calculate total booking value of successfully completed rides | `total_booking_value_of_rides_successful` |
| 10 | List all incomplete rides along with their reason | `incomplete_rides_along_with_reason` |

---

## 📊 Dashboard Previews

The Power BI report is structured across **5 focused pages**, each answering a distinct set of business questions. Every page includes a **date range slicer** (01-07-2024 to 30-07-2024) for time-filtered exploration.

---

### Page 1 — Overall Summary
> *Total bookings, total booking value, booking status breakdown (donut), and ride volume over time (dual-axis bar+line).*

![Overall Dashboard](./Overall.png)

---

### Page 2 — Vehicle Type Performance
> *Per-vehicle breakdown of total booking value, successful booking value, average distance, and total distance travelled.*

![Vehicle Type Dashboard](./Vehicle_Type.png)

---

### Page 3 — Revenue Analysis
> *Revenue by payment method (bar chart), daily ride distance trend (July 1–30), and top 5 customers by total booking value.*

![Revenue Dashboard](./Revenue.png)

---

### Page 4 — Cancellation Analysis
> *Cancellation reasons split by customer (pie) and driver (pie), with total bookings, successful bookings, and cancelled bookings as KPI cards.*

![Cancellation Dashboard](./Cancellation.png)

---

### Page 5 — Ratings Analysis
> *Driver and customer average ratings displayed as a comparison grid across all 7 vehicle types.*

![Ratings Dashboard](./Ratings.png)

---

## 🔍 Key Insights

> *All figures verified directly against `Bookings.csv` (20,407 rows) and confirmed against the dashboard screenshots. No numbers are assumed or estimated.*

---

### 📦 Overall Booking Performance

- **20,407 total bookings** were recorded across July 2024, with a **total booking value of ₹11,148,671**
- **12,652 bookings (62%) were successful**, generating **₹6,900,234 in realised revenue** — the remainder represents unrecovered demand
- **Booking status breakdown:** Success 62% · Cancelled by Driver 17.91% · Cancelled by Customer 10.2% · Driver Not Found 9.9%
- **5,735 bookings did not complete**, split across three failure modes — driver cancellations being the single largest category at 3,654 rides
- Ride volume across July shows **consistent daily demand** with no extreme outlier days, confirming steady operational load throughout the month

---

### 🚗 Vehicle Type Insights

- **7 vehicle categories** are tracked: Prime Sedan, Prime SUV, Prime Plus, Mini, Auto, Bike, and E-Bike — roughly equal in booking volume (~2,800–3,000 each)
- **Prime Sedan** leads in total booking value at **₹1.67M** and successful booking value at **₹1.06M** — the highest absolute revenue converter in the fleet
- **Bike** records the highest average ride distance at **25.70 km**, followed closely by Prime SUV (25.07 km), Mini (25.02 km), and E-Bike (25.16 km)
- **Auto** is the clear short-haul category — average distance of just **10.00 km** and 18.12K total km, roughly 60% lower than any other vehicle type
- All vehicle types show a **significant gap between total and successful booking value**, confirming that cancellations affect revenue uniformly across the fleet rather than being concentrated in one category

---

### 💰 Revenue & Payment Insights

- **Cash is the dominant payment method** — 6,934 rides paid in cash vs. 5,113 via UPI, making cash ~57% of all payment-recorded rides
- **Credit Card (480 rides) and Debit Card (125 rides) together account for under 5%** of transactions — extremely low card adoption for a tech platform
- The **top 5 customers by booking value** (from the Revenue dashboard) collectively contribute ₹17,010, led by CID836942 at ₹3,757 — a high-value retention segment
- **Daily ride distance is stable** across all 30 days in July, ranging between ~8K–11K km/day with a peak around July 22 — no demand crash or surge event in the dataset

---

### ❌ Cancellation Insights

*Verified against raw CSV counts.*

**Customer Cancellations (2,081 total):**

| Reason | Count | Share |
|--------|-------|-------|
| Driver is not moving towards pickup location | 610 | 29.31% |
| Driver asked to cancel | 552 | 26.53% |
| Change of plans | 408 | 19.61% |
| AC is Not working | 320 | 15.38% |
| Wrong Address | 191 | 9.18% |

- The **top 2 customer cancellation reasons (56%) are both driver-behaviour failures** — the driver not moving and the driver asking the customer to cancel. These are platform-controllable, not demand-side problems.
- **"AC is Not Working" (15.38%)** is a fully preventable, vehicle-maintenance-driven loss — a direct cost of skipping pre-ride vehicle checks

**Driver Cancellations (3,654 total):**

| Reason | Count | Share |
|--------|-------|-------|
| Personal & Car related issue | 1,263 | 34.56% |
| Customer related issue | 1,064 | 29.12% |
| Customer was coughing/sick | 742 | 20.31% |
| More than permitted people in there | 585 | 16.01% |

- **"Personal & Car related issue" at 34.56% (1,263 rides)** is the single largest cancellation driver across the entire dataset — a fleet readiness and driver accountability problem
- **"Customer was coughing/sick" (20.31%)** and **"More than permitted people" (16.01%)** together account for 36% of driver cancellations — both pointing to a need for better pre-ride customer screening tools

---

### 🔧 Incomplete Rides

- **795 rides were marked Incomplete** with three tracked reasons:
  - **Vehicle Breakdown: 322 rides (40.5%)** — the leading cause, a direct fleet maintenance signal
  - **Customer Demand: 313 rides (39.4%)** — customer-initiated mid-ride stops
  - **Other Issue: 160 rides (20.1%)**

---

### ⭐ Ratings Insights

*All averages verified from raw CSV data.*

**Driver Ratings by Vehicle Type:**

| Vehicle | Avg Driver Rating |
|---------|------------------|
| Prime Plus | 4.01 |
| Prime Sedan | 4.00 |
| Prime SUV | 4.00 |
| E-Bike | 4.00 |
| Mini | 3.99 |
| Auto | 3.99 |
| Bike | 3.99 |

**Customer Ratings by Vehicle Type:**

| Vehicle | Avg Customer Rating |
|---------|---------------------|
| Mini | 4.02 |
| Auto | 4.00 |
| Prime Plus | 4.00 |
| Prime Sedan | 3.99 |
| Prime SUV | 3.98 |
| Bike | 3.98 |
| E-Bike | 3.98 |

- **Ratings are uniform across all 7 vehicle types** — the entire fleet sits within a 0.04-point band (3.98–4.02) for both driver and customer ratings
- **Prime Sedan driver ratings range from 3.0 (min) to 5.0 (max)** — confirming individual variance exists, but the average is pulled to a consistent mid-point
- **Mini leads customer ratings at 4.02** despite being a budget category — confirming that value-for-money expectations are being met or exceeded
- Driver and customer ratings **mirror each other closely** across all categories, indicating a mutually respectful and balanced service experience with no vehicle type as a systemic outlier

---

## ⚙️ Setup & How to Use

### Prerequisites

- **MySQL Workbench** — [Download here](https://dev.mysql.com/downloads/workbench/)
- **Power BI Desktop** — [Download here](https://powerbi.microsoft.com/en-us/desktop/)

### Step 1 — Clone the Repository

```bash
git clone https://github.com/yanshiSharma/Ola-Cab-Analysis.git
cd Ola-Cab-Analysis
```

### Step 2 — Set Up the Database

```sql
-- Open MySQL Workbench and run:

CREATE DATABASE ola;
USE ola;

-- Then run the full script (creates table, loads data, creates all 10 Views):
SOURCE ola-analysis.sql;

-- Note: Update the file path in the LOAD DATA LOCAL INFILE statement
-- to match your local path to Bookings.csv before running
```

> **Tip:** If `LOCAL_INFILE` is disabled, enable it first:
> ```sql
> SET GLOBAL LOCAL_INFILE = ON;
> ```

### Step 3 — Verify SQL Views

```sql
-- Each of the 10 queries is stored as a View. Test any with:
SELECT * FROM Successful_Bookings;
SELECT * FROM Avg_ride_distance_for_each_vehicle_type;
SELECT * FROM top_5_customers_who_booked_the_highest_number_of_rides;
SELECT * FROM max_and_min_driver_ratings_for_Prime_Sedan;
-- ... and so on for all 10 views
```

### Step 4 — Open the Power BI Dashboard

1. Open **`ola dashboard.pbix`** in Power BI Desktop
2. If prompted about data source, go to **Home → Transform Data → Data Source Settings** and update the path to your local `Bookings.csv`
3. Click **Home → Refresh** to reload all visuals

### Step 5 — Explore the Dashboard

- Use the **Date slicer** on every page to filter to any date window within July 2024
- Navigate the **5 pages** via the tabs at the bottom: Overall, Vehicle Type, Revenue, Cancellation, Ratings
- Click any pie or donut segment to **cross-filter** all visuals on the page simultaneously
- Hover over any chart element to see **exact values in tooltips**

---

## 🚀 Future Scope — What's Next

| Enhancement | Description |
|-------------|-------------|
| **🕐 Hour-of-Day Demand Analysis** | Add a `HOUR(Event_Time)` breakdown in SQL and Power BI to identify peak booking windows — enables data-driven driver allocation and surge pricing decisions |
| **📍 Location-Level Cancellation Heatmap** | Join pickup/drop locations (50 unique areas in dataset) with a Bengaluru GeoJSON map to visualize which zones have the highest cancellation and incomplete ride rates |
| **📉 Cancellation Prediction Model** | Train a binary classifier (Python/scikit-learn) on booking features — vehicle type, location, time, V_TAT — to predict cancellation risk at booking time |
| **🔔 Real-Time Ops Alerts** | Publish to Power BI Service and configure data-driven alerts when hourly cancellation rate crosses a defined threshold |
| **🧑‍🤝‍🧑 Customer Segmentation (RFM)** | Apply Recency, Frequency, Monetary analysis to identify loyalty tiers and churn-risk segments — actionable for targeted retention campaigns |
| **💳 Payment Migration Tracking** | Monitor Cash→UPI shift over multiple months to measure the ROI of digital payment promotions — key metric given cash currently dominates at 57% |
| **🚘 Driver Composite Scoring** | Build a driver score combining `Driver_Ratings`, cancellation rate, and `V_TAT` — supports performance-based incentive and deactivation decisions |
| **📆 Multi-Month Trend Analysis** | Extend the dataset beyond July 2024 to surface seasonal demand patterns, booking growth rate, and month-over-month cancellation trend changes |

---

## 💡 Skills Demonstrated

```
✅ MySQL database design — CREATE TABLE with appropriate data types and PRIMARY KEY
✅ Data loading — LOAD DATA LOCAL INFILE from CSV into MySQL
✅ SQL Views — 10 named, reusable analytical views covering the full business question set
✅ Aggregation queries — COUNT, AVG, SUM, MAX, MIN with GROUP BY and ORDER BY
✅ Filtered queries — WHERE on Booking_Status, Vehicle_Type, Payment_Method, Driver reason
✅ Multi-page Power BI dashboard design with consistent Ola brand theming (#ChaloNiklo)
✅ DAX measures — total/successful/cancelled bookings, booking value, per-vehicle aggregations
✅ Power Query ETL — CSV ingestion, null handling, date/type normalization
✅ Booking status funnel analysis (Success → Cancelled by Customer/Driver → Driver Not Found)
✅ Cancellation root-cause analysis at reason level — customer-side and driver-side separately
✅ Vehicle-type matrix — booking value, success value, avg distance, total distance
✅ Revenue breakdown by payment method with top-customer identification table
✅ Dual ratings grid — driver vs. customer ratings across all 7 vehicle categories
✅ Date slicer interactivity enabling self-service time-window exploration
✅ Business insight generation directly tied to operational decision-making
```

---

## 📬 Connect

**Yanshi Sharma** — Data Analyst

[![GitHub](https://img.shields.io/badge/GitHub-yanshiSharma-181717?style=flat-square&logo=github)](https://github.com/yanshiSharma)

---

<div align="center">
<sub>Built with 🚖 SQL + Power BI · Part of Data Analytics Portfolio</sub>
</div>
