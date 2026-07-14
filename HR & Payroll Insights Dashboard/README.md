# 📊 HR & Payroll Insights Dashboard (Power BI)

## 📌 Project Overview
This Power BI dashboard provides a comprehensive analysis of organizational human resources and payroll distribution. The goal is to empower HR managers and financial executives to track payroll allocations, monitor operational costs, understand workforce demographics, and detect anomalies in bonus or commission structures across departments.

---

## 🛠️ Data Architecture & Modeling
The project uses a structured **Star Schema** to ensure optimized performance and clear filter propagation. 

* **Fact Table:** `Fact_Salary_Dataset` — contains monthly financial transaction logs (Basic Salary, HRA, Allowances, Deductions, Net Salary, etc.).
* **Dimension Tables:**  `employee_dataset` — contains unique employee details (Designation, Gender, Date of Joining).
  * `dept_dataset` — contains department metadata (Department Name, Operational Location).
  * `Dim_Date` — a custom DAX calendar table created to support Time Intelligence metrics.

### 📐 Entity-Relationship Diagram (ERD)
The structured database architecture showing relationships and data flow between facts and dimension tables:
![Data Model](Assets/data_model.png)

## 📸 Dashboard Preview
The comprehensive user interface showcasing executive insights and visual performance analysis:
![Dashboard View](Assets/dashboard_preview.png)

---

## 🧼 Data Transformation & Cleaning (Power Query)
End-to-end ETL processing was performed using the **Power Query Engine**:
* **Data Sanitization:** Handled structural data issues such as casing inconsistencies (e.g., `sMiTh` to `Smith`) and text typos in Designations (`MANEGER`, `MANGER` rewritten to `Manager`).
* **Data Type Enforcement:** Parsed and validated text string dates into strict uniform locale dates (`DD-MM-YYYY`).
* **Trim & Clean:** Eliminated trailing spaces from geographical text values (e.g., `BOSTON ` cleaned to `BOSTON`).

---

## 🧪 DAX Formulas & Key Metrics
The report relies heavily on custom DAX measures housed inside a dedicated metric table. Key formulas implemented include:

```dax
// 1. Calculate Total Payroll Expenses
Total Net Salary = SUM('Fact_Salary_Dataset'[NetSalary])

// 2. Calculate Month-over-Month (MoM) Growth in Deductions
Deductions MoM Growth = 
VAR CurrentMonth = [Total Deductions]
VAR PreviousMonth = CALCULATE([Total Deductions], PARALLELPERIOD('Dim_Date'[Date], -1, MONTH))
RETURN
DIVIDE(CurrentMonth - PreviousMonth, PreviousMonth, 0)

// 3. Average Employee Cost per Department
Avg Employee Cost = DIVIDE([Total Net Salary], DISTINCTCOUNT('Fact_Salary_Dataset'[EmployeeID]), 0)
