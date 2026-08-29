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
From the following tables write a SQL query to find the details of an order. Return ord_no, ord_date, purch_amt, Customer Name, grade, Salesman, commission. 

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

```sql
SELECT
    o.ord_no,
    o.ord_date,
    o.purch_amt,
    c.cust_name AS "Customer Name",
    c.grade,
    s.name AS "Salesman",
    s.commission
FROM orders o
JOIN customer c
    ON o.customer_id = c.customer_id
JOIN salesman s
    ON o.salesman_id = s.salesman_id;
```

**Output:**

<img width="1231" height="780" alt="image" src="https://github.com/user-attachments/assets/93e461b3-6bfd-4d47-a8c5-de3d2f6c1cb4" />


**Question 2**
---
write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11
        5006 | Mc Lyon    | Paris    |       0.14
        5007 | Paul Adam  | Rome     |       0.13
        5003 | Lauson Hen | San Jose |       0.12
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

```sql
SELECT 
    s.name AS Salesman,
    c.cust_name,
    c.city
FROM salesman s
JOIN customer c
    ON s.city = c.city;
    
```

**Output:**

<img width="1047" height="677" alt="image" src="https://github.com/user-attachments/assets/30c77247-05e9-445a-80d0-bf3af13eb4c9" />


**Question 3**
---
Write the SQL query that accomplishes the selection of the first name from the "patients" table (aliased as "patient_name") and the first name from the "doctors" table (aliased as "doctor_name"), with an inner join on the "doctor_id" column and a condition filtering for patients with a non-null discharge date.

PATIENTS TABLE:
name             type
---------------  ---------------
patient_id       INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
date_of_birth    DATE
admission_date   DATE
discharge_date   DATE
doctor_id        INT

DOCTORS TABLE:

name             type
---------------  ---------------
doctor_id        INT
first_name       VARCHAR(50)
last_name        VARCHAR(50)
specialization   VARCHAR(100)

```sql
SELECT 
    p.first_name AS patient_name,
    d.first_name AS doctor_name
FROM patients p
INNER JOIN doctors d
    ON p.doctor_id = d.doctor_id
WHERE p.discharge_date IS NOT NULL;
```

**Output:**

<img width="802" height="362" alt="image" src="https://github.com/user-attachments/assets/7e73d762-9f8d-4e75-bb1d-6df9d6021a2c" />

**Question 4**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "salesman_name") and the "cust_name" column from the "customer" table (aliased as "customer_name"), with a left join on the "salesman_id" column.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)

```sql
SELECT 
    s.name AS salesman_name,
    c.cust_name AS customer_name
FROM salesman s
LEFT JOIN customer c
    ON s.salesman_id = c.salesman_id;
```

**Output:**

<img width="1245" height="737" alt="image" src="https://github.com/user-attachments/assets/64f2c9a6-e65f-40de-84f8-5a4d4e57ac19" />


**Question 5**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "salesman_name") and the "cust_name" column from the "customer" table (aliased as "customer_name"), with a left join on the "salesman_id" column.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)

```sql
SELECT 
    s.name AS salesman_name,
    c.cust_name AS customer_name
FROM salesman s
LEFT JOIN customer c
    ON s.salesman_id = c.salesman_id;
```

**Output:**

<img width="851" height="852" alt="image" src="https://github.com/user-attachments/assets/76e6eb28-4277-4bbf-a940-174852208733" />


**Question 6**
---
From the following tables write a SQL query to locate those salespeople who do not live in the same city where their customers live and have received a commission of more than 12% from the company. Return Customer Name, customer city, Salesman, salesman city, commission.  

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
SELECT
    c.cust_name AS "Customer Name",
    c.city AS city,
    s.name AS Salesman,
    s.city AS city,
    s.commission AS commission
FROM customer c
INNER JOIN salesman s
    ON c.salesman_id = s.salesman_id
WHERE c.city <> s.city
  AND s.commission > 0.12;
```

**Output:**

<img width="1282" height="685" alt="image" src="https://github.com/user-attachments/assets/19da1956-a6aa-4de4-a9a3-a195ae295ca9" />


**Question 7**
---
 From the following tables write a SQL query to find salespeople who received commissions of more than 12 percent from the company. Return Customer Name, customer city, Salesman, commission.  

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
SELECT
    c.cust_name AS "Customer Name",
    c.city,
    s.name AS Salesman,
    s.commission
FROM customer c
INNER JOIN salesman s
    ON c.salesman_id = s.salesman_id
WHERE s.commission > 0.12;
```

**Output:**

<img width="1275" height="756" alt="image" src="https://github.com/user-attachments/assets/ebd0e3f1-affc-4f66-bbf7-91c2ec99a1c3" />


**Question 8**
---
SQL statement to generate a report with customer name, city, order number, order date, order amount, salesperson name, and commission to determine if any of the existing customers have not placed orders or if they have placed orders through their salesman or by themselves.

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
SELECT
    c.cust_name,
    c.city,
    o.ord_no,
    o.ord_date,
    o.purch_amt AS "Order Amount",
    s.name,
    s.commission
FROM customer c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
LEFT JOIN salesman s
    ON c.salesman_id = s.salesman_id;
```

**Output:**

<img width="1265" height="803" alt="image" src="https://github.com/user-attachments/assets/8898997d-9f54-40d1-8684-1a106e60afb7" />


**Question 9**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name"), with an inner join on the "patient_id" column and a condition filtering for test results with the test name 'Blood Pressure'.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id

```sql
SELECT 
    p.first_name AS patient_name
FROM patients p
INNER JOIN test_results t
    ON p.patient_id = t.patient_id
WHERE t.test_name = 'Blood Pressure';
```

**Output:**

<img width="488" height="367" alt="image" src="https://github.com/user-attachments/assets/c0fcd9d0-d65c-4b55-a0a4-1825ef65e115" />

**Question 10**
---
Write the SQL query that achieves the selection of all columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for salesman with the name 'Mc Lyon'.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)

```sql
SELECT c.*
FROM customer AS c
LEFT JOIN salesman AS s
    ON c.salesman_id = s.salesman_id
WHERE s.name = 'Mc Lyon';
```

**Output:**

<img width="1262" height="427" alt="image" src="https://github.com/user-attachments/assets/b804d98d-c8ca-49fd-94ed-5d5a096467cd" />


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
