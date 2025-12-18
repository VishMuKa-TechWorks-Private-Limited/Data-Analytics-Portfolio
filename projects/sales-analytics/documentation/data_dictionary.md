# Sales Analytics Data Dictionary

## Sales Transactions Table

| Field Name | Data Type | Description | Example |
|------------|-----------|-------------|---------|
| OrderID | String | Unique identifier for each order | ORD001 |
| OrderDate | Date | Date when the order was placed | 2024-01-15 |
| CustomerID | String | Foreign key to Customer table | CUST1001 |
| ProductID | String | Foreign key to Product table | PROD501 |
| Quantity | Integer | Number of units purchased | 2 |
| UnitPrice | Decimal | Price per unit at time of sale | 149.99 |
| Revenue | Decimal | Total sale amount (Quantity × UnitPrice) | 299.98 |
| Cost | Decimal | Total cost of goods sold | 200.00 |
| Profit | Decimal | Revenue minus Cost | 99.98 |
| RegionID | String | Geographic region code (NA, EU, AP) | NA |
| ChannelID | String | Sales channel (Online, Retail) | Online |

## Customers Table

| Field Name | Data Type | Description | Example |
|------------|-----------|-------------|---------|
| CustomerID | String | Unique customer identifier (Primary Key) | CUST1001 |
| CustomerName | String | Full name of the customer | John Smith |
| Email | String | Customer email address | john.smith@email.com |
| RegistrationDate | Date | Date when customer account was created | 2022-06-15 |
| Segment | String | Customer classification (New, Regular, VIP) | VIP |
| Country | String | Customer's country of residence | USA |

## Products Table

| Field Name | Data Type | Description | Example |
|------------|-----------|-------------|---------|
| ProductID | String | Unique product identifier (Primary Key) | PROD501 |
| ProductName | String | Name of the product | Wireless Headphones |
| Category | String | Main product category | Electronics |
| Subcategory | String | Product subcategory | Audio |
| Brand | String | Brand or manufacturer name | TechBrand |
| Cost | Decimal | Standard cost per unit | 100.00 |
| MSRP | Decimal | Manufacturer Suggested Retail Price | 149.99 |

## Region Codes

| Code | Region | Countries Included |
|------|--------|-------------------|
| NA | North America | USA, Canada, Mexico |
| EU | Europe | UK, France, Germany, Spain, etc. |
| AP | Asia Pacific | China, Japan, India, Singapore, UAE, etc. |

## Customer Segments

| Segment | Definition | Criteria |
|---------|------------|----------|
| New | New customers | Registered within last 6 months |
| Regular | Regular customers | Active for 6-24 months, moderate purchase frequency |
| VIP | High-value customers | Active for 24+ months, high purchase frequency/value |

## Calculated Metrics

| Metric | Formula | Description |
|--------|---------|-------------|
| Profit Margin % | (Profit / Revenue) × 100 | Percentage of revenue that is profit |
| Average Order Value | Total Revenue / Number of Orders | Average amount per transaction |
| Customer LTV | Total Revenue per Customer | Lifetime value of a customer |
| YoY Growth % | ((Current Year - Previous Year) / Previous Year) × 100 | Year-over-year growth percentage |

## Data Quality Notes

- All monetary values are in USD
- Dates are in YYYY-MM-DD format
- No null values in primary and foreign keys
- Revenue = Quantity × UnitPrice (validated)
- Profit = Revenue - Cost (validated)
