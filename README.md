# MY-LITA-PROJECT-1

Project 1: Sales Performance Analysis for a Retail Store 

Summary: In this project, you are tasked with analyzing the sales performance of a retail store. 
You will need to explore sales data to uncover key insights such as top-selling products, regional 
performance, and monthly sales trends. The goal is to produce an interactive Power BI 
dashboard that highlights these findings. 
Instructions: 

1. Excel:
   
o Perform an initial exploration of the sales data. Use pivot tables to summarize 
total sales by product, region, and month. 
o Use Excel formulas to calculate metrics such as average sales per product and 
total revenue by region. 
o Create any other interesting report

![excel project 1](https://github.com/user-attachments/assets/a6f3e648-e28e-44e8-bcbc-5e02fdcb021c)   
![excel project 2](https://github.com/user-attachments/assets/0c33d886-2bfc-497a-a7b4-5375b31a4e2f)


---

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
SELECT MONTH(orderdate) AS
Month, SUM(quantity * UnitPrice) AS
monthly_sales
FROM [dbo].['LITA Capstone project$']
WHERE YEAR(orderdate)= 
YEAR(GETDATE())
GROUP BY Month(orderdate);
```

![monthly sales total](https://github.com/user-attachments/assets/94d4e075-30af-40c8-921f-9eff34d355c6)

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

o calculate the percentage of total sales contributed by each region. 

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

o identify products with no sales in the last quarter.

```
SELECT Product
FROM [dbo].['LITA Capstone project$']
WHERE OrderDate <
DATEADD(QUARTER,-1,GETDATE())
GROUP BY Product
HAVING SUM(Quantity)=0;
```

![no sales](https://github.com/user-attachments/assets/2f2a8c27-1b54-4903-a734-f05bb5c6c70d)

Note: There is no product without sales in the last quarter

# 3. Power BI: 

o Create a dashboard that visualizes the insights found in Excel and SQL. The 
dashboard should include a sales overview, top-performing products, and 
regional breakdowns.
