# SQL-Project-Demographic and income analysis of Employees-for-Soulvibe.tech

![image](https://github.com/user-attachments/assets/baff6728-66b5-4bf8-b4fe-73a74e9ee902)


## Overview
This project demonstrates my SQL problem-solving skills by analyzing an employee income dataset. It involves data import and solving various business problems using SQL queries.


## Project structure 
- **Database Setup**: Creation of the `my_project` database.
- **Importing data**: Importing sample csv file into tables.
- **Business Problems**: Solving 12 specific business problems using SQL queries.
 
## Database Setup
```sql
CREATE DATABASE my_project;
```

## Data Import

## Business Problems Solved

### 1.Find the average income for each Education_Level for those who are employed full-time.
```sql
SELECT Education_level, Avg(Income) AS Avg_emp_Income,Employee_Status
FROM project
WHERE Employee_Status = 'Full-Time"
ORDER BY Education_level;
```
## OUTPUT/RESULT:

<img width="287" alt="Screenshot 2025-05-29 at 10 01 19 AM" src="https://github.com/user-attachments/assets/d9259e00-1352-4f44-a024-c2c82d5d96db" />



### 2. Retrieve the top 5 highest earning individuals and their details.
``` sql
SELECT*
FROM project
ORDER BY Income DESC
LIMIT 5;
```

## OUTPUT/RESULT:

<img width="510" alt="image" src="https://github.com/user-attachments/assets/1b79aa60-0fd0-42f6-949e-b0178f9acfd1" />
<img width="510" alt="image" src="https://github.com/user-attachments/assets/09fe6e18-bb5c-44c6-a966-c37ab8553c5d" />


### 3. Count how many people in each Occupation have more than 2 dependents and own a house.

```SQL
SELECT Occupation, COUNT(*) AS EMP_COUNT, Houseownership_Status as House_type
FROM project
WHERE No of dependents >2
AND Houseownership_Status = 'OWN'
GROUP BY Occupation;
```
##OUTPUT/RESULT:

<img width="227" alt="image" src="https://github.com/user-attachments/assets/f5c8781c-8b76-4b37-a18b-80d540e0edaa" />


### 4. List all individuals living in Urban locations with an income above the average income.

```sql
SELECT Occupation,Income,Location
WHERE Location = 'URBAN'
AND Income > (
        SELECT AVG(Income)
        FROM project
        WHERE Location = 'URBAN'
               )
Order by Income Desc
```

## OUTPUT/RESULT:

<img width="178" alt="image" src="https://github.com/user-attachments/assets/43de86da-0612-44d9-86e5-f5be2edc3d8e" />\

### 5. Identify how many males and females are in each Employment_Status.

```SQL
SELECT Employment_Status,GENDER,COUNT(*) AS "GENDER"
FROM project
GROUP BY Employment_Status,GENDER
ORDER BY Employment_Status,GENDER;
```


## OUTPUT/RESULT:

<img width="247" alt="image" src="https://github.com/user-attachments/assets/03794c00-f09b-4f07-b635-22a94d2d7417" />

### 6. What is the total and average income by Location and Occupation?

```SQL
SELECT Location, Occupation, 
       SUM(Income) AS Total_Income,
       AVG(Income) AS Average_Income
FROM project
GROUP BY Location, Occupation;
```

## OUTPUT/RESULT:

<img width="277" alt="image" src="https://github.com/user-attachments/assets/00edb6e6-bdb7-4923-87c3-75019ee71828" />

### 7. Find the average Household_Size grouped by Type_of_Housing.

```SQL
SELECT Type_of_Housing, AVG(Household_Size) AS Average_Household_Size
FROM project
GROUP BY Type_of_Housing;
```
## OUTPUT/RESULT:

<img width="228" alt="image" src="https://github.com/user-attachments/assets/84482c2c-feaf-41c4-b575-396f17b8d72f" />

### 8. Calculate the minimum, maximum, and average Work_Experience for each Marital_Status.

```SQL
SELECT Marital_Status,
       MIN(Work_Experience) AS Min_Experience,
       MAX(Work_Experience) AS Max_Experience,
       AVG(Work_Experience) AS Avg_Experience
FROM project
GROUP BY Marital_Status;
```
## OUTPUT/RESULT:

<img width="453" alt="image" src="https://github.com/user-attachments/assets/539edd07-edcb-493a-ae29-c83192dd036d" />

### 9. Write a query to rank individuals by Income within each Education_Level.

```SQL
SELECT *, 
       RANK() OVER (
PARTITION BY Education_Level
ORDER BY Income DESC)
AS Income_Rank
FROM project;
```

## OUTPUT/RESULT:

<img width="229" alt="image" src="https://github.com/user-attachments/assets/0a0e2f40-e9fc-4f52-8a92-8c3f2b982342" />, <img width="229" alt="image" src="https://github.com/user-attachments/assets/50043412-8200-4e30-bf29-e2151e8b0ae1" />, <img width="229" alt="image" src="https://github.com/user-attachments/assets/e11608aa-239f-45ca-8cc3-c7c0d326a8e8" />

### 10. Find the top 3 Occupation types with the highest average income.

```sql
SELECT Occupation, AVG(Income) AS Average_Income
FROM project
GROUP BY Occupation
ORDER BY Average_Income DESC
LIMIT 3;
```

## OUTPUT/RESULT:

<img width="194" alt="image" src="https://github.com/user-attachments/assets/0e29a45e-7d6a-48fa-9016-b5377fb7915c" />

### 11. Use a window function to calculate the cumulative income for each Gender.
```sql
SELECT *, 
       SUM(Income) OVER (
                          PARTITION BY Gender
                          ORDER BY Income) AS Cumulative_Income
FROM project;
```

## OUTPUT/RESULT:

<img width="215" alt="image" src="https://github.com/user-attachments/assets/087139ba-d518-4c65-9d74-ea88cf471aaf" />, <img width="212" alt="image" src="https://github.com/user-attachments/assets/26ae1946-27a6-4153-b2e4-e80faf952f7d" />


### 12. List the people whose income is above the median income for the dataset.

```sql
WITH Median_CTE AS (
    SELECT PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY Income) AS Median_Income
    FROM income_data
)
SELECT *
FROM income_data, Median_CTE
WHERE income_data.Income > Median_CTE.Median_Income;
```

## OUTPUT/RESULT:

<img width="859" alt="image" src="https://github.com/user-attachments/assets/5ca39374-ce88-48f1-88da-94aff80f27a8" />


## Conclusion

This project highlights my ability to handle complex SQL queries and provides solutions to real-world business problems in the context of Income dataset. The approach taken here demonstrates a structured problem-solving methodology, data manipulation skills, and the ability to derive actionable insights from data and extracting various meaningful relation ships.


















