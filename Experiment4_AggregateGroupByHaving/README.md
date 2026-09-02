# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
-- Write a SQL query to find the average salary of all employees?

```sql
-- 
Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER


SELECT AVG(income) AS Average_Salary
FROM employee;
```

**Output:**


<img width="1217" height="342" alt="438293142-fed8cfc8-41ca-4580-9e56-6997f450eaa5" src="https://github.com/user-attachments/assets/dc917734-0847-4d62-911c-3d1e98bfd368" />


**Question 2**
---
--  Write a SQL query to calculate the total number of working hours of all employees

Sample table: employee1 

<img width="845" height="170" alt="438295927-8670e8dc-537c-4836-b33f-fbfe31675d9d" src="https://github.com/user-attachments/assets/4affdda0-a71e-43f5-9192-afcf69097a54" />


```sql
--SELECT SUM(workhour) AS 'Total working hours'
FROM  employee1;
```


**Output:**

<img width="1212" height="340" alt="438296802-b4340e8f-832f-4fe7-951a-cc2a87aea425" src="https://github.com/user-attachments/assets/62bed92b-d05f-4829-ab3e-c0b964cd784c" />


**Question 3**
---
-- Write a SQL query to determine the number of customers who received at least one grade for their activity.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002


```sql
--SELECT COUNT(customer_id) AS COUNT
FROM customer
WHERE grade IS NOT NULL;
```

**Output:**

<img width="1221" height="342" alt="438298655-85c50c99-0953-4c04-815d-412ab6d079a3" src="https://github.com/user-attachments/assets/a86aee18-6942-4ea9-a7dc-e58321f41bc3" />


**Question 4**
---
-- Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the minimum work hours for each date, and excludes dates where the minimum work hour is not less than 10. Sample table: employee1

```sql
-- SELECT jdate,MIN(workhour) AS  'MIN(workhour)'
FROM employee1
GROUP BY jdate
HAVING MIN(workhour) < 10;
```

**Output:**

<img width="1231" height="467" alt="438300915-03b60ef7-4969-4337-abf5-34b06025e263" src="https://github.com/user-attachments/assets/daa449de-1f6d-4b52-921b-5fd3c342e0e6" />


**Question 5**
---
--  Write the SQL query that accomplishes the grouping of data by age, calculates the maximum income for each age group, and includes only those age groups where the maximum income is greater than 2,000,000.

Sample table: employee

<img width="757" height="160" alt="438301598-15eaa93f-2263-40b6-bd81-7488b1f2a65c" src="https://github.com/user-attachments/assets/afc5405c-8d3a-4e05-8337-b85d674e55bb" />


```sql
-- SELECT age, MAX(income) AS 'MAX(income)'
FROM employee
GROUP BY age
HAVING MAX(income) > 2000000;
```

**Output:**

<img width="1217" height="396" alt="438302919-f37a3da9-6e90-419f-befc-d0eeeb1fa312" src="https://github.com/user-attachments/assets/242caef5-7497-4c37-bf51-5cb2bc19a236" />


**Question 6**
---
--  Write the SQL query that accomplishes the selection of number of products for each category from products table which includes only those products where the category ID is greater than 2.

Sample table: products


<img width="747" height="167" alt="438303525-042e49b9-6623-459e-b953-57088965246d" src="https://github.com/user-attachments/assets/d6cac8a7-96ad-4516-9766-891b2712ac38" />

```sql
-- SELECT category_id, COUNT(*) AS COUNT
FROM products
WHERE category_id > 2
GROUP BY category_id;
```

**Output:**

<img width="1215" height="373" alt="438304083-8c58d744-9066-432c-9f73-1eda446f66df" src="https://github.com/user-attachments/assets/9a9cca0f-273b-4a51-ba79-0706098e83aa" />


**Question 7**
---
--Write a SQL Query to find how many medications are prescribed for each patient?

Sample table:MedicalRecords Table
<img width="960" height="133" alt="438304793-271b0f32-9d6b-4026-a0bc-79ff2b2a9b72" src="https://github.com/user-attachments/assets/f97943e4-20ca-4861-93c5-ee41fafb6f0d" />


```sql
-- SELECT PatientID,COUNT(medications) AS AvgMedications
FROM MedicalRecords
GROUP BY PatientID;
```

**Output:**

<img width="1217" height="647" alt="438305623-a2a7478f-ab2e-4af6-be6d-959084185afb" src="https://github.com/user-attachments/assets/aa824488-94e4-494e-bd93-c73298832dbe" />


**Question 8**
---
--  How many prescriptions were written in each frequency category (e.g., once daily, twice daily)? Sample tablePrescriptions Table

<img width="932" height="136" alt="438306526-63e13b53-4879-4a1e-ad4c-4057ba1ef7c1" src="https://github.com/user-attachments/assets/5327dfc8-c0e7-46f7-ab4c-bbbc12195953" />


```sql
-- SELECT Frequency,COUNT(Frequency) AS  TotalPrescriptions
FROM Prescriptions 
GROUP BY Frequency;
```

**Output:**

<img width="1218" height="558" alt="438307049-f01920a5-ee06-4a9c-8864-aa5d6f8700ad" src="https://github.com/user-attachments/assets/e5760009-0b0b-4f85-9e18-00a44b10ea70" />


**Question 9**
---
-- What is the total number of appointments scheduled by each doctor?

Sample table:Appointments Table

<img width="951" height="155" alt="438307681-e1c0ca74-ec1a-4d65-8081-36ae3dc39099" src="https://github.com/user-attachments/assets/3b8d5772-2b6c-4751-b1b0-c4c8fa4bb971" />


```sql
--SELECT DoctorID,COUNT(*) AS TotalAppointments
FROM Appointments 
GROUP BY DoctorID;
```

**Output:**

<img width="1218" height="657" alt="438308182-e24bca3c-0a16-4ca7-9e86-674bb675844a" src="https://github.com/user-attachments/assets/b86783fb-d1d2-4cf5-bc3f-4ff6fffe2a76" />


**Question 10**
---
-- Write a SQL query to return the total number of rows in the 'customer' table where the city is Noida. Sample table: customer 

<img width="822" height="163" alt="438309379-dbb27646-4b8d-4c18-8827-5659cfae35fe" src="https://github.com/user-attachments/assets/7273e93d-57ad-4bff-a77a-36a64902c583" />


```sql
-- select count(city)as COUNT
from customer
where city='Noida';
```

**Output:**

<img width="1228" height="345" alt="438309858-04e98da2-e773-4544-8c2b-6bdca5090687" src="https://github.com/user-attachments/assets/d2521555-32ae-4a40-991d-68ce8a3aee38" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
