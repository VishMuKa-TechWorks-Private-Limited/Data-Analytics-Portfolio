# 📊 Sales Performance Analytics Dashboard

## 🎯 Project Overview

An interactive Power BI dashboard designed to provide comprehensive insights into sales performance, customer behavior, and revenue trends. This project demonstrates end-to-end business intelligence capabilities from data modeling to actionable insights.

**Business Impact:** Enabled data-driven decision-making that contributed to a 15% increase in revenue through improved sales strategies and customer targeting.

![Dashboard Overview](./screenshots/dashboard-overview.png)

---

## 📈 Business Objectives

- Monitor real-time sales performance across multiple dimensions (region, product, time)
- Identify top-performing products and underperforming segments
- Analyze customer purchasing patterns and lifetime value
- Forecast sales trends for strategic planning
- Track KPIs: Revenue, Profit Margin, Customer Acquisition, Sales Growth

---

## 🔍 Key Insights Delivered

### Revenue Analysis
- **Total Revenue:** $12.5M (YTD)
- **Year-over-Year Growth:** 18.3%
- **Average Order Value:** $285
- **Top Product Category:** Electronics (42% of total revenue)

### Regional Performance
- **Best Performing Region:** North America ($5.2M)
- **Fastest Growing Region:** Asia Pacific (+35% YoY)
- **Region with Highest Profit Margin:** Europe (28%)

### Customer Intelligence
- **Customer Segments:** Identified 3 distinct customer segments
- **Customer Retention Rate:** 67%
- **High-Value Customers:** Top 20% customers contribute 65% of revenue
- **Average Customer Lifetime Value:** $1,850

### Product Performance
- **Best-Selling Products:** Top 10 products analyzed
- **Product Return Rate:** 4.2% (industry avg: 8%)
- **Cross-sell Opportunities:** Identified 15 high-potential product combinations

---

## 📊 Dashboard Features

### Page 1: Executive Summary
- High-level KPIs (Revenue, Profit, Orders, Customers)
- Revenue trend over time
- Top 5 products and regions
- Performance against targets

### Page 2: Sales Analysis
- Sales by product category and subcategory
- Regional sales distribution map
- Monthly and quarterly sales trends
- Sales channel performance (Online vs. Retail)

### Page 3: Customer Analytics
- Customer segmentation analysis
- Customer acquisition and retention metrics
- Cohort analysis
- Customer lifetime value distribution

### Page 4: Product Performance
- Product profitability analysis
- Inventory turnover rates
- Product mix analysis
- Seasonality patterns

### Page 5: Forecasting
- 6-month sales forecast using time series analysis
- Confidence intervals
- Scenario planning (best case, worst case, expected)

---

## 🛠️ Technical Implementation

### Data Sources
- **Source System:** SQL Server Database
- **Data Refresh:** Scheduled daily refresh at 6:00 AM
- **Data Volume:** 250,000+ sales transactions
- **Historical Range:** 3 years (2022-2024)

### Data Model
- **Schema:** Star Schema
- **Fact Tables:** Sales Transactions, Returns
- **Dimension Tables:** Products, Customers, Date, Geography, Sales Channels
- **Relationships:** One-to-Many relationships with bi-directional filters where needed

### DAX Measures (Sample)

```dax
// Total Revenue
Total Revenue = SUM(Sales[Revenue])

// Revenue Growth YoY
Revenue Growth YoY = 
DIVIDE(
    [Total Revenue] - CALCULATE([Total Revenue], SAMEPERIODLASTYEAR('Date'[Date])),
    CALCULATE([Total Revenue], SAMEPERIODLASTYEAR('Date'[Date])),
    0
)

// Customer Lifetime Value
Customer LTV = 
AVERAGEX(
    VALUES(Customer[CustomerID]),
    CALCULATE([Total Revenue])
)

// Profit Margin %
Profit Margin % = 
DIVIDE(
    SUM(Sales[Profit]),
    SUM(Sales[Revenue]),
    0
)

// Running Total Revenue
Running Total Revenue = 
CALCULATE(
    [Total Revenue],
    FILTER(
        ALLSELECTED('Date'[Date]),
        'Date'[Date] <= MAX('Date'[Date])
    )
)
```

### Power Query Transformations
- Data type conversions and validation
- Removed duplicates and null values
- Created calculated columns (Age, Tenure, Segment)
- Merged data from multiple sources
- Applied business rules and filters

---

## 📂 Dataset Information

### Sample Data Structure

**Sales Transactions Table**
- `OrderID`: Unique order identifier
- `OrderDate`: Date of transaction
- `CustomerID`: Customer identifier
- `ProductID`: Product identifier
- `Quantity`: Units sold
- `UnitPrice`: Price per unit
- `Revenue`: Total sale amount
- `Cost`: Product cost
- `Profit`: Revenue - Cost
- `RegionID`: Geographic region
- `ChannelID`: Sales channel

**Customers Table**
- `CustomerID`: Unique customer identifier
- `CustomerName`: Full name
- `Email`: Contact email
- `RegistrationDate`: Account creation date
- `Segment`: Customer segment (New, Regular, VIP)
- `Country`: Customer location

**Products Table**
- `ProductID`: Unique product identifier
- `ProductName`: Product name
- `Category`: Main category
- `Subcategory`: Product subcategory
- `Brand`: Manufacturer brand
- `Cost`: Unit cost
- `MSRP`: Manufacturer suggested retail price

### Data Files
- [Sample Dataset](./data/sales_sample_data.csv) - Sample of 1,000 transactions for demonstration
- [Data Dictionary](./documentation/data_dictionary.md) - Complete field definitions

---

## 🎨 Design Principles

- **Clean Layout:** Minimalist design with clear visual hierarchy
- **Color Scheme:** Corporate blue and green palette for professionalism
- **Interactivity:** Cross-filtering across all visuals
- **Performance:** Optimized DAX and data model for fast rendering
- **Mobile-Friendly:** Responsive design for mobile viewing
- **Accessibility:** High contrast colors and clear labels

---

## 📸 Dashboard Screenshots

### Executive Summary
![Executive Summary](./screenshots/executive-summary.png)

### Sales Analysis
![Sales Analysis](./screenshots/sales-analysis.png)

### Customer Analytics
![Customer Analytics](./screenshots/customer-analytics.png)

### Product Performance
![Product Performance](./screenshots/product-performance.png)

---

## 🚀 Implementation Guide

### Prerequisites
- Power BI Desktop (latest version)
- Access to sample data files
- Basic understanding of DAX and Power Query

### Steps to Replicate
1. Download the sample dataset from the `/data` folder
2. Open Power BI Desktop
3. Import the CSV files using "Get Data" > "Text/CSV"
4. Follow the data modeling steps in the [documentation](./documentation/setup_guide.md)
5. Create relationships between tables
6. Implement the DAX measures provided
7. Build visualizations following the dashboard layout

---

## 📚 Learning Resources

Key concepts demonstrated in this project:
- Star schema data modeling
- Time intelligence functions in DAX
- Advanced filtering and context manipulation
- Dynamic measures and calculated columns
- Report design best practices

---

## 🔄 Future Enhancements

- [ ] Integration with real-time data streaming
- [ ] Advanced predictive analytics using Python integration
- [ ] Automated anomaly detection
- [ ] What-if parameter analysis for scenario planning
- [ ] Natural language Q&A integration

---

## 📞 Questions & Feedback

Have questions about this project or want to discuss the implementation? Feel free to reach out!

---

## 📄 Files in This Project

```
sales-analytics/
├── README.md                          # This file
├── data/
│   ├── sales_sample_data.csv         # Sample transactions
│   ├── customers_sample.csv          # Customer data
│   └── products_sample.csv           # Product catalog
├── screenshots/
│   ├── dashboard-overview.png        # Main dashboard view
│   ├── executive-summary.png         # Executive page
│   ├── sales-analysis.png            # Sales details page
│   ├── customer-analytics.png        # Customer page
│   └── product-performance.png       # Product page
└── documentation/
    ├── data_dictionary.md            # Field definitions
    ├── setup_guide.md                # Implementation steps
    └── dax_measures.txt              # All DAX formulas
```

---

**Project Status:** ✅ Completed | **Last Updated:** December 2025
