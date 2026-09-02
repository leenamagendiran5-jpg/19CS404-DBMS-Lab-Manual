# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
--From the following tables write a SQL query to find those customers with a grade less than 300. Return cust_name, customer city, grade, Salesman, salesmancity. The result should be ordered by ascending customer_id.

Sample table: customer


 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005

        Sample table: salesman

        
 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12

```sql
-- SELECT c.cust_name, c.city, c.grade, s.name AS Salesman, s.city AS city 
FROM customer c INNER JOIN salesman s ON c.salesman_id = s.salesman_id WHERE 
    c.grade < 300
ORDER BY 
    c.customer_id ASC;
```

**Output:**

<img width="1260" height="766" alt="441132324-fb19768f-4823-45ae-a6c7-140af7e3e903" src="https://github.com/user-attachments/assets/1a04bf32-5787-4316-9762-994ecc627e85" />


**Question 2**
---
--  Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c"), with a left join on the "customer_id" column and a condition filtering for orders with a purchase amount less than 100.

<img width="857" height="347" alt="441133262-08aaf8da-5069-4257-99a1-32c99b6452a2" src="https://github.com/user-attachments/assets/07c937e7-64d8-4b25-b040-8bc3e4f15079" />


```sql
--SELECT c.cust_name
FROM customer c
LEFT JOIN orders o ON c.customer_id = o.customer_id
WHERE o.purch_amt < 100;
```

**Output:**

<img width="823" height="471" alt="441133693-960b52b8-848e-48dd-8629-2d24d3922147" src="https://github.com/user-attachments/assets/b0e8bc72-f9d7-4746-8974-1ddf73af02c6" />


**Question 3**
---
--  From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.

Sample table: customer


 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005


        Sample table: salesman

        
 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12

```sql
-- SELECT 
    c.cust_name, 
    c.city, 
    c.grade, 
    s.name AS Salesman, 
    s.city AS city
FROM 
    customer c
INNER JOIN 
    salesman s ON c.salesman_id = s.salesman_id
ORDER BY 
    c.customer_id ASC;
```

**Output:**

<img width="1267" height="841" alt="441134567-abd4336a-fcd4-4242-a991-cebeb6a14cc4" src="https://github.com/user-attachments/assets/a17e255d-bea0-423b-9238-bc682b077bda" />


**Question 4**
---
--  From the following tables write a SQL query to find the details of an order. Return ord_no, ord_date, purch_amt, Customer Name, grade, Salesman, commission.

Sample table: orders


ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001

Sample table: customer


 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005

Sample table: salesman
        

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12

        
```sql
-- SELECT 
    o.ord_no,
    o.ord_date,
    o.purch_amt,
    c.cust_name AS "Customer Name",
    c.grade,
    s.name AS "Salesman",
    s.commission
FROM 
    orders o
JOIN 
    customer c ON o.customer_id = c.customer_id
JOIN 
    salesman s ON o.salesman_id = s.salesman_id;
```

**Output:**

<img width="1276" height="781" alt="441135433-ee9de951-4d51-4e9a-9876-7c44ac1c83b1" src="https://github.com/user-attachments/assets/a5644d08-37e7-42a5-8a97-9ad8fd855815" />


**Question 5**
---
--Write a SQL statement to join the tables salesman, customer and orders so that the same column of each table appears once and only the relational rows are returned.

Sample table: orders


ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001

Sample table: customer


 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005


Sample table : salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12


```sql
-- SELECT 
    o.ord_no,
    o.purch_amt,
    o.ord_date,
    c.cust_name,
    c.city AS customer_city,
    c.grade,
    s.name AS salesman_name,
    s.city AS salesman_city,
    s.commission
FROM 
    orders o
JOIN 
    customer c ON o.customer_id = c.customer_id
JOIN 
    salesman s ON o.salesman_id = s.salesman_id;
```

**Output:**

<img width="1276" height="780" alt="441136792-c9b9e311-9d4b-415b-af3b-c3dbbc7bc8a2" src="https://github.com/user-attachments/assets/2a63d1ba-008f-4a2b-8422-da5aaf5ecde8" />


**Question 6**
---
--Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and a condition filtering for appointments with an appointment date between '2024-02-01' and '2024-02-28'.


<img width="982" height="427" alt="441137290-788c6324-2a33-4607-9b3c-ce0fbb8c721a" src="https://github.com/user-attachments/assets/da2d4e6c-72af-4385-82cf-b27994769224" />




```sql
--SELECT p.*
FROM patients p
INNER JOIN appointments a ON p.patient_id = a.patient_id
WHERE a.appointment_date BETWEEN '2024-02-01' AND '2024-02-28';
```

**Output:**

<img width="1232" height="410" alt="441137661-7da6d49a-ba82-474b-b638-3ce851014f12" src="https://github.com/user-attachments/assets/b664c7b9-939e-45fd-9e7b-e1a2d61c13b9" />


**Question 7**
---
--  SQL statement to generate a report with customer name, city, order number, order date, order amount, salesperson name, and commission to determine if any of the existing customers have not placed orders or if they have placed orders through their salesman or by themselves.

Sample table: customer


 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        3008 | Julian Green   | London     |   300 |        5002
        3004 | Fabian Johnson | Paris      |   300 |        5006
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        3001 | Brad Guzan     | London     |       |        5005


  Sample table: orders

  
ord_no      purch_amt   ord_date    customer_id  salesman_id
----------  ----------  ----------  -----------  -----------
70001       150.5       2012-10-05  3005         5002
70009       270.65      2012-09-10  3001         5005
70002       65.26       2012-10-05  3002         5001
70004       110.5       2012-08-17  3009         5003
70007       948.5       2012-09-10  3005         5002
70005       2400.6      2012-07-27  3007         5001
70008       5760        2012-09-10  3002         5001
70010       1983.43     2012-10-10  3004         5006
70003       2480.4      2012-10-10  3009         5003
70012       250.45      2012-06-27  3008         5002
70011       75.29       2012-08-17  3003         5007
70013       3045.6      2012-04-25  3002         5001

Sample table: salesman


 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12




```sql
-- SELECT 
    c.cust_name,
    c.city,
    o.ord_no,
    o.ord_date,
    o.purch_amt AS "Order Amount",
    s.name,
    s.commission
FROM 
    customer c
LEFT JOIN 
    orders o ON c.customer_id = o.customer_id
LEFT JOIN 
    salesman s ON o.salesman_id = s.salesman_id;
```

**Output:**

<img width="1206" height="780" alt="441138513-9e4e04ab-ce88-43cc-9a7c-266d2d60ce34" src="https://github.com/user-attachments/assets/0c1e992d-412a-4923-8b67-7574ce32920f" />


**Question 8**
---
--Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for test results with the test name 'Blood Pressure'.

<img width="983" height="417" alt="441138751-1df56d52-08de-4577-a2ae-458a0b07da93" src="https://github.com/user-attachments/assets/3ad4a2e1-4b51-46b6-a950-2b797090039c" />



```sql
-- SELECT p.first_name AS patient_name, t.*
FROM patients p
INNER JOIN test_results t ON p.patient_id = t.patient_id
WHERE t.test_name = 'Blood Pressure';
```

**Output:**

<img width="1201" height="397" alt="441139160-4dfa98cd-445a-4386-a013-0c51d811cf50" src="https://github.com/user-attachments/assets/83853a0e-7fdd-41e9-8137-5ab6a6c8ac4e" />


**Question 9**
---
--Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and conditions filtering for test results with the test names 'Blood Test' or 'Blood Pressure' and results not containing the substring 'Normal'. 

<img width="898" height="417" alt="441139520-ed5d407e-4808-437d-aed5-b4660a014f10" src="https://github.com/user-attachments/assets/bb0f7d5f-a8ef-4503-9eba-e91b4ec92dce" />


```sql
--SELECT p.*
FROM patients p
INNER JOIN test_results t ON p.patient_id = t.patient_id
WHERE t.test_name IN ('Blood Test', 'Blood Pressure')
  AND t.result NOT LIKE '%Normal%';

```

**Output:**

<img width="1212" height="403" alt="441139953-a5fcd77e-73be-472d-99b6-1d400b85acd3" src="https://github.com/user-attachments/assets/d78919c4-0e9e-4a6e-bda2-fb331f42a951" />


**Question 10**
---
-- Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c") and the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the same city as the salesman. 

<img width="833" height="382" alt="441140636-b12959e5-0e18-4564-8b94-cc16a9f0292a" src="https://github.com/user-attachments/assets/8a1522ab-68ec-4f55-a3c9-ce4c72bbc6b4" />


```sql
-- SELECT c.cust_name, s.name
FROM customer c
LEFT JOIN salesman s ON c.salesman_id = s.salesman_id
WHERE c.city = s.city;
```

**Output:**

<img width="856" height="546" alt="441140986-dd9fc321-948d-4608-a115-461dcb2c6456" src="https://github.com/user-attachments/assets/1e6b9ec5-45e8-4813-a4e4-b08d15689842" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
