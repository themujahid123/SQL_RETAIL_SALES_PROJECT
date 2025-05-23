# SQL_RETAIL_SALES_PROJECT  

# Project Overview 
**Project Title:** Retail Sales Data insights  
**Level:** Beginner  
**Database:** `Retail Sales Data 

This project is developed to demonstrate essential SQL skills typically required for data analysts.it involves setting up a retail sales database,clinning and exploring the data, and answering busines related 
questions using SQL queries The purpose of this project is to help beginners understand real-world applications of SQL in a structure and practical way
**Objectives
# Objectives
**Database Setup:** Create and populate a retail sales database using structure sales data   
**Data Cleaning:** Identify and handle missing or incorrect data entries   
**Exploratory Analysis:** Perform basic SQl-based exploration to understand trends and structure    
**Business Insights:** use SQL to answer key questions that help understand sales performances and customer behavior  

# Project Structure   
**1.Database Creation:**
The project start by creating a database named ` RETAIL_SALES_ANALYSIS`.  
**Table Creation:** A table named `RETAIL_SALES` is created to store the sales data .The table structure includes columns for transaction id,sale date,sale time,customer id,gender,age,product category 
quantity sold ,price per unit,cost of goods sold ,total sales amount  

``` SQL
CREATE DATABASE RETAIL_SALES_ANALYSIS

CREATE TABLE RETAIL_SALES 
(transactions_id INT PRIMARY KEY,
	sale_date DATE,
	sale_time TIME,
	customer_id INT,retail_salestransactions_id
	gender varchar(10),
	age int,
	category varchar(20),
	quantiy int,
	price_per_unit float,
	cogs float,
	total_sale float);
```
### 2.Data Exploring And Cleaning
**Customer Count:** Find out how many unique customers are in the dataset  
**Category Count:** Identify all unique product categories in the dataset  
**Null Values Check:** Check for any Null values in dataset and delete missing records  
```sql
SELECT COUNT(DISTINCT customer_id) from RETAIL_SALES 
SELECT DISTINCT category from RETAIL_SALES 

SELECT * FROM RETAIL_SALES 
WHERE transactions_id IS NULL OR sale_date IS NULL 
     OR sale_time IS NULL customer_id IS NULL OR gender IS NULL OR age IS NULL	
	 OR category IS NULL OR quantiy IS NULL OR price_per_unit IS NULL OR cogs IS NULL 

DELETE FROM RETAIL_SALES 
WHERE transactions_id IS NULL OR sale_date IS NULL 
     OR sale_time IS NULL customer_id IS NULL OR gender IS NULL OR age IS NULL	
     OR category IS NULL OR quantiy IS NULL OR price_per_unit IS NULL OR cogs IS NULL
```
### 3.Data analysis And Finding
1.**WRITE SQL QUERY TO RETRIVE ALL THE COLUMNS  SALES MADE ON '2022-11-5**  
```SQL
SELECT *
FROM RETAIL_SALES
WHERE SALE_DATE = "2022-11-5"
```  

2.**WRITE SQL QUERY TO RETRIVE ALL THE TRANSACTION WHERE THE CATEGORY IS 'CLOTHING' AND QUANTITY SOLD MORE THEN 4 IN MONTHG OFF NOVEMBER 2022**
```SQL
SELECT category,sum(total_sale)
FROM RETAIL_SALES  
WHERE 
     category = 'Clothing' 
	 AND DATE_FORMAT(sale_date, '%Y-%m') = '2022-11'
     AND quantiy >=4
GROUP BY 1
```

3.**WRITE SQL QUERY TO CALCULATE TOTAL SALES FOR EACH CATEGORY**
```SQL
SELECT category,SUM(total_sale),count(quantiy)
FROM RETAIL_SALES 
GROUP BY category
```

4.**WRITE SQL QUERY TO FIND AVERAGE AGE OF CUSTOMER WHO PURCHASE ITEMS FROM 'BEAUTY' CATEGORY**
```SQL
 SELECT ROUND(AVG(age)) AS AVG_AGE 
 FROM RETAIL_SALES 
 WHERE category = 'Beauty'
```

5.**WRITE SQL QUERY TO FIND ALL TRANSACTIONS WHERE THE TOTAL_SALES IS GREATER THE 1000**
```SQL
 SELECT * 
 FROM RETAIL_SALES 
 WHERE TOTAL_SALE = 1000
```

6.**WRITE SQL QUERY TO FIND THE TOTAL NUMBER OF TRANSACTIONS MADE BY EACH GENDER AND EACH CATEGORY**
```SQL
SELECT 
      gender, category,COUNT(transactions_id) as TOTAL_TRANSACTIONS
FROM RETAIL_SALES 
GROUP BY 1,2
```

7.**- WRITE SQL QUERY TO FIND AVERAGE SALE OF MONTH AND FIND OUT THE BEST SELLING MONTH IN EACH YEAR**
```SQL
WITH MONTHLY_RANKED AS (
SELECT 
      YEAR(sale_date) AS SALES_YEAR,MONTH(sale_date) AS SALES_MONTH,ROUND(AVG(total_sale))as TOTAL_SALES,
      RANK()OVER(PARTITION BY YEAR(SALE_DATE) ORDER BY AVG(total_sale) DESC) AS MONTH_RANK
FROM RETAIL_SALES 
GROUP BY 1,2)
SELECT SALES_YEAR,SALES_MONTH,TOTAL_SALES,MONTH_RANK
FROM MONTHLY_RANKED 
WHERE MONTH_RANK = 1
```

8.**SAME QUERY WITH DIFFRENT APPROACH**
```SQL
SELECT * FROM 
(SELECT 
      YEAR(sale_date) AS SALES_YEAR,MONTH(sale_date) AS SALES_MONTH,ROUND(AVG(total_sale))as TOTAL_SALES,
      RANK()OVER(PARTITION BY YEAR(SALE_DATE) ORDER BY AVG(total_sale) DESC) AS MONTH_RANK
FROM RETAIL_SALES 
GROUP BY 1,2) AS T1 
WHERE MONTH_RANK = 1
```

9.**WRITE THE QUERY TO FIND TOP 5 CUSTOMERS BASED ON THERE HIGHEST TOTAL SALES**
```SQL
SELECT customer_id,sum(total_sale) as HIGHEST_SALES 
FROM RETAIL_SALES
GROUP BY 1 
ORDER BY HIGHEST_SALES DESC 
LIMIT 5
```

10.**WRITE SQL QUERY TO FIND UNIQUE CUSTOMERS WHO PURCHASED IN EACH CATEGORY**
```SQL
SELECT category,COUNT(DISTINCT customer_id)
FROM RETAIL_SALES 
GROUP BY 1
```
11.**WRITE SQL QUERY TO CREATE EACH SHIFT AND NUMBER OF ORDERS (EXAMPLE MORNING <12 AND AFTERNON BETWEEN 12 TO 17 AND EVINIG >17)**
```SQL
WITH HOURLY_SALES AS (
SELECT *,
         CASE 
          WHEN HOUR(SALE_TIME) < 12 THEN "MORNING"
		  WHEN HOUR(SALE_TIME) BETWEEN 12 AND 17 THEN "AFTERNON" 
          ELSE "EVINING"
          END AS SHIFT
FROM RETAIL_SALES )
SELECT SHIFT,COUNT(customer_id) as TOTAL_ORDERS
FROM HOURLY_SALES 
GROUP BY SHIFT
```
## Finding 
**Customers Demographics:** The dataset includes customers from various age group,with sales distributed across different  categories such as Clothing and beauty.  
**High-value Transactions:** Several transactins had sales amount greater the 1000 indicate premium purchase.  
**Sales Trends:** monthly ﻿analysis show variation in sales helping identify peak season.  
**Customer Insights:** The analysis finding top spending customers and most popular product categories   

##  Report
**Sales Summary:** A detailed report summarizing total sales, customer demographics, and category performance.  
**Trend Analysis:** Insights into sales trends across the different month and shifts.  
**Customer Insights:** Report on top customer and unique customer counts per categories.  

## Conclusion 
The project serves as a comprehensive introduction to sql for data analyts,covering database setup,data cleaning,exploratory data analysis and business driven sql queries.The finding from this project
can help to drive business decision by understanding sales pattern,customer behaviour,and product performance.  

## Author - MUJAHID PASHA


