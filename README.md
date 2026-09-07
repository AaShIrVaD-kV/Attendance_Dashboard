# 📊 Employee Attendance Analytics Dashboard

### Power BI • Power Query • DAX • Excel • Data Transformation

**🎯 Objective:** Transform raw employee attendance data into a professional, interactive MIS dashboard that helps management understand attendance, absenteeism, leave patterns and late arrivals.

---

## 🌟 Project Overview

This project was created as an **MIS Executive-style attendance reporting solution**.

The workflow starts with raw attendance data in Excel, transforms it using **Power Query**, enriches it with employee master information, calculates attendance KPIs using **DAX**, and finally presents the results through an interactive **Power BI dashboard**.

The dashboard is designed to answer practical management questions such as:

- 👥 How many employees are being tracked?
- ✅ How many attendance records are marked Present?
- ❌ How many are Absent?
- 🏖️ How many are on Leave?
- 📈 What is the overall Attendance %?
- ⏰ How many late-arrival instances occurred?
- 🏢 Which departments have better or weaker attendance?
- 📅 How does attendance change day by day?
- 🚨 Which employees may require attention?

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
| --- | --- |
| 🟦 **Microsoft Excel** | Source attendance data |
| 🟨 **Power Query** | Data cleaning, transformation and merging |
| 🟪 **Power BI** | Dashboard development and visualization |
| 🧮 **DAX** | KPI and attendance calculations |
| 📊 **Power BI Visuals** | Charts, cards, slicers and management reporting |

---

# 🔄 Data-to-Dashboard Process

```text
Raw Excel Data
      ↓
Data Cleaning
      ↓
Power Query Transformation
      ↓
Unpivot Attendance Data
      ↓
Check-In / Check-Out Extraction
      ↓
Working Hours Calculation
      ↓
Late Minutes Calculation
      ↓
Attendance Status Classification
      ↓
Employee Master Merge
      ↓
DAX Measures
      ↓
Power BI Dashboard
      ↓
Management Insights
```

---

# 1️⃣ Data Source

The project uses an employee attendance dataset containing daily attendance information.

The original attendance data was structured in a **wide format**, where each employee appeared as a separate column.

Example:

| Date | Person_0 | Person_1 | Person_2 |
| --- | --- | --- | --- |
| 01-Jan-2024 | 08:55-17:20 | 09:10-17:30 | 08:50-17:15 |
| 02-Jan-2024 | 09:05-17:10 | 08:58-17:25 | 09:15-17:20 |

For the MIS dashboard, this structure is not ideal because employee information is stored across columns.

Therefore, the data was transformed into a **long / transactional format**.

---

# 2️⃣ Power Query -- Data Transformation

## Step 1: Filter the Required Period 📅

The attendance dataset was filtered to the required reporting period (**January 2024**).

---

## Step 2: Unpivot Employee Columns 🔄

The employee columns were unpivoted.

### Before
```text
Date | Person_0 | Person_1 | Person_2 | ...
```

### After
```text
Date | Employee_ID | Attendance_Time
```

This is important because Power BI works much better with a normalized/long-format attendance table.

---

## Step 3: Split Check-In and Check-Out ⏱️

The `Attendance_Time` field contained values such as `08:55-17:20`, `09:10-17:30`, etc.

The field was split using the `-` delimiter into `Check_In` and `Check_Out` fields and converted to **Time** data type.

---

# 3️⃣ Working Hours Calculation 🕐

Working hours were calculated using `Check_Out - Check_In`.

Example: `09:00 → 17:30` => Working Hours = 8.5 hours.

---

# 4️⃣ Late Minutes Calculation ⏰

Standard Start Time = **09:00 AM**.

Employees checking in after 09:00 receive a late-minute value (`Check-In - 09:00`).

---

# 5️⃣ Attendance Status Logic 🟢🟡🔴

Distinguishes:
- 🟢 **Present**
- 🔴 **Absent**
- 🟡 **Leave**
- ⚪ **Weekend**
- 🔵 **Holiday**

Weekends and holidays are separated from working-day attendance analysis.

---

# 6️⃣ Employee Master Data 👥

The attendance table was merged with an Employee Master table containing Employee ID, Name, Department, and Designation.

---

# 7️⃣ DAX Measures 🧮

- **Total Employees**: `DISTINCTCOUNT(Table1_1[Employee_ID])`
- **Present Count**: `CALCULATE(COUNTROWS(Table1_1), Table1_1[Attendance_Status] = "Present")`
- **Absent Count**: `CALCULATE(COUNTROWS(Table1_1), Table1_1[Attendance_Status] = "Absent")`
- **Leave Count**: `CALCULATE(COUNTROWS(Table1_1), Table1_1[Attendance_Status] = "Leave")`
- **Attendance %**: `DIVIDE([Present Count], [Present Count] + [Absent Count] + [Leave Count])`
- **Late Marks**: `CALCULATE(COUNTROWS(Table1_1), Table1_1[Late_Minutes] > 0)`

---

# 8️⃣ Dashboard Design 🎨

Clean **purple + white professional MIS theme** with KPI Cards, Charts (Department-wise, Daily Trend, Status Breakdown, Summary, Late Marks, Attention required), and Slicers.

---

# 9️⃣ Employees Requiring Attention 🚨

Highlights employees with lower attendance percentages:
- 🔴 **< 90%**: Requires attention
- 🟠 **90–92%**: Monitor
- 🟢 **> 92%**: Good

---

# 🔟 Understanding the Daily Attendance Chart Trend 📉

Explains mid-month synthetic data fluctuations and Y-axis zoom effects.

---

# 📁 Project Structure

```text
Employee-Attendance-MIS/
│
├── 📊 ATTENDANCE.pbix
├── 📗 attendance_2023_2024.xlsx
└── 📖 README.md
```

---

# 🏆 Key Takeaway

> **Raw Data → Clean Data → Structured Data → Calculations → Dashboard → Actionable Insights**
