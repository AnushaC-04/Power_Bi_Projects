#  DAX Measures

This document contains all the DAX measures used in the **Employee Payroll & Workforce Analytics Dashboard**. These measures power KPI cards, charts, maps, and other visualizations used throughout the report.

---

#  Total Payroll

Calculates the total gross payroll paid to all employees.

```DAX
Total Payroll =
SUM('Fact_Salary'[Gross Salary])
```

---

#  Total Employees

Returns the total number of unique employees.

```DAX
Total Employees =
DISTINCTCOUNT('Fact_Salary'[EmployeeID])
```

---

#  Average Salary

Calculates the average gross salary of employees.

```DAX
Avg salary =
AVERAGE('Fact_Salary'[Gross Salary])
```

---

#  Average Bonus

Returns the average bonus received by employees.

```DAX
Avg Bonus =
AVERAGE('Fact_Salary'[Bonus])
```

---

#  Maximum Salary

Returns the highest gross salary in the organization.

```DAX
Max Salary =
MAX('Fact_Salary'[Gross Salary])
```

---

#  Lowest Salary

Returns the minimum gross salary.

```DAX
Lowest Salary =
MIN('Fact_Salary'[Gross Salary])
```

---

#  Total Deductions

Calculates the total deductions across all employees.

```DAX
Total Deductions =
SUM('Fact_Salary'[Deductions])
```

---

#  Company Average Salary

Returns the overall company average salary regardless of filters applied in the report.

```DAX
company_avg =
CALCULATE(
    AVERAGE('Fact_Salary'[Gross Salary]),
    ALL('Fact_Salary')
)
```

---

#  Gross Salary

Calculates the total gross salary.

```DAX
Gross Salary =
SUM('Fact_Salary'[Gross Salary])
```

---

#  Maximum Net Salary

Returns the maximum take-home salary after deductions.

```DAX
net_max_salary =
MAX('Fact_Salary'[NetSalary])
```

---

#  Department Payroll

Calculates total payroll for each department.

```DAX
Department Payroll =
SUM('Fact_Salary'[Gross Salary])
```

---

#  Gender-wise Payroll

Calculates payroll distribution based on gender.

```DAX
Gender Payroll =
SUM('Fact_Salary'[Gross Salary])
```

---

#  Monthly Payroll

Calculates payroll for each month.

```DAX
Monthly Payroll =
CALCULATE(
    SUM('Fact_Salary'[Gross Salary])
)
```

---

#  Employee Count

Returns the total number of employees in the selected context.

```DAX
Employee Count =
DISTINCTCOUNT('Fact_Salary'[EmployeeID])
```

