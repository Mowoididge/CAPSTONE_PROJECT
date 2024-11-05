# Sales Data Analysis 

## Project Overview
This project provides an in-depth analysis of a sales dataset to uncover key insights and trends such as top-selling products, regional
performance, and monthly sales trends.. The primary objective is to identify high-performing products, analyze seasonal trends, and provide actionable insights for improving sales strategies.
## Data Sources
The primary source of data is https://canvas.instructure.com/files/273182802/download?download_frd=1 which supplied by the Incubator Hub Fascilitators
## Tools Used
- Excel: For data exploration and preparation
- SQL: For data cleaning and advanced querying.
- Power BI: For dynamic visualizations and dashboards.
## Data Cleaning and Preparation
In the initial phase of loading the data, I performed the following actions:
1.  Data Inspection
2.  Handling Missing variables in excel
3.  Data Loading and validation in excel and power BI
4.  Data cleaning and formating
## Exploratory Data Analysis
The initial EDA involved exploring the data to answer some key questions about the data such as;
- what is the overall sales trend by region,month and product
- Which is the Highest  selling products
- Who are the top 5 customers
- What is the monthly sales value
## Data Analysis
```Excel
=UNIQUE(C2:C50001)  =AVERAGEIF(C:C, I2, H:H)
=UNIQUE(D2:D50001)   =SUMIF(D:D,L2,H:H)
```

```SQL
SELECT * FROM [dbo].[CAPSTONE SALES DATA]
.....TOTAL SALES FOR EACH PRODUCT

SELECT product,SUM(SALES_PER_PRODUCT) AS Total_Sales
FROM  [dbo].[CAPSTONE SALES DATA]
GROUP BY Product

....TOTAL NUMBER OF SALES TRANSACTIONS
SELECT Region,COUNT(OrderID) AS Transaction_Count
FROM [dbo].[CAPSTONE SALES DATA]

.....Highest-selling Product....
SELECT Top 1 Product,SUM(SALES_PER_PRODUCT) AS total_Sales
FROM [dbo].[CAPSTONE SALES DATA]
GROUP BY Product
ORDER BY Total_Sales DESC

.....monthly sales totals for the current year....
SELECT FORMAT(OrderDate, 'MMMM') AS month_name,
    SUM(SALES_PER_PRODUCT) AS monthly_sales
FROM [dbo].[CAPSTONE SALES DATA]
WHERE YEAR(OrderDate) = YEAR(GETDATE())
GROUP BY FORMAT(OrderDate, 'MMMM'),MONTH(OrderDate)
ORDER BY MONTH(OrderDate)

....top 5 customer by purchase amount....
SELECT Top 5 Customer_Id,SUM(SALES_PER_PRODUCT) AS Total_Sales
FROM [dbo].[CAPSTONE SALES DATA]
GROUP BY Customer_Id
ORDER BY Total_Sales DESC

......TOTAL SALES PERCENTAGE BY REGION.....
SELECT Region,SUM(SALES_PER_PRODUCT) AS Regional_sales,
    (SUM(SALES_PER_PRODUCT) * 100.0 / (SELECT SUM(SALES_PER_PRODUCT) 
	FROM [dbo].[CAPSTONE SALES DATA])) AS sales_percentage
	FROM [dbo].[CAPSTONE SALES DATA]
GROUP BY Region
ORDER BY sales_percentage DESC

...Products with no No sale within the last quarter...
SELECT OrderID,Product FROM [dbo].[CAPSTONE SALES DATA]
WHERE OrderID NOT IN (
	SELECT DISTINCT OrderID
    FROM [dbo].[CAPSTONE SALES DATA]
     WHERE 
     OrderDate >= DATEADD(quarter, -1, GETDATE())
    )
```
## Data Visualization


