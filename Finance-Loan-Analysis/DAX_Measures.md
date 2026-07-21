# 🧮 Key DAX Measures

### Total Loan Applications

```DAX
Total Loan Applications =
COUNTA('Fact_Loan'[Loan Id])
```

---

### Total Funded Amount

```DAX
Total Funded Amount =
SUM('Fact_Loan'[Loan Amount])
```

---

### Total Amount Received
 
```DAX
Total Amount Received =
SUM('Fact_Loan'[Total Payment Received])
```

---

### Average Loan Amount

```DAX
Average Loan Amount =
AVERAGE('Fact_Loan'[Loan Amount])
```

---

### Average Interest Rate

```DAX
Average Interest Rate =
AVERAGE('Fact_Loan'[Interest Rate])
```

---

### Average DTI

```DAX
Average DTI =
AVERAGE('Fact_Loan'[DTI])
```

---

### Good Loan Applications

```DAX
Good Loan Applications =
CALCULATE(
    [Total Loan Applications],
    'Fact_Loan'[Loan Status] IN {"Fully Paid","Current"}
)
```

---

### Bad Loan Applications

```DAX
Bad Loan Applications =
CALCULATE(
    [Total Loan Applications],
    'Fact_Loan'[Loan Status] = "Charged Off"
)
```

---

### Good Loan %

```DAX
Good Loan % =
DIVIDE(
    [Good Loan Applications],
    [Total Loan Applications]
)
```

---

### Bad Loan %

```DAX
Bad Loan % =
DIVIDE(
    [Bad Loan Applications],
    [Total Loan Applications]
)
```

---

### Good Loan Funded Amount

```DAX
Good Loan Funded Amount =
CALCULATE(
    [Total Funded Amount],
    'Fact_Loan'[Loan Status] IN {"Fully Paid","Current"}
)
```

---

### Bad Loan Funded Amount

```DAX
Bad Loan Funded Amount =
CALCULATE(
    [Total Funded Amount],
    'Fact_Loan'[Loan Status] = "Charged Off"
)
```

---

### Good Loan Amount Received

```DAX
Good Loan Amount Received =
CALCULATE(
    [Total Amount Received],
    'Fact_Loan'[Loan Status] IN {"Fully Paid","Current"}
)
```

---

### Bad Loan Amount Received

```DAX
Bad Loan Amount Received =
CALCULATE(
    [Total Amount Received],
    'Fact_Loan'[Loan Status] = "Charged Off"
)
```

---

### Non-Performing Loan Ratio (NPL)

```DAX
NPL Ratio =
DIVIDE(
    [Bad Loan Applications],
    [Total Loan Applications]
) * 100
```

---

### Total Value at Risk

```DAX
Total Value at Risk =
CALCULATE(
    [Total Funded Amount],
    'Fact_Loan'[Loan Status] = "Charged Off"
)
```

---

### Average Bad Loan Interest Rate

```DAX
Average Bad Loan Interest Rate =
CALCULATE(
    [Average Interest Rate],
    'Fact_Loan'[Loan Status] = "Charged Off"
)
```

---

### Average Bad Loan DTI

```DAX
Average Bad Loan DTI =
CALCULATE(
    [Average DTI],
    'Fact_Loan'[Loan Status] = "Charged Off"
)
```

---

### Top Funding State

```DAX
Top Funding State =
VAR StateTable =
    TOPN(
        1,
        SUMMARIZE(
            'Fact_Loan',
            'Fact_Loan'[States],
            "Funded", [Total Funded Amount]
        ),
        [Funded],
        DESC
    )
RETURN
MAXX(StateTable, 'Fact_Loan'[States])
```

---

### Top Loan Purpose

```DAX
Top Loan Purpose =
VAR PurposeTable =
    TOPN(
        1,
        SUMMARIZE(
            'Fact_Loan',
            'Fact_Loan'[Purpose],
            "Funded", [Total Funded Amount]
        ),
        [Funded],
        DESC
    )
RETURN
MAXX(PurposeTable, 'Fact_Loan'[Purpose])
```

---

### Largest Credit Grade

```DAX
Largest Credit Grade =
VAR GradeTable =
    TOPN(
        1,
        SUMMARIZE(
            'Fact_Loan',
            'Fact_Loan'[Grade],
            "Funded", [Total Funded Amount]
        ),
        [Funded],
        DESC
    )
RETURN
MAXX(GradeTable, 'Fact_Loan'[Grade])
```
