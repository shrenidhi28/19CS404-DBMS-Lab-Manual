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
<img width="864" alt="image" src="https://github.com/user-attachments/assets/8cf8e3a6-ee7c-4731-9ce7-2e1c33d6aab9" />


```sql
-- select salesman.name as Salesman, customer.cust_name, salesman.city from salesman inner join customer on salesman.city=customer.city;

```

**Output:**
<img width="927" alt="image" src="https://github.com/user-attachments/assets/b9ab4dc2-bf4c-4f44-879e-a2c3f95704e0" />


**Question 2**
---
<img width="916" alt="image" src="https://github.com/user-attachments/assets/014ae8b0-85cf-4fb6-abd0-f9628f8cee40" />


```sql
-- select customer.cust_name,customer.city,customer.grade,salesman.name as Salesman,salesman.city from customer inner join salesman on customer.salesman_id=salesman.salesman_id where customer.grade<300 order by customer.customer_id;
```

**Output:**

<img width="962" alt="image" src="https://github.com/user-attachments/assets/6acba85b-77d5-4a5b-9eab-be97a6a6c430" />


**Question 3**
---
<img width="962" alt="image" src="https://github.com/user-attachments/assets/f616e3fb-d1db-4fbd-8716-f4482586fc7c" />


```sql
-- select s.name,c.cust_name,c.city,c.grade,c.salesman_id from Salesman s left join Customer c on s.salesman_id=c.salesman_id;

```

**Output:**

<img width="962" alt="image" src="https://github.com/user-attachments/assets/bb8cfed6-c58e-4311-b2c2-528610ba7cb2" />


**Question 4**
---
<img width="962" alt="image" src="https://github.com/user-attachments/assets/a058ae17-2ac5-4822-b5b5-dceab42c433b" />


```sql
-- select p.first_name as patient_name, t.* from PATIENTS p inner join test_results t on p.patient_id=t.patient_id where t.test_name='Blood Pressure';
```

**Output:**

<img width="972" alt="image" src="https://github.com/user-attachments/assets/9383a93e-1dd6-422f-ba4f-cbfbb22f0d19" />


**Question 5**
---
<img width="736" alt="image" src="https://github.com/user-attachments/assets/3bc39b5c-930a-49d3-823f-9d1e53003edc" />


```sql
-- select o.ord_no,o.ord_date,o.purch_amt,
c.cust_name as 'Customer Name',c.grade, s.name as Salesman,s.commission from orders o inner join customer c on o.customer_id=c.customer_id inner join salesman s on o.salesman_id=s.salesman_id;
```

**Output:**

<img width="1032" alt="image" src="https://github.com/user-attachments/assets/b25d4b77-ce10-4472-984a-a4550b4719ac" />


**Question 6**
---
--From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.

Sample table: customer

customer_id | cust_name | city | grade | salesman_id -------------+----------------+------------+-------+------------- 3002 | Nick Rimando | New York | 100 | 5001 3007 | Brad Davis | New York | 200 | 5001 3005 | Graham Zusi | California | 200 | 5002 3008 | Julian Green | London | 300 | 5002 3004 | Fabian Johnson | Paris | 300 | 5006 3009 | Geoff Cameron | Berlin | 100 | 5003 3003 | Jozy Altidor | Moscow | 200 | 5007 3001 | Brad Guzan | London | | 5005 Sample table: orders

ord_no purch_amt ord_date customer_id salesman_id

```sql
-- select o.ord_no,o.purch_amt,c.cust_name,c.city from orders o
join customer c on o.customer_id=c.customer_id
where o.purch_amt between 500 and 2000;
```

**Output:**

<img width="1015" alt="image" src="https://github.com/user-attachments/assets/962ecbe0-1b24-4d7d-8f80-d0527f333bcf" />


**Question 7**
---
-- Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the first name from the "doctors" table (aliased as "doctor_name"), with an inner join on the "doctor_id" column and a condition filtering for patients with a null discharge date.
PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id

DOCTORS TABLE:

ATTRIBUTES - doctor_id, first_name, last_name, specialization

```sql
-- select p.first_name as patient_name,d.first_name as doctor_name from patients p
inner join doctors d on p.doctor_id = d.doctor_id
where p.discharge_date is null;
```

**Output:**

<img width="780" alt="image" src="https://github.com/user-attachments/assets/87a1a867-5cb1-44e1-9f69-bccfe7e1d0ba" />


**Question 8**
---
-- Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the city 'New York'

```sql
-- left join customer c on s.salesman_id=c.salesman_id
where c.city="New York";
```

**Output:**

<img width="780" alt="image" src="https://github.com/user-attachments/assets/80833a09-a71c-43e1-9f7d-c912d4dbe6ce" />


**Question 9**
---
<img width="1022" alt="image" src="https://github.com/user-attachments/assets/aaa6d7dc-49f3-4e0b-9e45-b0f8d27d57d4" />


```sql
-- select c.cust_name as"Customer Name",c.city,s.name as Salesman,s.commission from customer c
join salesman s on c.salesman_id=s.salesman_id
where s.commission>0.12;
```

**Output:**

<img width="1023" alt="image" src="https://github.com/user-attachments/assets/ae50a9fe-ff16-4ef7-ab28-179626db6f68" />


**Question 10**
---
-- Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), the "cust_name," "city," "grade," and "salesman_id" columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for customers with a grade less than or equal to 100.

```sql
-- SELECT s.name,
       c.cust_name,
       c.city,
       c.grade,
       c.salesman_id
FROM customer AS c
LEFT JOIN salesman AS s ON c.salesman_id = s.salesman_id
WHERE c.grade <= 100;
```

**Output:**

<img width="1008" alt="image" src="https://github.com/user-attachments/assets/0d9d9f81-968c-4f7b-ad2f-cd688f1fbf2a" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
