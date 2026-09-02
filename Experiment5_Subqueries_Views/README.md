# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
--  Write a SQL query to List departments with names longer than the average length Departments Table (attributes: department_id, department_name)

<img width="1147" height="180" alt="441121112-601b7491-6659-406c-b3ef-09a48970ea30" src="https://github.com/user-attachments/assets/e7892e6a-3323-4ebb-bf85-604273ae0850" />


```sql
-- SELECT department_id, department_name
FROM Departments
WHERE LENGTH(department_name) > (
    SELECT AVG(LENGTH(department_name)) FROM Departments
);
```

**Output:**

<img width="712" height="412" alt="441121438-b4b34710-2470-484a-864c-20f49ada5ac0" src="https://github.com/user-attachments/assets/f6f55c10-48d8-471d-a0f0-f1a4775ec98e" />


**Question 2**
---
-- Write a SQL query to Retrieve the medications with dosages equal to the lowest dosage Table Name: Medications (attributes: medication_id, medication_name, dosage)

<img width="905" height="226" alt="441122047-b3ce9e5e-6c7e-4df8-b7bb-ff451f1b5528" src="https://github.com/user-attachments/assets/238e5aca-3a4e-4ac5-ac7b-41032163dd19" />


```sql
-- SELECT medication_id, medication_name, dosage
FROM Medications
WHERE dosage = (
    SELECT MIN(dosage)
    FROM Medications
);
```

**Output:**

<img width="955" height="387" alt="441122458-48b57122-79e7-4546-a7a3-a47045cc3faa" src="https://github.com/user-attachments/assets/5ea03d00-553b-4925-8646-28af1df2ca75" />


**Question 3**
---
--Write a SQL query to Identify customers whose city is different from the city of the customer with the highest ID SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER

```sql
--SELECT *
FROM customer
WHERE city <> (
    SELECT city
    FROM customer
    WHERE id = (SELECT MAX(id) FROM customer)
);
```

**Output:**

<img width="1243" height="537" alt="441123193-7ac19955-caf9-4ec4-9728-cf306c683979" src="https://github.com/user-attachments/assets/333a2edc-43db-49ea-807a-5e4d8f789b31" />


**Question 4**
---
-- Write a SQL query to Retrieve the names of customers who have a phone number that is not shared with any other customer. SAMPLE TABLE: customer

name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER

```sql
-- SELECT name
FROM customer
WHERE phone IN (
    SELECT phone
    FROM customer
    GROUP BY phone
    HAVING COUNT(*) = 1
);
```

**Output:**

<img width="812" height="490" alt="441123964-d3aaaee9-420a-4a99-9392-e2c54b498511" src="https://github.com/user-attachments/assets/f14657a0-6c06-4aaa-b66e-81d338433cea" />


**Question 5**
---
--Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)

<img width="727" height="292" alt="441124269-c0d045aa-4f81-4584-ab4a-cd9ad6ec0363" src="https://github.com/user-attachments/assets/5950790f-dabd-482e-8c3f-922f854c5316" />


```sql
-- SELECT *
FROM Grades g
WHERE grade = (
    SELECT MAX(grade)
    FROM Grades
    WHERE subject = g.subject
);
```

**Output:**

<img width="1248" height="442" alt="441124619-1622ea28-49bc-4fa5-9237-a65aab635a0e" src="https://github.com/user-attachments/assets/3e7284ba-53d6-4f82-bd96-b2aad2ef924e" />


**Question 6**
---
--  Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi

Sample table: CUSTOMERS


ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000



```sql
-- SELECT *
FROM CUSTOMERS
WHERE ADDRESS = 'Delhi';
```

**Output:**

<img width="1242" height="370" alt="441125293-400b166d-7512-49dc-9eb6-aca2ca7714b8" src="https://github.com/user-attachments/assets/70c9ebee-bcbe-458d-9b3e-71fe7503a659" />


**Question 7**
---
--  Write a SQL query to Retrieve the names and cities of customers who have the same city as customers with IDs 3 and 7

SAMPLE TABLE: customer


name             type
---------------  ---------------
id               INTEGER
name             TEXT
city             TEXT
email            TEXT
phone            INTEGER

```sql
-- SELECT name, city
FROM customer
WHERE city IN (
    SELECT city
    FROM customer
    WHERE id IN (3, 7)
);
```

**Output:**

<img width="872" height="448" alt="441125745-b60183fb-f979-4821-931b-b2f8b297ad78" src="https://github.com/user-attachments/assets/0c08450d-3ba8-4d1c-a4cd-1486273230dc" />


**Question 8**
---
-- Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the maximum grade achieved in each subject. Sample table: GRADES

<img width="747" height="281" alt="441126732-bf246299-c6d3-4770-854d-d9c0fdf37cbd" src="https://github.com/user-attachments/assets/a2101ee6-757a-485d-9999-9f393191e4de" />


```sql
-- select student_name   ,  grade
from GRADES g
where grade =
(
     select max(grade)
     from GRADES
     where subject = g.subject
);
```

**Output:**

<img width="823" height="417" alt="441127074-6738e361-a609-4902-a782-c6e06040f2ac" src="https://github.com/user-attachments/assets/392a4695-aa52-448b-8e59-ba0dd25b9ac3" />


**Question 9**
---
-- Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is LESS than $2500.

Sample table: CUSTOMERS


ID          NAME        AGE         ADDRESS     SALARY
----------  ----------  ----------  ----------  ----------

1          Ramesh     32              Ahmedabad     2000
2          Khilan        25              Delhi                 1500
3          Kaushik      23              Kota                  2000
4          Chaitali       25             Mumbai            6500
5          Hardik        27              Bhopal              8500
6          Komal         22              Hyderabad       4500

7           Muffy          24              Indore            10000

```sql
-- select *
from CUSTOMERS
where SALARY < 2500;
```

**Output:**

<img width="1237" height="447" alt="441127627-d7c3e604-6c72-4a2c-a51c-f34c15b61bc7" src="https://github.com/user-attachments/assets/df1528b1-ca17-481c-aacc-27aeb1f553d0" />


**Question 10**
---
--From the following tables write a SQL query to find the order values greater than the average order value of 10th October 2012. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

Note: date should be yyyy-mm-dd format ORDERS TABLE


name            type
----------     ----------
ord_no          int
purch_amt    real
ord_date       text
customer_id  int
salesman_id  int

```sql
-- select * 
from ORDERS
where purch_amt >
(
     select purch_amt
     from ORDERS
     where ord_date = '2012-10-10'
);
```

**Output:**

<img width="1246" height="447" alt="441128714-4e78fefc-67a9-4d14-84b9-e972e14fd3eb" src="https://github.com/user-attachments/assets/22c9b5a9-036d-462e-b1b0-83b913eb488e" />



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
