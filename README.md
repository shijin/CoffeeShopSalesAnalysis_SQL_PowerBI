# Coffee Shop Sales Analysis – Snowflake SQL & Power BI
## Project Overview

This project focuses on analyzing sales data for a coffee shop using Snowflake SQL for data processing and Power BI for visualization.
The goal was to extract actionable insights to help the coffee shop improve sales performance, understand customer behavior, and identify key growth opportunities.

The analysis covers sales trends, order volumes, product performance, and store-wise comparisons, enabling data-driven business decisions.

## Objectives

The main objectives of the project were to:
- Calculate monthly sales, orders, and quantity sold with Month-on-Month (MoM) comparisons.
- Identify sales trends across weekdays vs weekends.
- Analyze store location performance to optimize resources.
- Discover top-performing products and high-sales periods.
- Provide interactive dashboards for dynamic exploration.

## KPI Requirements
1. Total Sales Analysis
Total monthly sales.
Month-on-month increase or decrease.
Difference between selected month and previous month.

2. Total Orders Analysis
Total number of orders per month.
Month-on-month trend comparison.
Difference from previous month.

3. Total Quantity Sold Analysis
Monthly quantity sold.
Month-on-month changes.
Comparison with previous month.

## Chart Requirements
Calendar Heat Map – Shows daily sales volume with dynamic tooltips.
Sales by Weekdays & Weekends – Compares performance trends.
Sales by Store Location – Highlights MoM changes for each store.
Daily Sales with Average Line – Identifies high and low performing days.
Sales by Product Category – Analyzes top-performing categories.
Top 10 Products by Sales – Quick view of best-selling products.
Sales by Days & Hours – Heat map to visualize peak sales times.

## Tools & Technologies Used
Database: Snowflake
Data Processing: SQL
Visualization: Power BI
Data Modeling: Star Schema design for efficient reporting

## Project Workflow
Data Import – Loaded raw sales data into Snowflake.
Data Cleaning & Transformation – Removed inconsistencies, null values, and outliers.
Data Modeling – Structured tables for reporting.
KPI Calculation – Used SQL queries for MoM changes, totals, and rankings.
Dashboard Development – Built interactive Power BI dashboard with slicers, tooltips, and heat maps.


## SQL Queries
### Month on Month Percentage Increase in Sales
SELECT  
    MONTH(transaction_date) AS MONTH,  
    ROUND(SUM(transaction_qty*unit_price)) AS TOTAL_SALES,  
    ROUND((SUM(transaction_qty*unit_price) - LAG(SUM(transaction_qty*unit_price),1) OVER (ORDER BY MONTH(transaction_date)))/  
    LAG(SUM(transaction_qty*unit_price), 1) OVER (ORDER BY MONTH(transaction_date))*100,2) AS MOM_INCREASE_PERCENTAGE  
FROM   
    coffeeshopsales  
WHERE   
    MONTH(transaction_date) IN (4, 5) – (April, May)  
GROUP BY  
    MONTH(transaction_date)  
ORDER BY  
    MONTH(transaction_date);  

### Calculating Sales on Weekdays and Weekends
SELECT  
    CASE WHEN DAYOFWEEK(transaction_date) IN (1, 7) THEN 'Weekends'  
    ELSE 'Weekdays'  
    END AS day_type,  
    SUM(unit_price*transaction_qty) AS Total_Sales  
FROM   
    coffeeshopsales  
WHERE   
    MONTH(transaction_date) = 5  
GROUP BY  
    CASE WHEN DAYOFWEEK(transaction_date) IN (1, 7) THEN 'Weekends'  
    ELSE 'Weekdays'  
    END  

## Dashboard Preview
[Link](https://app.powerbi.com/links/kDShy6xa4E?ctid=695626df-d117-4278-b37d-1252e4fd8b07&pbi_source=linkShare)

