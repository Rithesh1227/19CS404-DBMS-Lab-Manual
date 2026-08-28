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
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi

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
SELECT *
FROM CUSTOMERS
WHERE ADDRESS = 'Delhi';
```

**Output:**

<img width="1280" height="400" alt="image" src="https://github.com/user-attachments/assets/6219072f-e25f-4e9f-906e-5c773e26756e" />

**Question 2**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is EQUAL TO $1500.

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
SELECT *
FROM CUSTOMERS
WHERE SALARY = 1500;
```

**Output:**

<img width="1257" height="392" alt="image" src="https://github.com/user-attachments/assets/76375236-273c-4f92-8c3f-92f52d0509da" />

**Question 3**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $1500.

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
SELECT *
FROM CUSTOMERS
WHERE SALARY > 1500;
```

**Output:**

<img width="1263" height="635" alt="image" src="https://github.com/user-attachments/assets/d184ccc1-a858-4b89-86a1-79e5ef1884b5" />


**Question 4**
---
Write a SQL query that retrieve all the columns from the table "Grades", where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)



```sql
SELECT *
FROM GRADES g
WHERE grade = (
    SELECT MAX(grade)
    FROM GRADES
    WHERE subject = g.subject
);
```

**Output:**
<img width="1332" height="487" alt="image" src="https://github.com/user-attachments/assets/576902ae-56dd-4b64-9658-5d58f48abad2" />

**Question 5**
---
From the following tables write a SQL query to find the order values greater than the average order value of 10th October 2012. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

Note: date should be yyyy-mm-dd format

ORDERS TABLE

name            type
----------     ----------
ord_no          int
purch_amt    real
ord_date       text
customer_id  int
salesman_id  int

```sql
SELECT ord_no, purch_amt, ord_date, customer_id, salesman_id
FROM ORDERS
WHERE purch_amt > (
    SELECT AVG(purch_amt)
    FROM ORDERS
    WHERE ord_date = '2012-10-10'
);
```

**Output:**
<img width="1301" height="517" alt="image" src="https://github.com/user-attachments/assets/d73fbb66-cb62-4db4-8493-3cd0545cc60e" />


**Question 6**
---
From the following tables, write a SQL query to find all the orders issued by the salesman 'Paul Adam'. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

salesman table

name             type
---------------  ---------------
salesman_id      numeric(5)
name                 varchar(30)
city                    varchar(15)
commission       decimal(5,2)

orders table

name             type
---------------  --------
order_no         int
purch_amt        real
order_date       text
customer_id      int
salesman_id      int

```sql
SELECT ord_no, purch_amt, ord_date, customer_id, salesman_id
FROM orders
WHERE salesman_id = (
    SELECT salesman_id
    FROM salesman
    WHERE name = 'Paul Adam'
);
```

**Output:**

<img width="1282" height="456" alt="image" src="https://github.com/user-attachments/assets/010f28b5-359f-46c2-8f21-cd3b54806e84" />


**Question 7**
---
From the following tables, write a SQL query to find all the orders generated in New York city. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

SALESMAN TABLE

name               type
-----------        ----------
salesman_id  numeric(5)
name             varchar(30)
city                 varchar(15)
commission   decimal(5,2)

ORDERS TABLE

name            type
----------      ----------
ord_no          int
purch_amt    real
ord_date       text
customer_id  int
salesman_id  int

```sql
SELECT ord_no, purch_amt, ord_date, customer_id, salesman_id
FROM orders
WHERE salesman_id IN (
    SELECT salesman_id
    FROM salesman
    WHERE city = 'New York'
);
```

**Output:**

<img width="1277" height="572" alt="image" src="https://github.com/user-attachments/assets/e23fb289-ffb8-468e-aca5-09b90ac12d69" />


**Question 8**
---
Write a SQL query to List departments with names longer than the average length

Departments Table (attributes: department_id, department_name)

```sql
SELECT department_id AS depar, department_name
FROM Departments
WHERE LENGTH(department_name) > (
    SELECT AVG(LENGTH(department_name))
    FROM Departments
);
```

**Output:**

<img width="1032" height="497" alt="image" src="https://github.com/user-attachments/assets/00c50429-e06f-42a7-9f11-e441d920d18c" />


**Question 9**
---
Write a SQL query to Retrieve the medications with dosages equal to the lowest dosage

Table Name: Medications (attributes: medication_id, medication_name, dosage)

```sql
SELECT medication_id AS medic, medication_name, dosage
FROM Medications
WHERE dosage = (
    SELECT MIN(dosage)
    FROM Medications
);
```

**Output:**

<img width="980" height="452" alt="image" src="https://github.com/user-attachments/assets/a01afaab-c0b9-4c3c-9838-9c838fb28373" />

**Question 10**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is greater than $4500.

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
SELECT *
FROM CUSTOMERS
WHERE SALARY > 4500;
```

**Output:**

<img width="1273" height="495" alt="image" src="https://github.com/user-attachments/assets/6bfb5e57-02ce-414f-adec-761af421eb54" />


## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
