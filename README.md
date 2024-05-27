# About

Hello, I'm Celeste. Welcome to my data analytics portfolio!

The purpose of this repository is to showcase my data anlytics skills, share projects, and build upon my skills as I continue in my data analytics graduate certificate at East Tennessee State University.

# Table of Contents

- [Portfolio Projects](portfolio-projects)
- SQL
  - [Bike Shop Database Creation and Data Exploration](bike-shop-database-creation-and-data-exploration)
- Python
  - [Analysis of Student Spending](analysis-of-student-spending)

# Portfolio Projects

This section will describe each data project with links to the accompanying code files.

## Bike Shop Database Creation and Data Exploration

Database design and creation, SQL queries and reports, data analysis of findings, and recommendations. 

### Overview

This project originated as an assignment for one of my graduate courses. 
However, I've expanded its scope by formulating my own business inquiries and developing relevant queries. 
The database itself was crafted during my graduate studies. The objective of this data analysis is to offer insights into the sales performance of the bike shop and its employees. 
Through an in-depth examination of the data housed within this relational database, my aim was to identify patterns, propose recommendations based on data-driven insights, and enhance my comprehension of bike shop sales dynamics.

### Data Source 

The bike shop database consists of nine relational tables, each depicting specific entities and their attributes.

### Tools
- MySQL Workbench
  
### Database Creation and Preparation
1. Conducted an in-depth analysis of 9 provided CSV files to discern their entity relationships.
2. Established key constraints to ensure data integrity.
3. Developed a comprehensive diagram illustrating tables, attributes, primary keys, and foreign keys.
4. Executed the creation of the bikeshop database, creating scripts for all 9 tables.
5. Successfully imported CSV files into the bikeshop database, ensuring seamless data integration.

### Exploratory Data Analysis 
Code: [bikeshop_queries.sql](https://github.com/CelesteRoberts/Data-Projects/blob/main/bikeshop_queries.sql)
- Determined the bicycle model generating the highest revenue.
- Identified states boasting the highest sales revenue.
- Explored the most popular bike model per state.
- Conducted a month-over-month comparison of sales for 2003 and 2004.
- Analyzed employee sales in conjunction with their respective salaries to pinpoint top performers.

### Findings and Recommendations 

1. **Bike Model Analysis:**
   - *Highest overall revenue model:* "Mountain Full" generates the highest overall revenue.
   - *Further investigation:* This prompts an investigation into whether mountain bikes are the most commonly purchased model, or if they have the highest average sale price.
   - *Additional finding:* Full mountain bikes are not only the highest revenue-generating model, but also the most commonly purchased, indicating strong demand for this model.

2. **State Sales Analysis:**
   - *Leading states in sales revenue:*  California, New York, Texas, Florida, and Illinois are the top states by sales revenue, possibly connected to factors like 		population density or average household income levels.

3. **Popular Bike Models by State:**
   - *Most popular bike models:* The analysis by state reveals that mountain, mountain full, race, and road bikes are the top four most popular models.
   - *Regional preferences*: Road bikes appear to be most popular in densely populated regions, possibly influenced by higher numbers of individuals opting for bicycle commuting in urban settings. 

4. **Month-over-month Sales Comparison**
   - *Highest revenue months:* November 2003 and December 2004 have the highest sales revenue.
   - *Lowest sales months:* February experienced the lowest sales volume in both 2003 and 2004, indicating a potential seasonal trend.

5. **Employee Performance Analysis:**
   - *Salary vs. Sales volume:* The employee with the highest salarfy also boasts the highest sales volume.
   - *Salary vs. Sales performance discrepency:* Interestingly, the second-highest salary-earning employee demonstrates the second-lowest sales volume, suggesting a potential disparity between salary and sales performance. 

These insights provide valuable information for strategic decision-making, such as inventory management, marketing strategies, and employee performance evaluations.

## Analysis of Student Spending

### Project Overview
This project was completed as a component of my graduate coursework.
This data analysis project aims to provide insights into the spending habits of college students. By analzying various aspects of spending data, I sought out to identify trends, make data-driven recommendations, and gain a deeper understanding of student's spending habits. 

### Data Source
Student Spending Data: The primary dataset used for this analysis is the "student_spending.xlsx" file containing detailed information about student spending. This data was obtained on Kaggle.com. 

## Tools
- Python
- Jupytor Notebook
- Libraries: NumPy, Pandas, MatPlotLib, Seaborn

### Data Cleaning Steps:
1. Remove duplicates
2. Define numeric and non-numeric features
3. Find percentages of missing values for each feature
4. Handle null values with imputation
5. Find and remove outliers

### Data Analysis and Visualization
- Performed meaningful statistical analysis of data set to gain insights into spending habits of students in relation to their gender, school year, and income level to gain valuable insights. 
- Created a series of bar plots, bar graphs, and pie charts to visualize the data.

Code: [student_spending_analysis.ipynb](https://github.com/CelesteRoberts/Data-Projects/blob/main/student_spending_analysis.ipynb)

### Data Insights and Recommendations
#### Results/ Findings
1. **Equal monthly income distribution:** Despite variations across school years, the analysis indicates a relatively even distribution of monthly income across both genders and different years of schooling. This suggests a consistent earning potential among students regardless of gender or academic progress.
2. **Spending Trends:** Males exhibit significantly higher average spending across all genders, with a notable margin. Conversely, sophomores display the highest spending among all school years.
3. **Income trends:** Freshman year stands out with slightly higher income levels compared to other school years. This could be attributed to freshmen working more during their initial college year, while higher-level students allocate more time to academic pursuits. 
4. **Gender discrepancy in earnings:** Contrary to traditional gender earnings gaps, the analysis suggests that females tend to earn more than males, with non-binary individuals earning the most. 
5. **Major expenditure categories:** Housing is the highest monthly expenditure on average for students, with food costs being the second highest expenditure, and technology and transportation close to being tied for the third largest expenditure.

#### Recommendations
These recommendations are provided based on findings above from the position of school faculty wishing to enhance student's financial resources. 
- These findings highlight opportunities to support students in optimizing their financial well-being and guidance on managing major expenditures effectively.
- Considering the evident trend of males exhibiting notably higher average spending compared to other genders, it's recommended to prioritize financial planning education and support initiatives towards male students.
- Considering that freshmen may engage in more work compared to students in higher school years, explore part-time job openings or internship programs specifically tailored for freshmen.
- Develop strategies to assist students in managing these expenses effectively, such as providing resources for affordable housing options, meal planning tips, and transportation subsidies or alternatives.
