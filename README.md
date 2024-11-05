# MY-LITA-PROJECT-1

## Project 1: Sales Performance Analysis for a Retail Store 

A sales performance analysis in a retail store typically aims to evealuate and understand key sales trends, identify top-performing products and pinpoint areas for improvement. Here's an overview to guide through structuring a sales performance analysis project;

1.   Objective
*   To assess the store's sales performannce to inform better business decisions
*   To identify top-performing products, peak sales periods, and underperforming areas
*   To analyze customer buying patterns, and regional trends on sales.

2.   Data Collection
The main data sources for this analysis is the "Data Sales" file, which are open-source datasets available

3.   Tools Used
*   Excel:   for data cleaning and visualization
*   SQL:     Utilized for data cleaning through queries
*   PowerBI:   Used for both data cleaning and visualization

4.   Data Cleaning and Preparations
In the initial phase of Data Cleaning and Preparations, we perform the following actions;
*   Data loading and inspection
*   Handling missing variables
*   Data Cleaning and Formatting

Summary: In this project, you are tasked with analyzing the sales performance of a retail store. 
You will need to explore sales data to uncover key insights such as top-selling products, regional 
performance, and monthly sales trends. The goal is to produce an interactive Power BI 
dashboard that highlights these findings. 
Instructions: 

1. Excel:
   
o Perform an initial exploration of the sales data. Use pivot tables to summarize 
total sales by product, region, and month. 


![48](https://github.com/user-attachments/assets/4a38cc74-35b7-426b-aa05-40f9888ecc5a)


o Use Excel formulas to calculate metrics such as average sales per product and 
total revenue by region. 

i.   AverageIF

```
=AVERAGEIF($C2:$C9922,$C2,$H2:$H9922)
```

![45](https://github.com/user-attachments/assets/54b05405-eace-40e9-8635-e45719113bf4)

ii.   SumIF

```
=SUMIF($D2:$D9922,$D2,$H1:$H9922)
```

![46](https://github.com/user-attachments/assets/a0736373-ee8f-4167-8535-bc59867b6e5f)



![47](https://github.com/user-attachments/assets/da75efa1-a026-4662-b8cc-7024aa3f2e66)



o Create any other interesting report

##   Excel Chart
![49](https://github.com/user-attachments/assets/9ef69bf9-fa21-4eec-9a8f-99590c233c16)



2. SQL:
   
Hint – You need to load the dataset into your SQL Server environment to write and 
validate your queries.

```
create database MY_LITA_PROJECT_1
select * from [dbo].['LITA Capstone project$']
```

Write queries to extract key insights based on the following questions;

o retrieve the total sales for each product category.

```
SELECT Product, 
SUM(Revenue) AS TotalSales
FROM [dbo].['LITA Capstone project$']
GROUP By Product;
```

![retrieve](https://github.com/user-attachments/assets/16f88ee5-d214-4683-bb04-1d53257f0b32)

o find the number of sales transactions in each region. 

```
SELECT REGION,
COUNT(*) AS NumberofTransactions
FROM [dbo].['LITA Capstone project$']
GROUP BY REGION;
```

![sales transaction](https://github.com/user-attachments/assets/470ea09c-5a08-42c1-aaed-c205a5be7526)


o find the highest-selling product by total sales value. 

```
SELECT Product,
SUM(Quantity * UnitPrice) AS
TotalSalesValue
FROM [dbo].['LITA Capstone project$']
GROUP BY Product
```

![highest selling product](https://github.com/user-attachments/assets/0b6a5a82-de66-4b79-a20b-721e150c700d)

o calculate total revenue per product. 

```
SELECT Product,
SUM(Quantity * UnitPrice) AS
TotalRevenue
FROM [dbo].['LITA Capstone project$']
GROUP BY Product
```
![total revenue](https://github.com/user-attachments/assets/8b626e32-9ca1-429c-9e19-9665cdd89028)

o calculate monthly sales totals for the current year. 

```
SELECT DATENAME(MONTH, OrderDate) AS MonthName, SUM(revenue) AS MonthlySalesTotal
FROM [dbo].['LITA Capstone project$']
WHERE YEAR(OrderDate) = YEAR(GETDATE())
GROUP BY MONTH(OrderDate), DATENAME(MONTH, OrderDate)
ORDER BY MONTH(OrderDate);
```

![30](https://github.com/user-attachments/assets/71f2bd5d-9ada-4003-9a05-fa94b2b6ca0b)


o find the top 5 customers by total purchase amount. 

```
SELECT TOP 5 [Customer Id],
SUM(quantity * UnitPrice) AS
TotalPurchaseAmount
FROM [dbo].['LITA Capstone project$']
GROUP BY [Customer Id]
ORDER BY TotalPurchaseAmount DESC;
```

![top 5](https://github.com/user-attachments/assets/8d1eeb0c-285f-475b-b511-d2270e20a489)

This query provides the top 5 customers based on their total purchase amount, to identify high-value customers. 

o calculate the percentage of total sales contributed by each region. 

To calculate the percentage of total sales contributed by each region, sum up the sales for each region, then divide each region's total sales by the overall sales and multiply by 100 to get the percentage. 

```
WITH TotalSales AS (
SELECT SUM(quantity * UnitPrice) AS 
TotalSalesAmount
FROM [dbo].['LITA Capstone project$']
)
SELECT REGION, SUM(quantity * UnitPrice) AS RegionSales,
(SUM(quantity * UnitPrice) * 100.0)/ts.TotalSalesAmount AS PercentageContribution
FROM [dbo].['LITA Capstone project$']
CROSS JOIN TotalSales ts
GROUP BY Region,
ts.TotalSalesAmount;
```

![percentage](https://github.com/user-attachments/assets/6f9f43ea-f110-4d85-bb81-3399ee076d08)

This query with the total sales amount and percentage contribution for each region, making it easy to see which regions are the biggest contributors to total sales.

o identify products with no sales in the last quarter.

```
SELECT DISTINCT Product
FROM [dbo].['LITA Capstone project$']
WHERE Product NOT IN (
SELECT Product
FROM [dbo].['LITA Capstone project$']
WHERE OrderDate >= DATEADD(QUARTER, -1, GETDATE())
)
```

![31](https://github.com/user-attachments/assets/debb3b83-5225-499b-8dc5-5519c3c402aa)

This approach gives a clear view of products that may require promotional efforts or inventory adjustments due to recent inactivity. 

# 3. Power BI: 

It can connect to various data sources, including databases, cloud services, Excel spreadsheet, SQL etc. Users can clean and transform data using Power Query, making it ready for analysis. 

#Importing of Data from Excel
In Power BI, import mode allows users to load data from various sources into the application's internal memory.

![import data](https://github.com/user-attachments/assets/27a8e577-7b12-4b3d-b10f-c2a0f4c502d7)

o Create a dashboard that visualizes the insights found in Excel and SQL. The 
dashboard should include a sales overview, top-performing products, and 
regional breakdowns.

## Dashboard Design

A.   Sales Overview:            This section provides an overall view of the sales performance over time

B.   Top Performing Products:   This section shows which products are driving the most sales

C.   Regional Breakdown:        This section visualizes sales by Region

D.   Interactivity with Filters and Slicers:   To make the dashboard interactive, add slicers to filter by different dimensions;

i.   Date Slicers:               Allow filtering by date range

ii.   Product Slicer:            Let users filter the visuals by specific product categories or individual products 

E.   Total Number of CustomerID:   It will explain the total number of CustomerID

F.   Total Revenue:   Revenue generated over a specific period 

G.   Average Sales Per Product:   Over Two Million Per Product

H.   Number of Products:   The total number of products

I.   Region:   Using Slicer to highlight the region

J.   Total Revenue by Month:   Using Line Chart to represent the total sales by Month

K.   Total Revenue by Product:   Using donut chart to explain the total sales by product

L.   Total Revenue by Product:   Using Stacked Bar Chart to explain the total sales by product   


![project 1 sales](https://github.com/user-attachments/assets/ad8e3f7d-9ebe-46ec-be81-92d7acfc199a)



![sales 2](https://github.com/user-attachments/assets/4cffa20b-fd57-4dc9-9784-66ffe018e3e6)


## Expected Outcomes

*   Comprehensive insight into sales trends and product performance
*   Identification of sales peaks and seasonal trends
*   Strategies for increasing sales based on customer buying behaviours
*   Actionable recommendations to improve underperformiing areas and optimize product placement

## Recommendations

*   Summarize key findings and insights into a report or presentation
*   Provide actionable recommendations based on data analysis, such as adjusting product stock, rethinking promotions, or targeting specific customer segments
*   Suggest next steps for continous monitoring and further analysis 
