# Playbook: Personal Finance vs Inflation (2024–2025)

## Objective

The project analyzes personal expenses recorded between May 2024 and November 2025, comparing them with official inflation data from INDEC, to answer one central question:

**Did my personal spending keep pace with official inflation, or were there categories where the impact was significantly higher or lower than average?**

From this question, the following analysis axes are derived:
- Identify categories where spending grew above the official GBA inflation rate.
- Identify categories where spending remained below or in line with the IPC.
- Detect patterns that support financial protection decisions in future inflationary scenarios.

---

## Methodology

### 1. Preparation

**Data sources**
- Personal expenses from 2024 and 2025 in monthly CSV files exported from Notion, stored in `data/2024/` and `data/2025/`.
- Official IPC data from INDEC, stored in `data/indec/serie_ipc_divisiones.csv`.

**Storage and reproducibility**
- Raw data is maintained in CSV format to ensure traceability.
- Cleaned data is integrated into Google Sheets `analysis/finance_dashboard.xlsx` to build pivot tables, charts, and KPIs.

**Initial decisions**
- April 2024 was excluded as it contained only two days of expenses.
- `Total` was defined as the primary metric for all calculations.
- Redundant columns (`Total Share`, `Share`) were removed to maintain focus on personal spending.

---

### 2. Process

**Anonymization**
Specific values such as merchant names and personal descriptions were replaced with generic terms to preserve privacy without losing analytical granularity.

**Column standardization**
Categories and payment methods were translated to English using lookup sheets (`categories_lookup`, `payment_method_lookup`) and VLOOKUP formulas applied via ARRAYFORMULA across each monthly sheet.

**Column consistency check**
An auxiliary sheet was created to centralize and compare column names across all 19 monthly sheets using TRANSPOSE, enabling visual detection of inconsistencies without navigating between sheets.

**Normalization of the Total column**
Data exported from Notion arrived as text with invisible characters and currency prefixes (e.g. `ARS2,744.50`). A cleaning formula using SUBSTITUTE, TRIM, and VALUE was applied to convert each value to a usable number.

**Missing data treatment**
- `Payment Method`: filled with "Cash"
- `Description`: records without description were deleted
- `Category`: assigned based on expense context
- `Total`: records without amount were deleted

**INDEC data integration**
The historical IPC series was imported as the sheet `ipc_indec_raw`. A mapping sheet `categories_ipc_mapping` was created to link personal categories to INDEC divisions. The sheet `ipc_gba` was built using a QUERY that filters by GBA region, the analysis period (202405–202511), and division codes 01–12. Period values were stored as text in the original CSV, so comparisons use quoted strings rather than numbers.

**Master sheet**
All 19 monthly sheets were consolidated into a single `master` sheet using FILTER with `LEN() > 0`, which correctly handles date columns unlike QUERY. Two calculated columns were added: `ipc_category` (maps each expense to its INDEC division via VLOOKUP) and `period` (extracts YYYYMM from the date column to enable joins with `ipc_gba`).

---

### 3. Analysis

**Monthly variation — discarded**
A first approach compared month-over-month variation of personal expenses against the official CPI monthly variation. While the IPC showed a stable declining trend between 4% and 2%, personal expenses showed extreme volatility due to irregular large purchases. This made the comparison misleading and was discarded.

**Cumulative growth index**
Both series were reindexed to a common base of 100 in May 2024 to enable meaningful comparison over the full period.

The personal expenses index starts at 100 in May 2024. Each subsequent month is calculated as:
```
(current_month_total / previous_month_total) * previous_index
```

The official IPC index uses the raw INDEC index value (`ipc_index_raw`) reindexed to May 2024 = 100:
```
ipc_index_raw_current_month / ipc_index_raw_may_2024 * 100
```

The same indexing logic was applied at category level, using the monthly expenses pivot table as the source for personal spending and INDEX/MATCH against `ipc_gba` for the official IPC per division.

**Key finding:** By November 2025, personal expenses grew 58% from the May 2024 baseline, while the official CPI grew 63% over the same period. Personal spending remained slightly below the official inflation rate across the full period.

**Category-level analysis**
The final index value for each category in November 2025 was compared against the corresponding IPC division index. Out of 10 categories analyzed, 3 exceeded inflation (Food, Housing, and Restaurants) and 7 remained below it. The difference between each category's personal index and IPC index was calculated to quantify the gap.

---

### 4. Visualization

**KPI Scorecards — Overall performance**
Three scorecards summarize the overall result:
- `My Expenses Growth`: +58.8% (personal index from May 2024 to Nov 2025)
- `Official CPI Growth`: +63.1% (official IPC index same period)
- `Under Inflation By`: 4.3% (difference between the two)

**KPI Scorecards — Category highlights**
Two additional scorecards highlight the most extreme categories:
- `Biggest Overspend Category`: Housing, water, electricity, gas and other fuels
- `Biggest Underspend Category`: Miscellaneous goods and services

**Chart 1 — Personal Expenses vs IPC Inflation Index (Base 100 = May 2024)**
A combo chart showing monthly evolution of both indexes from May 2024 to November 2025, with a reference line at 100. This chart communicates how closely personal spending tracked official inflation over time and highlights months of significant divergence.

**Chart 2 — Personal vs IPC Index by Category (May 2024 – Nov 2025)**
A horizontal bar chart comparing the final index value of personal spending against the official IPC for each of the 10 categories. This chart reveals which categories drove spending above or below inflation and makes Housing's outsized impact immediately visible.

**Chart 3 — Spending vs Inflation Gap by Category (May 2024 – Nov 2025)**
A bar chart showing the difference between the personal index and the IPC index for each category. Positive values indicate spending above inflation, negative values below. This chart directly answers the project's central question at category level.

---

## Conclusions

**1. Overall spending remained below inflation**
Across the full 19-month period, personal expenses grew 58.8% while the official GBA CPI grew 63.1%. This means spending was effectively 4.3 percentage points below official inflation, which is a positive result in a high-inflation context. However, this aggregate result masks significant variation across categories.

**2. Housing was the dominant inflation driver**
Housing, water, electricity, gas and other fuels reached an index of 769 by November 2025, compared to an official IPC of 203 for the same division. This means personal housing costs grew nearly 4 times faster than the official rate for that category. This likely reflects a combination of rent increases, utility tariff adjustments, and the weight of this category in the overall budget. It is the single most important finding of the analysis.

**3. Food spending also exceeded inflation**
Food and non-alcoholic beverages reached a personal index of 226 against an official IPC of 150. Spending in this category grew approximately 50% more than the official rate, suggesting either a shift toward more expensive products, higher consumption volume, or both. In a persistent inflationary environment, food is typically one of the hardest categories to compress.

**4. Discretionary and variable categories were compressed**
Categories such as Clothing (2.59 vs 137.75), Miscellaneous goods and services (23.24 vs 161.88), and Furnishings (60.79 vs 139.61) show personal indexes far below their official IPC counterparts. This suggests that spending in these categories was actively reduced or deferred, likely as an adaptive response to inflationary pressure in essential categories like housing and food.

**5. Limitations of the dataset**
The analysis covers 19 months starting in May 2024. The absence of data prior to this date limits the ability to establish a longer baseline or contextualize the findings within the broader inflationary cycle that Argentina experienced from 2022 onward. Additionally, categories such as Gifts and Donations were excluded from the IPC comparison as they have no equivalent in the official basket, which means total spending and the IPC are not fully comparable at the aggregate level.

**6. Implications for financial planning**
The analysis suggests a pattern of unconscious adaptation: essential spending (housing, food) absorbed inflation or exceeded it, while discretionary spending was compressed. A conscious financial strategy for a high-inflation environment would involve monitoring housing costs closely, given their disproportionate impact, and identifying whether the compression in discretionary categories reflects genuine choice or financial constraint.