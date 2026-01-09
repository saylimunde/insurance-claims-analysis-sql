# insurance-claims-analysis-sql
Insurance data analysis using SQL with a strong focus on window functions. This project answers real-world business questions related to insurance claims, customer behavior, and regional risk analysis using MySQL. Demonstrates practical use of ranking, rolling aggregates, and advanced analytical SQL techniques.

### Dataset Description

The dataset contains insurance-related information for multiple patients, including:

Demographics (age, gender, region)

Health indicators (BMI, diabetic status, smoker status)

Family details (number of children)

Insurance claim amounts


### Tools & Technologies

Database: MySQL

Language: SQL

Concepts Used:

Window Functions

Aggregations

Ranking Functions

### Business Questions Solved
 
1️ Top Insurance Claimants

Identified the top 5 patients with the highest insurance claim amounts.

Used ranking logic to ensure accurate results even when values are tied.

2️ Average Claim by Number of Children

Calculated the average insurance claim based on the number of children a patient has.

Helped identify how family size impacts insurance costs.

3️ Highest & Lowest Claim per Region

Found the maximum and minimum claim values for each region.

Useful for regional risk assessment and premium adjustments.

4️ Claim Difference from First Recorded Claim

Computed how each patient’s claim differs from the first claim value in the dataset.

Demonstrates usage of FIRST_VALUE() window function.

5️ Claim Difference from Group Average

Calculated how much a patient’s claim deviates from the average claim of patients with the same number of children.

6️ Highest BMI Patient per Region

Identified patients with the highest BMI in each region.

Also provided overall BMI ranking across all regions.

7️ Claim Difference from Highest BMI Patient

Calculated the difference between a patient’s claim and the claim of the highest BMI patient in their region.

8️ Claim Difference by Smoker Status

Compared each patient’s claim with the maximum claim among patients with the same smoker status within the same region.

9️ Maximum BMI in Next Three Records

Used window frames to find the maximum BMI among the next three patients, ordered by age.

10 Rolling Average of Claims

Calculated a rolling average of the previous two insurance claims.

Demonstrates time-series–style analysis using SQL.

1️1️ First Claim by Gender & Region (Filtered)

Extracted the first insurance claim for male and female patients:

Region-wise

Non-diabetic patients

BMI between 25 and 30

Used CTE + window functions for clean logic.

##### Key SQL Concepts Demonstrated

ROW_NUMBER()

RANK() / DENSE_RANK()

FIRST_VALUE()

AVG(), MAX(), MIN() with OVER()

PARTITION BY

ORDER BY in window functions

Window frames (ROWS BETWEEN)

Common Table Expressions (CTEs)

### Key Learnings

Window functions allow row-level analysis without collapsing data

Proper use of PARTITION BY is critical for correct analytics

SQL can handle complex analytical logic without using subqueries excessively

These patterns are commonly used in insurance, finance, and healthcare analytics

#### How to Run the Project

Import the dataset into MySQL

Run the provided SQL file:

sql_queries.sql

Execute queries one by one to explore insights



CTEs (Common Table Expressions)

Analytical Queries
