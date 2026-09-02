# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**

Insert a book with ISBN 978-1234567890, Title Data Science Essentials, Author Jane Doe, Publisher TechBooks, and Year 2024 into the Books table.

sql
```
INSERT INTO Books (ISBN, Title, Author, Publisher, Year)
VALUES ('978-1234567890', 'Data Science Essentials', 'Jane Doe', 'TechBooks', 2024);
```

**Output:**

<img width="1212" height="287" alt="image" src="https://github.com/user-attachments/assets/e2610c27-22c8-4d9e-9133-a84cacb64806" />


**Question 2**

Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).

sql
```
CREATE TABLE Orders (
    OrderID INTEGER PRIMARY KEY,
    OrderDate DATE NOT NULL,
    CustomerID INTEGER,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);

```

**Output:**

<img width="1228" height="290" alt="image" src="https://github.com/user-attachments/assets/b604862d-d57d-49d7-97fe-e58c52b4d16e" />


**Question 3**

Insert all students from Archived_students table into the Student_details table.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      INT           0                       1
1           Name        VARCHAR(100)  0                       0
2           Gender      VARCHAR(10)   0                       0
3           Subject     VARCHAR(50)   0                       0
4           MARKS       INT           0                       0


sql
```
INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS)
SELECT RollNo, Name, Gender, Subject, MARKS
FROM Archived_students;

```

**Output:**

<img width="1231" height="295" alt="image" src="https://github.com/user-attachments/assets/f31a494a-6c81-4f9c-b52b-6106a6127080" />


**Question 4**

Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL

sql
```
CREATE TABLE ProjectAssignments (
    AssignmentID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    ProjectID INTEGER,
    AssignmentDate DATE NOT NULL,
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID),
    FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID)
);
```

**Output:**

<img width="1238" height="321" alt="image" src="https://github.com/user-attachments/assets/cdb2534c-7eda-4bb2-87c0-88c5da155d0c" />


**Question 5**

Create a new table named contacts with the following specifications:
contact_id as INTEGER and primary key.
first_name as TEXT and not NULL.
last_name as TEXT and not NULL.
email as TEXT.
phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.

sql
```
CREATE TABLE contacts (
    contact_id INTEGER PRIMARY KEY,
    first_name TEXT NOT NULL,
    last_name TEXT NOT NULL,
    email TEXT,
    phone TEXT NOT NULL CHECK (LENGTH(phone) >= 10)
);

```

**Output:**

<img width="1211" height="370" alt="image" src="https://github.com/user-attachments/assets/b9e0377d-9a24-4eaf-b466-fe9a6338cc44" />


**Question 6**

In the Cusomers table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

CustomerID  Name          Address      City        ZipCode
----------  ------------  ----------   ----------  ----------
306         Diana Prince  Themyscira
307         Bruce Wayne   Wayne Manor  Gotham      10007
308         Peter Parker  Queens                   11375

 
sql
```
INSERT INTO Customers (CustomerID, Name, Address, City, ZipCode)
VALUES 
(306, 'Diana Prince', 'Themyscira', NULL, NULL),
(307, 'Bruce Wayne', 'Wayne Manor', 'Gotham', '10007'),
(308, 'Peter Parker', 'Queens', NULL, '11375');

```

**Output:**

<img width="1202" height="285" alt="image" src="https://github.com/user-attachments/assets/81c6d6d0-e4a2-4dc0-8ef6-e9fa6de5df31" />


**Question 7**

Create a table named Departments with the following columns:

DepartmentID as INTEGER
DepartmentName as TEXT

sql
```
CREATE TABLE Departments (
    DepartmentID INTEGER,
    DepartmentName TEXT
);

```

**Output:**

<img width="1217" height="401" alt="image" src="https://github.com/user-attachments/assets/de1bd52f-c3a0-493e-87ff-48321460dee3" />


**Question 8**

Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0

sql
```
CREATE TABLE Products (
    ProductID INTEGER PRIMARY KEY,
    ProductName TEXT NOT NULL,
    Price REAL CHECK (Price > 0),
    Stock INTEGER CHECK (Stock >= 0)
);

```

**Output:**

<img width="1272" height="327" alt="image" src="https://github.com/user-attachments/assets/1adfb682-8820-4760-be35-ccdb04cbfd45" />


**Question 9**

Write an SQL query to add a new column salary of type INTEGER to the Employees table, with a CHECK constraint that ensures the value in this column is greater than 0.


sql
```
ALTER TABLE Employees
ADD COLUMN salary INTEGER CHECK (salary > 0);

```

**Output:**

<img width="1188" height="295" alt="image" src="https://github.com/user-attachments/assets/211741c2-5d71-4832-9e66-b8bffe00d669" />


**Question 10**

Write a SQL query to Add a new column named "discount" with the data type DECIMAL(5,2) to the "customer" table.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002

sql
```
ALTER TABLE customer
ADD COLUMN discount DECIMAL(5,2);

```

**Output:**

<img width="1212" height="401" alt="image" src="https://github.com/user-attachments/assets/ca8afd20-585c-4b41-a0c4-ac70fe79be4c" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
