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
--
-- Write a SQL query to Add a new ParentsNumber column  as number and Adhar_Number as Number in the Student_details table.

```sql
--
ALTER TABLE Student_details ADD ParentsNumber number;
ALTER TABLE Student_details ADD Adhar_Number number;
```

**Output:**

<img width="944" alt="image" src="https://github.com/user-attachments/assets/ec3045fa-d3a9-4104-8b60-0b612558b5ef" />


**Question 2**
---
-- Create a table named Products with the following constraints:

  ProductID as INTEGER should be the primary key.
  ProductName as TEXT should be unique and not NULL.
  Price as REAL should be greater than 0.
  StockQuantity as INTEGER should be non-negative.

```sql
--
create table Products(
ProductID INTEGER primary key,
ProductName TEXT UNIQUE not null,
Price REAL check(Price>0),
StockQuantity INTEGER check(StockQuantity>0)
);

```

**Output:**

<img width="944" alt="image" src="https://github.com/user-attachments/assets/b4856ff1-bd86-45d5-802c-fd7249b19bc7" />


**Question 3**
---
-- Write a SQL Query to add an attribute designation in the employee table with the data type VARCHAR(50).

```sql
-- alter table employee add designation varchar(50);
```

**Output:**

<img width="932" alt="image" src="https://github.com/user-attachments/assets/e66512d2-1038-4208-8ab0-bde548af1fcd" />


**Question 4**
---
-- 
Create a table named Locations with the following columns:

LocationID as INTEGER
LocationName as TEXT
Address as TEXT

```sql
--
create table Locations(
LocationID INTEGER ,
LocationName TEXT ,
Address TEXT );
```

**Output:**

<img width="889" alt="image" src="https://github.com/user-attachments/assets/11e026cf-9172-4ce5-9863-47b3ea212c5a" />


**Question 5**
---
-- 
Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
--
create table Invoices(
InvoiceID INTEGER PRIMARY KEY,
InvoiceDate DATE,
Amount REAL CHECK(Amount>0),
DueDate DATE CHECK(InvoiceDate<DueDate),
OrderID INTEGER REFERENCES Orders(OrderID)
)
```

**Output:**

<img width="905" alt="image" src="https://github.com/user-attachments/assets/68ce1559-0e71-4f7a-8d63-d74c8c965e20" />


**Question 6**
---
-- 
Create a table named Shipments with the following constraints:

ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
--
create table Shipments(
ShipmentID INTEGER PRIMARY KEY,
ShipmentDate DATE,
SupplierID INTEGER REFERENCES Suppliers(SupplierID),
OrderID INTEGER REFERENCES Orders(OrderID)
)
```

**Output:**

<img width="905" alt="image" src="https://github.com/user-attachments/assets/8cedbf0d-69e9-4eb2-b994-efa7b3a2ef5f" />


**Question 7**
---
-- 

Insert the following students into the Student_details table:
RollNo      Name        Gender      Subject     MARKS
----------  ----------  ----------  ----------  ----------
202            Ella King         F           Chemistry   87
203            James Bond   M          Literature    78

```sql
--
insert into Student_details VALUES (202,'Ella King','F','Chemistry',87);
insert into Student_details VALUES (203,'James Bond','M','Literature',78);
```

**Output:**

<img width="905" alt="image" src="https://github.com/user-attachments/assets/41db7eb2-527d-4633-a20b-b1019407f8e7" />


**Question 8**
---
-- Insert all employees from Former_employees into Employee Table attributes are EmployeeID, Name, Department, Salary

```sql
-- insert into Employee select EmployeeID,Name,Department,Salary FROM Former_employees;
```

**Output:**

<img width="905" alt="image" src="https://github.com/user-attachments/assets/21e4ecae-87d3-4c09-99d2-aefb815572f9" />


**Question 9**
---
-- 
Create a new table named products with the following specifications:
product_id as INTEGER and primary key.
product_name as TEXT and not NULL.
list_price as DECIMAL (10, 2) and not NULL.
discount as DECIMAL (10, 2) with a default value of 0 and not NULL.
A CHECK constraint at the table level to ensure:
list_price is greater than or equal to discount
discount is greater than or equal to 0
list_price is greater than or equal to 0

```sql
-- create table products(
product_id INTEGER primary key,
product_name TEXT not NULL ,
list_price DECIMAL(10, 2) not null check(list_price>=discount),
discount DECIMAL (10, 2) default 0 not null check(discount>=0));

```

**Output:**

<img width="905" alt="image" src="https://github.com/user-attachments/assets/8acb150e-b7e9-47b1-aa8f-26da8c3f7c05" />


**Question 10**
---
-- Insert a new product with ProductID 101, Name Laptop, Category Electronics, Price 1500, and Stock 50 into the Products table.

```sql
-- insert into Products values(101,'Laptop','Electronics',1500,50);
```

**Output:**
<img width="905" alt="image" src="https://github.com/user-attachments/assets/5175db2c-15eb-4386-9ac6-6f703dfce09e" />




## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
