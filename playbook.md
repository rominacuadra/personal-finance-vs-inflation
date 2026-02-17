# Playbook: Personal Finance vs Inflation (2024–2025)

## 🎯 Objectives
Analyze personal expenses during 2024–2025 and compare them with official inflation data from Argentina (published by INDEC, the National Institute of Statistics and Censuses). The goal is to understand:
- Which categories concentrate most expenses.
- How monthly spending evolves.
- Whether expenses follow overall inflation and category-specific Consumer Price Index (CPI).
- If spending limits are respected.
- What adjustments should be made considering projected inflation.

---

## 🧩 Methodology
1. **Data Collection**
   - Personal expenses for 2024 are stored in a CSV file: [`data/expenses_2024.csv`](data/expenses_2024.csv).
     - ![Preview of expenses_2024.csv](docs/images/expenses_2024_preview.png)
   - Personal expenses for 2025 are stored in a CSV file: [`data/expenses_2025.csv`](data/expenses_2025.csv).
     - ![Preview of expenses_2025.csv](docs/images/expenses_2025_preview.png)
   - Official CPI data from Argentina (INDEC) is stored in a CSV file: [`data/cpi_indec.csv`](data/cpi_indec.csv).
     - ![Preview of cpi_indec.csv](docs/images/cpi_indec_preview.png)

2. **Data Cleaning & Preparation**
   - Normalize formats (dates, categories, amounts).
   - Ensure consistency across datasets.
   - Apply privacy-preserving scaling to anonymize values.
   - Raw data is initially stored in CSV format (`expenses_2024.csv`, `expenses_2025.csv`, `cpi_indec.csv`) for reproducibility.
   - Cleaned data is then imported into Excel or Google Sheets (`analysis/finance_dashboard.xlsx`) to build pivot tables, charts, and interactive filters, showcasing advanced dashboarding skills.

3. **Analysis**
   - Descriptive analysis: spending by category, monthly evolution.
   - Comparative analysis: expenses vs CPI inflation.
   - Evaluation of spending limits compliance.
   - Projection: estimate future expenses adjusted for inflation.

4. **Visualization**
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