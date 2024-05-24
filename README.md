# Bike Shop Analysis

Database creation, SQL queries and reports, data analysis of findings and recommendations. 

## Table of Contents

- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Tools](#tools)
- [Database Creation and Preparation](#database-creation-and-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Findings and Recommendations](#findings-and-recommendations)

## Project Overview
This project originated as an assignment for one of my graduate courses. 
However, I've expanded its scope by formulating my own business inquiries and developing relevant queries. 
The database itself was crafted during my graduate studies. The objective of this data analysis is to offer insights into the sales performance of the bike shop and its employees. 
Through an in-depth examination of the data housed within this relational database, my aim was to identify patterns, propose recommendations based on data-driven insights, and enhance my comprehension of bike shop sales dynamics.

## Data Source 

The bike shop database comprises nine relational tables. The ER-Diagram displayed below illustrates these tables and their attributes. 
In addition to constructing this diagram, I identified the primary and foreign key relationships by thoroughly analyzing these tables and their relationships.

![Screenshot 2024-05-24 160530](https://github.com/CelesteRoberts/Bike-Shop-Analysis-in-SQL/assets/153464094/373a8920-b3aa-4642-9060-be12b77a20e0)

## Tools
- MySQL Workbench
- Excel
- Draw.io (to create the ER diagram)

## Database Creation and Preparation
1. Analyze 9 CSV files provided and determine their entity relationships.
2. Identify key constraints.
3. Create diagram of tables and their attributes, including their primary key and foreign keys.
4. Create bikeshop database and write create scripts for all 9 tables.
5. Import csv files into the bikeshop database.

## Exploratory Data Analysis 
- Identify the highest revenue generating bicycle model.
- Identify states with the highest sales revenue.
- Determine the most popular bike model per state?
- Find a month over month comparison for 2003 and 2004 sales.
- Analyze employee's sales with their respective salary. Who has the highest sales?

## Data Analysis 

This query displays all model types with total sales in order from highest to lowest total sales. 
The highest revenue generating bicycle model type is "Mountain Full"
  ```SQL
-- Find the highest revenue generating bicycle model type 
SELECT 
modeltype,
ROUND(SUM(saleprice), 2) AS Sales  # Sums sale price, rounds to 2 decimals
FROM bicycle 
GROUP BY modeltype 
ORDER BY Sales DESC; # Filtered results by total sales from highest to lowest
```
Result of query:

![Screenshot 2024-05-17 112618](https://github.com/CelesteRoberts/Bike-Shop-Analysis-in-SQL/assets/153464094/623d0e6d-f364-4720-9dda-f22ae1f6950e)

This query displays the top 5 states with the highest sales revenue.
```SQL
SELECT 
salestate as State,
ROUND(SUM(saleprice), 2) as Sales # sums sale price and rounds to 2 decimal placeds
FROM bicycle 
GROUP BY salestate
ORDER BY sales DESC #order by sum of total sales highest to lowest
LIMIT 5 # displaying top 5 only;
```
Result of Query:

![top5states](https://github.com/CelesteRoberts/Bike-Shop-Analysis-in-SQL/assets/153464094/a4dfa6fd-97c3-45b7-8b69-b357a842b393)

This query displays the most popular bike model per state with the total quantity of each.
```SQL
#Subquery to find the maximum quantity for each state
#create a CTE called ModelCounts, which calculates the counts of each bike model per state.
WITH ModelCounts AS ( 
    SELECT 
        salestate AS State,
        modeltype AS bikemodel,
        COUNT(*) AS Qty
    FROM bicycle
    GROUP BY State, bikemodel WITH ROLLUP
)
# Query to retrieve the most popular bike model per state from the CTE
SELECT
    mc.State, #Select state from CTE
    mc.bikemodel, #Select bikemodel from CTE
    mc.Qty #Select qty(count) from CTE
FROM  ModelCounts mc -- CTE
JOIN (
#subquery to find the max count for each state
    SELECT
        State,
        MAX(Qty) AS MaxQty #find max qty for each state
    FROM ModelCounts #from cte
    WHERE bikemodel IS NOT NULL -- Exclude the subtotal rows
    GROUP BY State
) MaxCounts ON mc.State = MaxCounts.State AND mc.Qty = MaxCounts.MaxQty #joining to CTE
WHERE mc.bikemodel IS NOT NULL -- Exclude the subtotal rows
ORDER BY mc.State ASC,  mc.Qty DESC;
```
For this result, I exported the data into an Excel file and created an infographic:

![Screenshot 2024-05-24 163508](https://github.com/CelesteRoberts/Bike-Shop-Analysis-in-SQL/assets/153464094/d2b4053f-98da-4855-9967-ccb951d91751)

This query reveals a month over month comparison for 2003 and 2004 sales. 

```SQL
#CTE to find sum of total sales by date (year and month)
WITH SalesbyDate AS ( #create CTE titled SalesbyDate
	SELECT 	year(orderdate) as order_year,
			month(orderdate) as order_month,
			sum(saleprice) as sales 
	FROM bicycle 
	GROUP BY year(orderdate), month(orderdate)
) 
#query to find sum of sales aggregated by year and month from the CTE. 
SELECT order_month,
	SUM(CASE WHEN order_year=2003 THEN sales ELSE 0 END) as sales_2003,
    SUM(CASE WHEN order_year=2004 THEN sales ELSE 0 END) as sales_2004
FROM SalesbyDate #CTE
GROUP BY order_month
ORDER BY order_month;
```
Result:

![salesbyyearandmonth](https://github.com/CelesteRoberts/Bike-Shop-Analysis-in-SQL/assets/153464094/f80449a9-7e67-48bf-98e3-47662d303fbc)

The following query provides an employee performance report that includes the employees total sales with a rank from 1 as highest sales, 
then provides the employees respective salary.

```SQL
Select
	CONCAT(e.lastname,", ", e.firstname) as Employee_Name,
    ROUND(SUM(b.saleprice),2) as Sales,
    DENSE_RANK() OVER (ORDER BY SUM(b.saleprice) DESC) as salesrank,
    e.Salary 
FROM employee e
INNER JOIN bicycle b ON b.employeeid = e.employeeid 
GROUP BY employee_name, e.salary
ORDER BY salary DESC
;
```
Result:

![Screenshot 2024-05-24 153642](https://github.com/CelesteRoberts/Bike-Shop-Analysis-in-SQL/assets/153464094/af4e2322-4c63-41e1-8220-0b0c23c45163)

## Findings and Recommendations 

1. **Bike Model Analysis:**
   - *Highest overall revenue model:* "Mountain Full" generates the highest overall revenue.
   - *Further investigation:* This prompts an investigation into whether mountain bikes are the most commonly purchased model, or if they have the highest average sale price.
   - *Additional finding:* Full mountain bikes are not only the highest revenue-generating model, but also the most commonly purchased, indicating strong demand for this model.

2. **State Sales Analysis:**
   - *Leading states in sales revenue:*  California, New York, Texas, Florida, and Illinois are the top states by sales revenue, possibly connected to factors like 		population density or average household income levels.

3. **Popular Bike Models by State:**
   - *Most popular bike models:* The analysis by state reveals that mountain, mountain full, race, and road bikes are the top four most popular models.
   - *Regional preferences*: Road bikes appear to be most popular in densely populated regions, possibly influenced by higher numbers of individuals opting for bicycle commuting in urban settings. 

4. **Most-over-month Sales Comparison:
   - *Highest revenue months:* November 2003 and December 2004 have the highest sales revenue.
   - *Lowest sales months:* February experienced the lowest sales volume in both 2003 and 2004, indicating a potential seasonal trend.

5. **Employee Performance Analysis:
   - *Salary vs. Sales volume:* The employee with the highest salarfy also boasts the highest sales volume.
   - *Salary vs. Sales performanc discrepency:* Interestingly, the second-highest salary-earning employee demonstrates the second-lowest sales volume, suggesting a potential disparity between salary and sales performance. 


These insights provide valuable information for strategic decision-making, such as inventory management, marketing strategies, and employee performance evaluations.
