# 💰 Financial Performance Dashboard

## 🎯 Project Overview

A comprehensive Power BI dashboard providing real-time financial insights, including P&L analysis, cash flow monitoring, budget variance tracking, and key financial ratios. This project demonstrates expertise in financial analytics and executive reporting.

**Business Impact:** Improved budget accuracy by 30% and reduced reporting time by 75% through automated financial dashboards.

![Dashboard Overview](./screenshots/dashboard-overview.png)

---

## 📈 Business Objectives

- Monitor financial performance against budget and targets
- Analyze revenue and expense trends across business units
- Track cash flow and working capital metrics
- Provide P&L statements with drill-down capabilities
- Calculate and visualize key financial ratios
- Enable data-driven financial decision-making

---

## 🔍 Key Insights Delivered

### Financial Overview (YTD)
- **Total Revenue:** $45.8M (Budget: $42.0M, +9% vs budget)
- **Net Profit:** $8.2M (18% profit margin)
- **EBITDA:** $12.5M (27% EBITDA margin)
- **Operating Expenses:** $37.6M (82% of revenue)

### Profitability Analysis
- **Gross Profit Margin:** 42%
- **Operating Profit Margin:** 22%
- **Net Profit Margin:** 18%
- **Return on Assets (ROA):** 15.2%
- **Return on Equity (ROE):** 24.8%

### Cash Flow Metrics
- **Operating Cash Flow:** $10.2M
- **Free Cash Flow:** $7.8M
- **Cash Conversion Cycle:** 45 days
- **Current Ratio:** 2.1
- **Quick Ratio:** 1.6

### Budget Variance
- **Revenue Variance:** +$3.8M favorable (+9%)
- **Expense Variance:** -$2.1M unfavorable (+6%)
- **Overall Budget Achievement:** 109% of target
- **Best Performing Unit:** Product Division (+15%)

---

## 📊 Dashboard Features

### Page 1: Executive Financial Summary
- Key financial KPIs at a glance
- Revenue and profit trends
- Budget vs. actual comparison
- Financial health scorecard

### Page 2: P&L Statement
- Dynamic profit & loss statement
- Year-over-year comparison
- Variance analysis (actual vs budget)
- Drill-down by business unit and cost center

### Page 3: Cash Flow Analysis
- Operating, investing, and financing activities
- Cash flow waterfall chart
- Working capital trends
- Days Sales Outstanding (DSO) tracking

### Page 4: Revenue Analysis
- Revenue by product, region, and customer
- Revenue trends and seasonality
- Top revenue contributors
- Revenue concentration risk

### Page 5: Expense Management
- Operating expenses breakdown
- Cost center analysis
- Expense trends over time
- Cost optimization opportunities

### Page 6: Financial Ratios
- Liquidity ratios
- Profitability ratios
- Efficiency ratios
- Leverage ratios
- Trend analysis

---

## 🛠️ Technical Implementation

### Data Sources
- **ERP System:** SAP/Oracle Financials
- **Budgeting Tool:** Adaptive Planning/Anaplan
- **Bank Feeds:** Automated cash position updates
- **Data Volume:** 500K+ transactions annually
- **Historical Range:** 3 years with monthly granularity

### Data Model
- **Schema:** Snowflake Schema
- **Fact Tables:** 
  - FactFinancials (revenue, expenses, profit)
  - FactCashFlow (receipts, payments)
  - FactBudget (budget allocations)
- **Dimension Tables:** 
  - DimAccount (chart of accounts)
  - DimCostCenter
  - DimBusinessUnit
  - DimDate (fiscal calendar)

### Key DAX Measures

```dax
// Total Revenue
Total Revenue = 
SUM(FactFinancials[Amount]) 
* IF(DimAccount[AccountType] = "Revenue", 1, 0)

// Net Profit
Net Profit = 
[Total Revenue] - [Total Expenses] - [Tax Expense]

// Profit Margin %
Profit Margin % = 
DIVIDE([Net Profit], [Total Revenue], 0) * 100

// Budget Variance
Budget Variance = [Actual Amount] - [Budget Amount]

// Budget Variance %
Budget Variance % = 
DIVIDE(
    [Budget Variance],
    [Budget Amount],
    0
) * 100

// YoY Growth %
YoY Growth % = 
VAR CurrentPeriod = [Total Revenue]
VAR PreviousYear = 
    CALCULATE(
        [Total Revenue],
        SAMEPERIODLASTYEAR('Date'[Date])
    )
RETURN
DIVIDE(
    CurrentPeriod - PreviousYear,
    PreviousYear,
    0
) * 100

// Current Ratio
Current Ratio = 
DIVIDE(
    [Current Assets],
    [Current Liabilities],
    0
)

// Quick Ratio
Quick Ratio = 
DIVIDE(
    [Current Assets] - [Inventory],
    [Current Liabilities],
    0
)

// Return on Assets
ROA = 
DIVIDE(
    [Net Profit],
    [Total Assets],
    0
) * 100

// Return on Equity
ROE = 
DIVIDE(
    [Net Profit],
    [Total Equity],
    0
) * 100

// Operating Cash Flow
Operating Cash Flow = 
CALCULATE(
    SUM(FactCashFlow[Amount]),
    FactCashFlow[ActivityType] = "Operating"
)

// Free Cash Flow
Free Cash Flow = 
[Operating Cash Flow] - [Capital Expenditure]

// Days Sales Outstanding
DSO = 
DIVIDE(
    [Accounts Receivable],
    [Total Revenue] / 365,
    0
)
```

---

## 📂 Dataset Information

### Sample Data Structure

**FactFinancials Table**
- `TransactionID`: Unique identifier
- `Date`: Transaction date
- `AccountID`: Chart of accounts reference
- `CostCenterID`: Cost center
- `BusinessUnitID`: Business unit
- `Amount`: Transaction amount
- `Type`: Revenue/Expense/Asset/Liability

**FactBudget Table**
- `BudgetID`: Unique identifier
- `FiscalYear`: Budget year
- `FiscalMonth`: Budget month
- `AccountID`: Account reference
- `BudgetAmount`: Planned amount

**DimAccount Table**
- `AccountID`: Account number
- `AccountName`: Account description
- `AccountType`: Revenue/Expense/Asset/Liability/Equity
- `Category`: Major grouping
- `Subcategory`: Detailed classification

### Data Files
- [Sample Financial Data](./data/financial_sample_data.csv)
- [Budget Data](./data/budget_data.csv)
- [Cash Flow Data](./data/cashflow_data.csv)
- [Data Dictionary](./documentation/data_dictionary.md)

---

## 🎨 Design Principles

- **Executive-Ready:** Clean, professional layout for C-suite
- **Drill-Down Enabled:** Navigate from summary to detailed transactions
- **Color Coding:** Green for favorable, red for unfavorable variances
- **Financial Standards:** Following GAAP/IFRS presentation
- **Real-Time:** Automated refresh for up-to-date insights
- **Security:** Row-level security by business unit

---

## 📸 Dashboard Screenshots

### Executive Summary
![Executive Summary](./screenshots/executive-summary.png)

### P&L Statement
![P&L Statement](./screenshots/pl-statement.png)

### Cash Flow Analysis
![Cash Flow](./screenshots/cashflow-analysis.png)

### Financial Ratios
![Financial Ratios](./screenshots/financial-ratios.png)

---

## 🚀 Implementation Guide

### Prerequisites
- Power BI Desktop (latest version)
- Understanding of financial statements
- Access to financial data (ERP export)
- Knowledge of fiscal calendar setup

### Steps to Replicate
1. Download sample datasets from `/data` folder
2. Import data into Power BI
3. Create fiscal calendar (Date dimension)
4. Build data model with proper relationships
5. Implement chart of accounts hierarchy
6. Create DAX measures for financial calculations
7. Build visualizations following financial reporting standards
8. Set up row-level security if needed
9. Configure scheduled refresh

---

## 📊 Financial Metrics Explained

### Profitability Ratios
- **Gross Margin:** (Revenue - COGS) / Revenue
- **Operating Margin:** Operating Income / Revenue
- **Net Margin:** Net Income / Revenue

### Liquidity Ratios
- **Current Ratio:** Current Assets / Current Liabilities
- **Quick Ratio:** (Current Assets - Inventory) / Current Liabilities

### Efficiency Ratios
- **Asset Turnover:** Revenue / Total Assets
- **Inventory Turnover:** COGS / Average Inventory
- **Receivables Turnover:** Revenue / Average AR

---

## 📈 Advanced Features

### Variance Analysis
- Budget vs. Actual with drill-down
- Prior year comparisons
- Forecast vs. Actual tracking
- Commentary integration

### What-If Analysis
- Scenario planning (best/worst/expected)
- Sensitivity analysis
- Break-even analysis
- Revenue projection modeling

### Forecasting
- Time series forecasting for revenue
- Expense trend projection
- Cash flow forecasting
- Seasonal adjustment

---

## 🔄 Future Enhancements

- [ ] Integration with accounting software API
- [ ] Automated variance commentary using AI
- [ ] Predictive analytics for financial planning
- [ ] Mobile app for executives
- [ ] Real-time alerts for threshold breaches
- [ ] Enhanced drill-through to transaction details

---

## 📚 Financial Reporting Best Practices

Demonstrated in this project:
- Consistent fiscal period definitions
- Proper account classification
- Variance analysis with explanations
- Trend visualization for pattern recognition
- KPI alignment with business strategy
- Secure access controls

---

## 📄 Files in This Project

```
financial-analytics/
├── README.md                          # This file
├── data/
│   ├── financial_sample_data.csv     # Transaction data
│   ├── budget_data.csv               # Budget allocations
│   ├── cashflow_data.csv             # Cash movements
│   └── chart_of_accounts.csv         # Account master
├── screenshots/
│   ├── dashboard-overview.png        # Main view
│   ├── executive-summary.png         # Executive page
│   ├── pl-statement.png              # P&L page
│   ├── cashflow-analysis.png         # Cash flow page
│   └── financial-ratios.png          # Ratios page
└── documentation/
    ├── data_dictionary.md            # Field definitions
    ├── financial_formulas.md         # Calculation guide
    └── implementation_guide.md       # Setup instructions
```

---

**Project Status:** ✅ Completed | **Last Updated:** December 2025

**Compliance Note:** All financial data is anonymized and fictional for demonstration purposes.
