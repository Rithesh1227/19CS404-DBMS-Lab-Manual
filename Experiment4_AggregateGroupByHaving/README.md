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
-- How many appointments are scheduled for each patient?

Sample table: Appointments Table

name                  type
--------------------  ----------
AppointmentID         INTEGER
PatientID             INTEGER
DoctorID              INTEGER
AppointmentDateTime   DATETIME
Purpose               TEXT
Status                TEXT

```sql
select patientID, count(*) as TotalAppointments from Appointments
group by PatientID;
```

**Output:**

<img width="681" height="688" alt="image" src="https://github.com/user-attachments/assets/2460babe-032f-4880-9edb-5b009b04ebc1" />


**Question 2**
---
-- Write a SQL Query to find how many medications are prescribed for each patient?

Sample table:MedicalRecords Table



For example:

Result
PatientID   AvgMedications
----------  --------------
4           5
6           1
7           1
8           3


```sql
select PatientID,count(*) as AvgMedications from MedicalRecords
group by PatientID;
```

**Output:**

<img width="722" height="665" alt="image" src="https://github.com/user-attachments/assets/9fc1922c-3053-4b3d-aa63-4d7136f05203" />


**Question 3**
---
-- How many patients have insurance coverage valid in each year?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
ValidityPeriod     TEXT

```sql
select strftime("%Y",ValidityPeriod) as ValidityYear, count(*) as TotalPatients from Insurance
group by ValidityPeriod;
```

**Output:**

<img width="717" height="416" alt="image" src="https://github.com/user-attachments/assets/d967b835-b3e7-49e1-bab2-166aa5c53fd9" />

**Question 4**
---
--Write a SQL query to find the average length of email addresses (in characters):

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER

```sql
select avg(length(email)) as avg_email_length from customer;
```

**Output:**

<img width="625" height="441" alt="image" src="https://github.com/user-attachments/assets/0709221c-0f2c-4dc6-a56c-157be454e4b8" />


**Question 5**
---
-- Write a SQL query to find the shortest email address in the customer table?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT   
city        TEXT
email       TEXT
phone       INTEGER

```sql
select name,email,length(email) as min_email_length from customer 
where length(email)=(select min(length(email)) from customer) limit 1;
```

**Output:**

<img width="1148" height="407" alt="image" src="https://github.com/user-attachments/assets/8b3856bb-8db3-4cd2-84ff-770baeec2e1d" />


**Question 6**
---
--Write a SQL query to find What is the age difference between the youngest and oldest employee in the company.

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER

```sql
select max(age)-min(age) as age_difference from employee;
```

**Output:**

<img width="653" height="327" alt="image" src="https://github.com/user-attachments/assets/9029bb3e-669e-46ce-970d-6112c8f3b76f" />


**Question 7**
---
-- Write a SQL query to  find the average salary of all employees?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER

```sql
select avg(income) as Average_Salary from employee;
```

**Output:**

<img width="605" height="375" alt="image" src="https://github.com/user-attachments/assets/1894956f-c31d-4138-95e3-63fcb8c5755f" />

**Question 8**
---
-- Write the SQL query to find how many patients have more than 3 medical records?.

Sample table: MedicalRecords

name        type
----------  ----------
RecordID    INTEGER
PatientID   INTEGER
DoctorID    INTEGER
Date        DATE
Diagnosis   TEXT
Treatment   TEXT
Medication  TEXT

```sql
select PatientID, count(*) as TotalRecords from MedicalRecords
group by PatientID
having TotalRecords > 3;

```

**Output:**

<img width="663" height="388" alt="image" src="https://github.com/user-attachments/assets/5f80a381-b009-43e3-a841-7842330ac588" />


**Question 9**
---
-- Write the SQL query that achieves the grouping of data by age, calculates the minimum income for each age group, and includes only those age groups where the minimum income is less than 1,000,000.

Sample table: employee

```sql
select age,min(income) as Income from employee
group by age
having Income <1000000;
```

**Output:**

<img width="793" height="510" alt="image" src="https://github.com/user-attachments/assets/e5c00232-35fe-44f7-b2d5-953300fff9ba" />


**Question 10**
---
--Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the minimum work hours for each date, and excludes dates where the minimum work hour is not less than 10.

Sample table: employee1



```sql
select jdate, MIN(workhour) from employee1
where  workhour<10
group by jdate;
```

**Output:**

<img width="716" height="493" alt="image" src="https://github.com/user-attachments/assets/1278eb6e-dafe-4735-84d4-59e022e8a5fa" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
