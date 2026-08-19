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
-- Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.

```sql
create table item
(
    item_id text primary key,
    item_desc text not null,
    rate integer not null,
    icom_id text check(length(icom_id)=4),
    foreign key (icom_id) references company(com_id)
        on update cascade
        on delete cascade
);
```

**Output:**

<img width="962" height="268" alt="image" src="https://github.com/user-attachments/assets/09a926bb-efbd-47fb-99d6-5d85567ea751" />


**Question 2**
---
-- Write an SQL Query to add the attributes designation, net_salary, and dob to the Companies table with the following data types:
designation as VARCHAR(50)
net_salary as NUMBER
dob as DATE
```sql
alter table Companies add column designation varchar(50);
alter table Companies add column net_salary number;
alter table Companies add column dob date;
```

**Output:**

<img width="1226" height="395" alt="image" src="https://github.com/user-attachments/assets/29fa51f6-27a7-4acb-a82f-e6c9ad2e3368" />


**Question 3**
---
-- Insert the below data into the Customers table, allowing the City and ZipCode columns to take their default values.

CustomerID  Name          Address
----------  ------------  ----------
304         Peter Parker  Spider St      


```sql
-- insert into Customers(CustomerID,Name,Address) values(304,"Peter Parker","Spider St");
```

**Output:**

<img width="1162" height="285" alt="image" src="https://github.com/user-attachments/assets/306efa98-8452-4ce7-950e-3c6d881e0245" />


**Question 4**
---
-- Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should set NULL on updates and deletes.
item_desc and rate should not accept NULL.

```sql
-- create table item(
    item_id text primary key,
    item_desc text not null,
    rate integer not null,
    icom_id text check(length(icom_id)=4),
    foreign key (icom_id) references company(com_id)
        on update set null
        on delete set null
);
```

**Output:**

<img width="1228" height="347" alt="image" src="https://github.com/user-attachments/assets/eb63cbdf-67ed-41ae-9e01-4a695c44e28e" />


**Question 5**
---
-- Write a SQL query to add a column named Date_of_birth as Date in the Student_details table.

```sql
-- alter table Student_details add column Date_of_birth Date;
```

**Output:**

<img width="1262" height="330" alt="image" src="https://github.com/user-attachments/assets/b93d0686-c1b7-4f30-ad32-d34bd94ab929" />


**Question 6**
---
-- Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0

```sql
-- create table Invoices(
   InvoiceID integer primary key,
   InvoiceDate Date,
   DueDate Date check(DueDate>InvoiceDate),
   Amount Real check(Amount>0));
```

**Output:**

<img width="1191" height="282" alt="image" src="https://github.com/user-attachments/assets/cfbf510d-eb28-490f-9247-4dac4fd69bd0" />


**Question 7**
---
--In the Student_details table, insert a student record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

RollNo      Name            Gender      Subject      MARKS
----------  ------------    ----------  ----------   ----------
205         Olivia Green    F
207         Liam Smith      M           Mathematics  85
208         Sophia Johnson  F           Science

```sql
-- insert into Student_details values(205,"Olivia Green","F",null,null);
insert into Student_details(RollNo,Name,Gender,Subject,MARKS) values(207,"Liam Smith","M","Mathematics",85);
insert into Student_details(RollNo,Name,Gender,Subject,MARKS) values(208,"Sophia Johnson","F","Science",null);
```

**Output:**

<img width="1218" height="270" alt="image" src="https://github.com/user-attachments/assets/590b91e9-afc4-47cd-b255-180eb4432eb0" />


**Question 8**
---
-- Create a table named Employees with the following columns:

EmployeeID as INTEGER
FirstName as TEXT
LastName as TEXT
HireDate as DATE
```sql
--create table Employees(
    EmployeeID INTEGER,
    FirstName TEXT,
    LastName TEXT,
    HireDate DATE);
```

**Output:**

<img width="1222" height="308" alt="image" src="https://github.com/user-attachments/assets/3899817e-e085-4bd7-ab23-fd705d21daf7" />

**Question 9**
---
-- Create a new table named contacts with the following specifications:
contact_id as INTEGER and primary key.
first_name as TEXT and not NULL.
last_name as TEXT and not NULL.
email as TEXT.
phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.

```sql
-- create table contacts(
    contact_id integer primary key,
    first_name text not null,
    last_name text not null,
    email text,
    phone text not null check(length(phone)>=10));
```

**Output:**

<img width="1235" height="318" alt="image" src="https://github.com/user-attachments/assets/5372540a-f96f-482a-aec3-4073d5f94dd8" />


**Question 10**
---
-- Insert all students from Archived_students table into the Student_details table.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      INT           0                       1
1           Name        VARCHAR(100)  0                       0
2           Gender      VARCHAR(10)   0                       0
3           Subject     VARCHAR(50)   0                       0
4           MARKS       INT           0                       0

```sql
insert into Student_details
select * from Archived_students;
```

**Output:**

<img width="1227" height="267" alt="image" src="https://github.com/user-attachments/assets/f7510e53-82ec-4a20-9e24-967e5f1b9a0d" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
