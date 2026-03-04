# Playbook: Personal Finance vs Inflation (2024–2025)

## 🎯 Objective

The project analyzes personal expenses recorded between May 2024 and November 2025, comparing them with official inflation data from INDEC, to answer one central question:

**Did my personal spending keep pace with official inflation, or were there categories where the impact was significantly higher or lower than average?**

From this question, the following analysis axes are derived:
- Identify categories where spending grew above the official GBA inflation rate.
- Identify categories where spending remained below or in line with the IPC.
- Detect patterns that support financial protection decisions in future inflationary scenarios.

---

## 🧩 Methodology

### 1. Preparation

**Data sources**
- Personal expenses from 2024 in monthly CSV files inside the `data/2024/` folder.
- Personal expenses from 2025 in monthly CSV files inside the `data/2025/` folder.
- Official IPC data from INDEC, obtained from https://www.indec.gob.ar/ftp/cuadros/economia/serie_ipc_divisiones.csv and storaged inside the [`data/indec/serie_ipc_divisiones.csv`](../data/indec/serie_ipc_divisiones.csv).

**Storage and reproducibility**
- Raw data is maintained in CSV format to ensure traceability.
- Cleaned data is integrated into Google Sheets [`analysis/finance_dashboard.xlsx`](../analysis/finance_dashboard.xlsx) to build pivot tables, charts, and interactive filters.

**Initial decisions**
- April 2024 was excluded as it contained only two days of expenses.
- *Total* was defined as the primary metric for all calculations.
- Redundant columns (*Total Share*, *Share*) were removed to maintain focus on personal spending.

---

### 2. Process

**Anonymization of sensitive data**
Specific values such as merchant names, personal descriptions, and payment methods were replaced with generic terms to preserve privacy without losing the granularity needed for analysis.

To standardize the `Category` column to English, an auxiliary sheet `categories_lookup` was created with the Spanish-English mapping and the following formula was applied:
```
=ARRAYFORMULA(IF(D2:D=""; ""; VLOOKUP(D2:D; categories_lookup!A:B; 2; FALSE)))
```
The same approach was applied to the `Payment Method` column, using the `payment_method_lookup` sheet:
```
=ARRAYFORMULA(IF(E2:E=""; ""; VLOOKUP(E2:E; payment_method_lookup!A:B; 2; FALSE)))
```

**Column and structure review**
To ensure consistency across monthly sheets before integrating them into the `master` sheet, an auxiliary sheet was created to centralize column names from each month using the following formula:
```
=TRANSPOSE(expense_history_may_2024!1:1)
```
This allowed visual comparison of the order and nomenclature of each sheet, making it easier to detect inconsistencies without navigating between them.

**Normalization of the Total column**
Data exported from Notion arrived in text format such as `ARS2,744.50`, including invisible characters (`CHAR(160)`, non-breaking space) that prevented operating with values as numbers. The following formula was applied to clean and convert each value:
```
=ARRAYFORMULA(IF(C2:C=""; ""; VALUE(SUBSTITUTE(TRIM(SUBSTITUTE(SUBSTITUTE(SUBSTITUTE(C2:C; CHAR(160); " "); "ARS"; ""); ","; "")); "."; ","))))
```
The transformation process was as follows: replacement of non-breaking spaces with normal spaces, removal of the "ARS" currency prefix, removal of the thousands comma in English format, removal of residual spaces with TRIM, conversion of the decimal point to comma for Argentine format compatibility, and final conversion of the text to a numeric value with VALUE.

**Format standardization**
Dates were standardized to DD/MM/YYYY format and amounts to a single decimal separator. Categories were aligned with the official IPC divisions to enable subsequent comparison.

**Treatment of missing data**
The following criteria were applied per affected column:
- `Payment Method`: missing values were filled with "Cash"
- `Description`: records without description were deleted
- `Category`: the most appropriate category was assigned based on the context of the expense
- `Total`: records without amount were deleted

**Duplicate detection**
Repeated records were filtered and consolidated where applicable.

**INDEC data integration**

The historical IPC series was downloaded from:
```
https://www.indec.gob.ar/ftp/cuadros/economia/serie_ipc_divisiones.csv
```
The file was imported as the sheet `ipc_indec_raw` within the main analysis file.

The sheet `categories_ipc_mapping` was created with the mapping between personal expense categories and INDEC IPC divisions. The categories Gifts and Donations were excluded from the mapping as they have no equivalent in the IPC basket.

Finally, the sheet `ipc_gba` was created with data filtered for the GBA region and the analysis period, using the following query:
```
=QUERY(ipc_indec_raw!A:H; "SELECT A,B,D,E,F WHERE H='GBA' AND D >= '202405' AND D <= '202511' AND A MATCHES '0[1-9]|1[0-2]'"; 1)
```
The query simultaneously filters by GBA region, by the period May 2024 to November 2025, and by division codes 01 to 12 corresponding to the 12 divisions of the IPC basket. It is worth noting that the period values were stored as text when importing the CSV, which is why the comparison uses quotes instead of numbers. Recognizing and resolving this type of format inconsistency is part of the data cleaning process.
- Spending distribution by category.  
- Monthly spending evolution vs inflation.  
- Categories exceeding spending limits.  
- Projection of next month’s expenses.  

**Master sheet**
A `master` sheet was created to consolidate all monthly records into a single table.
QUERY was discarded because it mishandles date columns in combined arrays. FILTER with `LEN() > 0` was used instead, as it checks for content regardless of data type.

The following formula was applied to clean and convert each value:
```
={FILTER(expense_history_may_2024!A2:E;LEN(expense_history_may_2024!A2:A)>0);FILTER(expense_history_june_2024!A2:E;LEN(expense_history_june_2024!A2:A)>0);FILTER(...))>0)}
```

---

## ✅ Conclusions (to be completed)  
- Key insights about personal spending behavior.  
- Impact of inflation on different categories.  
- Recommendations for financial adjustments.    