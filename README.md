# Personal Finance vs Inflation (Argentina 2024–2025)

## 🎯 Objective
Analysis of personal expenses between May 2024 and November 2025, compared against official IPC data from INDEC (Argentina's National Institute of Statistics and Censuses).

**Core question: Did my personal spending keep pace with official inflation, or were there categories where the impact was significantly higher or lower?**

## 📂 Repository Structure
```
data/
  2024/        # Monthly expense CSVs (anonymized)
  2025/        # Monthly expense CSVs (anonymized)
  indec/       # Official CPI data from INDEC
analysis/
  finance_dashboard.xlsx   # Main analysis file (Google Sheets)
docs/
  playbook.md        # Full methodology and technical decisions
  STYLE_GUIDE.md     # Design and naming conventions
```

## 🧩 Methodology
1. Data cleaning and normalization of personal expense records exported from Notion
2. Category mapping between personal expenses and official INDEC IPC divisions
3. Monthly comparison of spending growth vs official inflation by category
4. Identification of categories above and below the IPC average

## 🛠️ Tools
Google Sheets · INDEC public data

## 📄 Documentation
Full methodology, formulas, and decisions are documented in [`playbook.md`](docs/playbook.md).
Design and naming conventions are documented in [`STYLE_GUIDE.md`](docs/STYLE_GUIDE.md).
```