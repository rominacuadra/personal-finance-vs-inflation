# Playbook: Personal Finance vs Inflation (2024–2025)

## 🎯 Objectives
The project aims to analyze personal expenses during 2024–2025 and compare them with official inflation data from Argentina (INDEC).  
Key questions include:  
- Which categories and subcategories show the highest spending growth?  
- How does personal spending compare to official inflation rates?  
- Are predefined spending limits respected?  
- What adjustments could help mitigate the impact of inflation in the coming months?  

---

## 🧩 Methodology

### 1. Preparation
- **Data sources**:  
  - Personal expenses for 2024 stored in monthly CSV files inside the folder `data/2024/`.  
  - Personal expenses for 2025 stored in monthly CSV files inside the folder `data/2025/`.  
  - Official CPI data from Argentina (INDEC) stored in `data/cpi_indec.csv`.  
- **Storage and reproducibility**:  
  - Raw data is kept in CSV format to ensure traceability.  
  - Cleaned data is imported into Excel/Google Sheets (`analysis/finance_dashboard.xlsx`) to build pivot tables, charts, and interactive filters.  
- **Initial decisions**:  
  - April 2024 was excluded because it only contained two days of expenses.  
  - *Total* was defined as the primary metric for all calculations.  
  - Redundant columns (*Total Share*, *Share*) were removed to keep the focus on personal spending.  

### 2. Process
- **Anonymization of sensitive data**:  
  - Specific values (names, merchants, payment methods) were replaced with generic terms to preserve privacy.  
- **Column review and order**:  
  - A standard column order was established to integrate them into the *master* sheet.  
- **Text and spelling corrections**:  
  - Categories and descriptions were adjusted to avoid typographical inconsistencies.  
- **Handling missing or inconsistent data**:  
  - Irrelevant records were removed.  
  - Incomplete values were filled with estimates or marked as “NA”.  
- **Duplicate detection and removal**:  
  - Repeated records were filtered and consolidated as appropriate.  
- **Format normalization**:  
  - Dates standardized (DD/MM/YYYY).  
  - Amounts homogenized with a single decimal separator.  
  - Categories aligned with official CPI categories to enable comparisons.  

### 3. Analysis
- Descriptive analysis: spending by category, monthly evolution.  
- Comparative analysis: expenses vs CPI inflation.  
- Evaluation of compliance with spending limits.  
- Projection: estimate future expenses adjusted for inflation.  

### 4. Visualization
- Excel dashboard with pivot tables, charts, and slicers.  
- Highlight key categories and trends.  

---

## 📊 Results (to be completed)  
- Spending distribution by category.  
- Monthly spending evolution vs inflation.  
- Categories exceeding spending limits.  
- Projection of next month’s expenses.  

---

## ✅ Conclusions (to be completed)  
- Key insights about personal spending behavior.  
- Impact of inflation on different categories.  
- Recommendations for financial adjustments.  

---

## 🚀 Next Steps  
- Scale analysis to Power BI for interactive dashboards.  
- Extend methodology to other datasets (e.g., household or industry benchmarks).  