# Experiment 2: DDL Commands
### Name : SUJITH A
### Reg No : 212224230278

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
--
--Write a SQL query to Add a new column named "discount" with the data type DECIMAL(5,2) to the "customer" table.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
 

For example:

Test	Result
pragma table_info('customer');
cid         name         type                               notnull     dflt_value  pk
----------  -----------  ---------------------------------  ----------  ----------  ----------
0           customer_id  integer primarykey auto increment  0                       0
1           cust_name    varchar2(30)                       0                       0
2           city         varchar(30)                        0                       0
3           grade        number                             0                       0
4           salesman_id  number                             0                       0
5           discount     DECIMAL(5,2)                       0                       0


```sql
-- ALTER TABLE CUSTOMER
ADD discount DECIMAL(5,2);
```

**Output:**

![Screenshot (56)](https://github.com/user-attachments/assets/7acafeb1-6af0-49ce-895b-0692e3da86df)


**Question 2**
---
-- Create a table named Employees with the following columns:

EmployeeID as INTEGER
FirstName as TEXT
LastName as TEXT
HireDate as DATE
For example:

Test	Result
pragma table_info('Employees');
cid   name        type        notnull     dflt_value  pk
----  ----------  ----------  ----------  ----------  ----------
0     EmployeeID  INTEGER     0                       0
1     FirstName   TEXT        0                       0
2     LastName    TEXT        0                       0
3     HireDate    DATE        0                       0

```sql
-- create table Employees(
EmployeeID  INTEGER,
FirstName  TEXT,
LastName  TEXT,
HireDate  DATE);
```

**Output:**

![image](https://github.com/user-attachments/assets/7d1b0181-6502-468f-9657-4ace778d16e8)


**Question 3**
---
-- Create a table named Department with the following constraints:
DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.
For example:

Test	Result
INSERT INTO Department (DepartmentID, DepartmentName, Location) VALUES (1, 'Human Resources', 'New York');
select * from Department;
DepartmentID  DepartmentName   Location
------------  ---------------  ----------
1             Human Resources  New York

```sql
-- CREATE TABLE Department(
DepartmentID  INTEGER primary key,
DepartmentName TEXT unique not null,
Location TEXT);
```

**Output:**

![image](https://github.com/user-attachments/assets/9e98217a-979c-4c7f-bcd5-ecfecfdc4d41)


**Question 4**
---
-- Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
For example:

Test	Result
INSERT INTO Shipments (ShipmentID, ShipmentDate, SupplierID, OrderID) VALUES (2, '2024-08-03', 99, 1);
Error: FOREIGN KEY constraint failed


```sql
--create table Shipments(
ShipmentID INTEGER PRIMARY KEY,
ShipmentDate DATE,
SupplierID integer,
OrderID INTEGER,
foreign key (SupplierID) REFERENCES Suppliers(SupplierID),
FOREIGN KEY (OrderID) references Orders(OrderID));
```

**Output:**

![image](https://github.com/user-attachments/assets/ea95de5b-ab0a-423f-aba3-86bbc7fec952)


**Question 5**
---
-- In the Books table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ISBN             Title                      Author           Publisher   Year
---------------  -------------------------  ---------------  ----------  ----------
978-1234567890   Introduction to AI         John Doe
978-9876543210   Deep Learning              Jane Doe         TechPress   2022
978-1122334455   Cybersecurity Essentials   Alice Smith                  2021
For example:

Test	Result
SELECT * FROM Books;
ISBN             Title                      Author           Publisher   Year
---------------  -------------------------  ---------------  ----------  ----------
978-1234567890   Introduction to AI         John Doe
978-9876543210   Deep Learning              Jane Doe         TechPress   2022
978-1122334455   Cybersecurity Essentials   Alice Smith                  2021


```sql
-- INSERT INTO Books(ISBN,Title,Author,Publisher,Year)
VALUES('978-1234567890','Introduction to AI','John Doe',NULL,NULL),
('978-9876543210','Deep Learning','Jane Doe','TechPress',2022),
('978-1122334455','Cybersecurity Essentials','Alice Smith',NULL,2021);

```

**Output:**

![image](https://github.com/user-attachments/assets/b7980ae6-8c49-4bd9-a6d9-2dad5805350f)


**Question 6**
---
-- Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.
For example:

Test	Result
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");
UPDATE company SET com_id='COM5' WHERE com_id='COM4';
SELECT * FROM item;
item_id     item_desc     rate        icom_id
----------  ------------  ----------  ----------
ITM5        Charlie Gold  700         COM5

```sql
-- CREATE TABLE item(
item_id text primary key,
item_desc text,
rate integer,
icom_id text CHECK (LENGTH(icom_id)=4),
foreign key(icom_id) references company(com_id)
on update cascade
on delete cascade
);
```

**Output:**

![image](https://github.com/user-attachments/assets/b130d013-b196-4e84-8b48-4d71859a61f0)


**Question 7**
---
-- Write a SQL query to Add a new column State as text in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0
For example:

Test	Result
pragma table_info('Student_details');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      int         0                       1
1           Name        VARCHAR(10  1                       0
2           Gender      TEXT        1                       0
3           Subject     VARCHAR(30  0                       0
4           MARKS       INT (3)     0                       0
5           State       TEXT    

```sql
-- alter table Student_details
add column State TEXT;
```

**Output:**

![image](https://github.com/user-attachments/assets/0cbc9ecb-de4e-4253-9738-d8188a892acf)


**Question 8**
---
--Insert the below data into the Customers table, allowing the City and ZipCode columns to take their default values.

CustomerID  Name          Address
----------  ------------  ----------
304         Peter Parker  Spider St      

Note: The City and ZipCode columns will use their default values.
 
For example:

Test	Result
SELECT CustomerID, Name, Address
FROM Customers;
CustomerID  Name          Address
----------  ------------  ----------
304         Peter Parker  Spider St


```sql
-- INSERT INTO Customers(CustomerID,Name,Address)
VALUES('304','Peter Parker','Spider St');
```

**Output:**

![image](https://github.com/user-attachments/assets/93bb2b64-ef8e-4a66-8357-d8bdc42e1996)


**Question 9**
---
-- Insert all students from Archived_students table into the Student_details table.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      INT           0                       1
1           Name        VARCHAR(100)  0                       0
2           Gender      VARCHAR(10)   0                       0
3           Subject     VARCHAR(50)   0                       0
4           MARKS       INT           0                       0
For example:

Test	Result
select * from student_details;
RollNo      Name           Gender      Subject     MARKS
----------  -------------  ----------  ----------  ----------
1           Alice Johnson  Female      Math        85
2           Bob Smith      Male        Science     90
3           Charlie Brown  Male        English     78

```sql
-- insert into Student_details(RollNo,Name, Gender,Subject,MARKS)
select RollNo,Name,Gender,Subject,MARKS
from Archived_students;
```

**Output:**

![image](https://github.com/user-attachments/assets/b0283e60-24a0-4f74-a3cf-51874166d117)


**Question 10**
---
-- Create a table named Products with the following constraints:
ProductID as INTEGER should be the primary key.
ProductName as TEXT should be unique and not NULL.
Price as REAL should be greater than 0.
StockQuantity as INTEGER should be non-negative.
For example:

Test	Result
INSERT INTO Products (ProductID, ProductName, Price, StockQuantity) VALUES (1, 'Laptop', 999.99, 10);
select * from Products;
ProductID   ProductName  Price       StockQuantity
----------  -----------  ----------  -------------
1           Laptop       999.99      10


```sql
-- create table Products(
ProductID INTEGER PRIMARY KEY,
ProductName TEXT UNIQUE NOT NULL,
Price REAL check(Price>0),
StockQuantity INTEGER check(StockQuantity>0)
);
```

**Output:**

![image](https://github.com/user-attachments/assets/ed11553e-a229-45b4-abdd-44929c34d248)

MODULE 1 (SEB) GRADE SCREENSHOT:
![image](https://github.com/user-attachments/assets/75512c43-07e2-411d-884f-ac786fb618a3)


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
