# 🏨 Hotel Booking Demand Analysis

## 📌 Project Overview  
This project analyzes hotel booking data to identify **patterns, trends, and key factors influencing booking demand and cancellations**.  
We applied **data cleaning, preprocessing, feature engineering, and exploratory data analysis (EDA)** to prepare the dataset for predictive modeling.  

🎯 **Main Goal:** Provide insights into customer behavior and help hotels **reduce cancellations, improve guest satisfaction, and optimize revenue management**.  

---

## 📂 Dataset Description  
The dataset includes booking records from two hotels: **Resort Hotel** and **City Hotel**.  
Each row represents a booking with details about the booking process, guests, and stay information.  

### Key Columns  
| Column | Description |
|--------|-------------|
| **hotel** | Type of hotel (Resort or City). |
| **is_canceled** | Target column – 1 if the booking was canceled, 0 otherwise. |
| **lead_time** | Number of days between booking and arrival. |
| **arrival_date** | Combined arrival date (year, month, day). |
| **stays_in_weekend_nights** | Nights stayed on weekends. |
| **stays_in_week_nights** | Nights stayed on weekdays. |
| **adults, children, babies** | Number of guests in each category. |
| **meal** | Type of meal plan booked. |
| **country** | Guest’s country of origin. |
| **market_segment** | Booking channel segment. |
| **distribution_channel** | Channel used for booking. |
| **is_repeated_guest** | Whether the guest booked before. |
| **previous_cancellations** | Number of past canceled bookings. |
| **reserved_room_type / assigned_room_type** | Room type reserved vs. assigned. |
| **deposit_type** | Type of deposit made. |
| **days_in_waiting_list** | How many days the booking was on a waiting list. |
| **customer_type** | Type of booking (Transient, Group, etc.). |
| **adr** | Average Daily Rate (revenue ÷ nights). |
| **total_of_special_requests** | Number of special requests. |
| **reservation_status / reservation_status_date** | Final booking status and date. |

---

## 🛠 Preprocessing Steps  

### 1. Handling Missing Values  
- **Children** → Missing values filled with `0`.  
- **Country** → Filled with most frequent country (mode).  
- **Agent & Company** → Filled with `0` meaning “no agent/company.”  

✅ Dataset had no missing values after this step.

---

### 2. Outlier Detection & Treatment  
- Checked **numerical columns**: `adr`, `lead_time`, `stays_in_weekend_nights`, `stays_in_week_nights`, `days_in_waiting_list`, `adults`, `children`, `babies`, `required_car_parking_spaces`.  
- Applied **IQR (Interquartile Range) method** + **business rules**.  
- Key Findings:  
  - **ADR** had extreme values (> 5000). Capped at **1000**.  
  - **Lead Time** capped at **730 days** (2 years).  
  - **Stay duration** capped at **30 nights**.  
  - **Guests (adults/children/babies)** capped to reasonable bounds.  
  - **Parking spaces** capped at 5.  

✅ This reduced noise and improved data quality.

---

### 3. Data Type Correction  
- Converted `children`, `agent`, and `company` → **int**.  
- Converted categorical variables (`hotel`, `meal`, `market_segment`, etc.) → **category**.  
- Converted `reservation_status_date` → **datetime**.  

✅ Correct data types ensured efficiency and accuracy.

---

### 4. Feature Engineering  
We engineered new features to better capture guest behavior and booking patterns:  

- **arrival_month, arrival_day_of_week, arrival_quarter, is_weekend** → Seasonality insights.  
- **total_stay** = weekday + weekend nights.  
- **stay_category** = Short / Medium / Long stay.  
- **total_guests** = adults + children + babies.  
- **has_guests** = Flag if guests > 0.  
- **has_special_requests** = Flag if special requests > 0.  
- **room_changed** = Reserved vs. assigned room difference.  
- **waiting_list_flag** = 1 if waiting list > 0.  
- **adr_per_person** = ADR ÷ total guests.  
- **cancellation_ratio** = Previous cancellations ÷ previous bookings.  
- **total_nights** = Duplicate of total_stay (kept for modeling consistency).  

✅ These features improved interpretability and model readiness.

---

## 📊 Exploratory Data Analysis (EDA)  

### 🔹 Univariate Analysis  
- **Numerical columns** (`lead_time`, `adr`, `total_guests`, etc.) → Histograms + KDE showed skewed distributions (e.g., ADR right-skewed).  
- **Categorical columns** (`hotel`, `meal`, `deposit_type`, etc.) → Countplots revealed imbalances (e.g., most bookings are City Hotels).  

### 🔹 Target Variable (`is_canceled`)  
- **72.5% bookings not canceled**, **27.5% canceled**.  
- Visualized with a **pie chart** → clearly shows imbalance but sufficient data for both classes.  

### 🔹 Bivariate Analysis  
- **Numerical vs. Cancellations**:  
  - Higher **lead_time** strongly correlated with cancellations.  
  - Higher **adr** and **adr_per_person** linked with cancellations.  
  - Longer stays slightly more prone to cancellations.  
  - More **special requests** → less chance of cancellation.  

- **Categorical vs. Cancellations**:  
  - **Resort Hotels** had higher cancellation rates vs. City Hotels.  
  - **No Deposit** bookings → lower cancellations compared to **Non-Refund** deposits.  
  - **Online TA** segment showed highest cancellations.  
  - Guests with **room changes** had slightly more cancellations.  

✅ EDA gave us actionable business insights into how booking features affect cancellations.  

---

## 🚀 Business Value of the Project  
- **Reduce Cancellations** → By targeting high-risk bookings (e.g., high ADR, long lead time, Non-Refund deposits).  
- **Revenue Optimization** → Adjust pricing based on ADR patterns.  
- **Customer Retention** → Encourage repeated guests and meal plan bookings.  
- **Operational Planning** → Better manage waiting lists, room assignments, and group bookings.  

---

## ✅ Summary of Work Done So Far  
1. Cleaned and imputed missing values.  
2. Detected and capped outliers.  
3. Corrected data types.  
4. Engineered new features.  
5. Performed univariate, target, and bivariate analysis with actionable insights.  
