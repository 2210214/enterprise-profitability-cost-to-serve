# Enterprise Profitability & Cost-to-Serve Optimization

An end-to-end SQL Server + Power BI analytics project analyzing customer profitability, contribution margin, and Cost-to-Serve efficiency across a synthetic enterprise customer base of ~10,000 customers and 227K completed orders.

## Project Overview

This project moves from raw transactional CSV data through SQL Server staging, data quality validation, reporting-layer analytics, and an interactive Power BI executive dashboard.

It was built as a portfolio-quality demonstration of SQL analytics, data quality auditing, business intelligence, customer profitability analysis, and business insight generation.

The project was also reviewed end-to-end to identify and correct a critical profitability-metric issue in the original implementation.

## Business Problem

Strong revenue does not mean every customer is equally profitable.

Management needs to understand:

- Which customers generate the most profit?
- Which customers consume disproportionate operational costs?
- What are the main Cost-to-Serve drivers?
- Which customers are genuinely loss-making after accounting for product cost?
- How concentrated is profit across the customer base?
- Which customers should be prioritized for retention or cost review?

## Objectives

1. Measure Revenue, Cost-to-Serve, Gross Profit, and true Contribution Profit at the business and customer level.
2. Identify the main Cost-to-Serve drivers.
3. Segment customers by profitability and cost efficiency.
4. Quantify profit concentration through Pareto analysis.
5. Build an executive-ready interactive Power BI dashboard.
6. Produce actionable business insights and recommendations.

## Business Questions Answered

- What is our total revenue, true profit, and Cost-to-Serve ratio?
- Which customer segments and industries are most profitable?
- What drives operational Cost-to-Serve — shipping, storage, service, or returns?
- Which customers are genuinely loss-making once product cost is properly accounted for?
- How concentrated is our profit across the customer base?
- Which customers should be prioritized for retention, and which require cost review?

## Dashboard Preview

[Cost-to-Serve](dashboard/Cost-to-Serve.png)

[dashboard/Customer-Deep-Dive](dashboard/dashboard/Customer-Deep-Dive.png.png)

[Customer-Profitabilit](dashboard/Customer-Profitability.png)

[Customer-Risk&Profit-Concentration](dashboard/Customer-Risk&Profit-Concentration.png)

[Executive Overview ](dashboard/Executive-Overview.png)

## Key Correction From the Project Review

The original implementation's Contribution Profit metric excluded Product Cost (COGS), which produced an unrealistic 99.54% contribution margin.

The profitability logic was reviewed and corrected to account for Product Cost, resulting in a more realistic true contribution margin of approximately 26.4%.

The corrected analysis also identifies 13 genuinely loss-making customers rather than the 1 customer identified by the original metric.

This correction is important because it demonstrates the importance of validating business metrics and reconciling analytical results before using them for decision-making.

## Architecture

```text
CSV Source Data
      ↓
SQL Server Staging
      ↓
Data Quality Audit
      ↓
Validated Core Tables
      ↓
Reporting & Analytical Views
      ↓
Power BI Data Model
      ↓
Executive Dashboard
      ↓
Business Insights & Recommendations
```

## Repository Structure

```text
enterprise-profitability-cost-to-serve/

├── README.md
├── Insights.pdf
│
├── Dataset/
│   ├── Enterprise_CostToServe_Dataset.zip
│   └── Data_Dictionary
│
├── SQL/
│   └── 10 SQL scripts
│
└── PowerBI/
    └── Enterprise_profitability.pbix
```

## SQL Layer

The SQL layer implements a structured analytics workflow using SQL Server.

It includes:

- Database and schema creation
- Staging and data loading
- Data quality auditing
- Validation and reconciliation
- Reporting views
- Customer profitability analysis
- Cost-to-Serve analysis
- Customer segmentation
- Pareto analysis
- Customer risk analysis
- Executive KPI calculations

The SQL scripts are organized in execution order and should be run sequentially.

## Power BI Layer

The Power BI report provides an executive-level view of profitability and Cost-to-Serve performance.

The report contains:

1. Executive Overview
2. Customer Profitability
3. Cost-to-Serve
4. Customer Risk & Profit Concentration
5. Customer Deep Dive
6. Tooltip Page

The dashboard focuses on:

- Revenue and profitability
- Contribution Margin
- Cost-to-Serve
- Cost drivers
- Customer profitability
- Customer risk
- Profit concentration
- Interactive customer-level analysis

The Power BI model is designed around the SQL reporting layer to provide a controlled and consistent analytical foundation.

## Data Sources

The project uses a synthetic enterprise dataset containing 10 CSV source tables:

- Regions
- Warehouses
- Customers
- Products
- Orders
- Order Items
- Shipping Costs
- Storage Costs
- Customer Service
- Returns

The complete dataset and Data Dictionary are included in the `Dataset` folder.

## Data Quality & Validation

The project includes automated data quality and validation checks covering:

- Uniqueness
- Primary and foreign key relationships
- Referential integrity
- Financial validity
- Date validity
- Business-rule validation
- Transactional row-count reconciliation

The final dataset was validated for internal consistency, including zero orphaned foreign-key records.

## Analytical Methodology

The analysis focuses on separating revenue from the operational and product costs required to generate that revenue.

Key analytical concepts include:

- Revenue
- Product Cost / COGS
- Gross Profit
- Contribution Profit
- Contribution Margin
- Cost-to-Serve
- Cost-to-Serve Ratio
- Customer Profitability
- Customer Segmentation
- Pareto Profit Concentration
- Customer Risk

The corrected True Contribution Profit metric is used as the primary profitability measure for the validated business analysis.

## Dashboard Structure

### Executive Overview

Provides a high-level view of:

- Revenue
- Contribution Profit
- Contribution Margin
- Cost-to-Serve
- Customer and order performance

### Customer Profitability

Analyzes customer-level revenue, cost, profit, and profitability differences across customer segments and industries.

### Cost-to-Serve

Breaks down operational costs across:

- Customer Service
- Shipping
- Storage
- Returns

### Customer Risk & Profit Concentration

Highlights:

- Profit concentration
- Customer risk
- High-value customers
- Customers requiring closer attention

### Customer Deep Dive

Provides detailed customer-level analysis to support investigation and decision-making.

## Key Insights

- True Contribution Margin is approximately **26.4%**, rather than the 99.5% implied by the original legacy metric.
- Cost-to-Serve represents approximately **0.46% of revenue**, making it a relatively small but meaningful operational efficiency lever.
- **13 customers** are genuinely loss-making after Product Cost is properly accounted for, and they are concentrated entirely in the SMB segment.
- Customer Service represents approximately **58.7%** of total Cost-to-Serve.
- Shipping represents approximately **29.3%** of total Cost-to-Serve.
- Customer Service and Shipping together account for approximately **88%** of total Cost-to-Serve, making them the primary cost-optimization targets.
- Profit is meaningfully concentrated across the customer base, with roughly half of customers generating approximately 80% of true contribution profit.

Full business analysis and narrative are available in `Insights.pdf`.

## Business Recommendations

1. Investigate the 13 genuinely loss-making customers, all within the SMB segment, for pricing, service-model, or account-management review.
2. Prioritize Customer Service cost efficiency because it is the largest Cost-to-Serve driver.
3. Review shipping method mix and related operational decisions for cost-sensitive customer segments.
4. Protect and grow the highest-value customers responsible for the majority of contribution profit.
5. Continue validating profitability metrics before using them for management or commercial decision-making.

## Technologies

- SQL Server
- T-SQL
- BULK INSERT
- SQL Views
- Data Quality & Validation
- Power BI
- DAX
- Data Modeling
- Interactive Dashboards
- Markdown / PDF Documentation

## Workflow / Reproduction Instructions

1. Extract the CSV dataset from `Dataset/Enterprise_CostToServe_Dataset.zip` to a known local path.
2. Open the SQL scripts in SQL Server Management Studio or execute them using `sqlcmd`.
3. Run the SQL scripts in their numeric order.
4. Update the CSV folder path in the relevant data-loading script before execution.
5. Review the data quality and validation results before proceeding with analytical queries.
6. Open `PowerBI/Enterprise_profitability.pbix` in Power BI Desktop.
7. Connect the report to the corresponding SQL Server environment.
8. Refresh the data model and review the dashboard results.
9. Use `Insights.pdf` for the final business insights and recommendations.

## Assumptions

- The dataset is synthetic but internally consistent and was validated for key data-quality and referential-integrity rules.
- Completed orders are the primary analytical population for revenue and profitability KPIs.
- Cancelled and returned orders are excluded from profitability views where applicable.
- Storage cost is allocated to orders based on units sold within the same warehouse, product, and month. This is an allocation methodology rather than a directly tracked per-order storage cost.

## Future Enhancements

- Re-run customer segmentation, Pareto, and risk analysis using the corrected True Contribution Profit metric and validate whether customer classifications change materially.
- Extend the Power BI dashboard with additional product- and region-level profitability analysis.
- Add additional performance optimization such as indexing and query tuning if the dataset is expanded significantly.
- Introduce a lightweight orchestration layer, such as SQL Server Agent or Azure Data Factory, if the project evolves into a recurring production data pipeline.

## Portfolio Note

This project demonstrates an end-to-end analytical workflow rather than focusing only on dashboard creation.

It combines SQL data preparation and validation, business-rule analysis, profitability modeling, Cost-to-Serve analysis, Power BI visualization, and business recommendations to demonstrate how raw transactional data can be transformed into decision-oriented insights.

## Contact

**Eslam Eid**

📧 Email: [ie1214@fayoum.edu.eg](mailto:ie1214@fayoum.edu.eg)

🔗 LinkedIn: [linkedin.com/in/eslam-eid-80781a202](https://www.linkedin.com/in/eslam-eid-80781a202)
