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
<img width="916" alt="image" src="https://github.com/user-attachments/assets/d6cf757a-b92f-497a-a086-5dc1692377b1" />

```sql
--  select ord_no,purch_amt,ord_date,customer_id,Orders.salesman_id from Orders join Salesman on Orders.salesman_id=Salesman.salesman_id where Salesman.city='New York';
```

**Output:**

<img width="916" alt="image" src="https://github.com/user-attachments/assets/b4fd74ec-a214-4e86-9bde-0b73aaad8b34" />

**Question 2**
---
<img width="916" alt="image" src="https://github.com/user-attachments/assets/a11e533d-0ae0-4afe-ae55-96020910de1c" />


```sql
-- select name,city from customer where city =(select city from customer where id=3 ) or city=(select city from customer where id=7 );
```

**Output:**

<img width="504" alt="image" src="https://github.com/user-attachments/assets/17529b8b-f4ba-4f16-9735-75b183327a24" />

**Question 3**
---
<img width="912" alt="image" src="https://github.com/user-attachments/assets/58694ba7-f587-4950-911a-8a7ec38ad89b" />


```sql
-- select ord_no,purch_amt,ord_date,customer_id,Orders.salesman_id from Orders join Salesman ON Orders.salesman_id=Salesman.salesman_id where Salesman.city='London';
```

**Output:**

<img width="944" alt="image" src="https://github.com/user-attachments/assets/43fe27dc-c6b9-4691-98bd-dbcf6e7fcd63" />


**Question 4**
---
<img width="872" alt="image" src="https://github.com/user-attachments/assets/88662062-f1a3-46ff-8fdf-6677cc24b4cd" />



```sql
-- select sum(inventory) as total_available_amount from fruits where price > 0.5;


```

**Output:**

<img width="555" alt="image" src="https://github.com/user-attachments/assets/98712fb6-c9e9-4adb-8356-ca3899d657c2" />

**Question 5**
---
<img width="948" alt="image" src="https://github.com/user-attachments/assets/0359bd8e-e7ea-43dd-862b-91a47abf7845" />


```sql
-- select ord_no,purch_amt,ord_date,customer_id,salesman_id from ORDERS where purch_amt>(select avg(purch_amt) from ORDERS where ord_date='2012-10-10'); 
```

**Output:**

<img width="948" alt="image" src="https://github.com/user-attachments/assets/97b65fdd-7c76-4ba0-ae4a-1ebc04a6c660" />

**Question 6**
---
<img width="948" alt="image" src="https://github.com/user-attachments/assets/4102b80b-e803-424d-8ddf-dda614dea4f5" />


```sql
-- select ord_no,purch_amt,ord_date,customer_id,Orders.salesman_id from Orders join Salesman on Orders.salesman_id=Salesman.salesman_id where Salesman.salesman_id=(select salesman_id from Orders where customer_id='3007'); 
```

**Output:**

<img width="948" alt="image" src="https://github.com/user-attachments/assets/ac6f8f69-07cd-4134-99f7-7e042134746c" />


**Question 7**
---
<img width="913" alt="image" src="https://github.com/user-attachments/assets/99a76f79-783d-4c30-8009-48857e935bc6" />


```sql
-- select id,name,age,city, income from Employee where age<=35;

```

**Output:**

<img width="955" alt="image" src="https://github.com/user-attachments/assets/03d2d261-803b-429a-9870-55bd4b5a229f" />


**Question 8**
---
<img width="1021" alt="image" src="https://github.com/user-attachments/assets/49041de5-daf1-49fa-8d70-95fe4d272c21" />


```sql
-- select age, SUM(income) from employee group by age having SUM(income) > 1000000 order by age;
```

**Output:**

<img width="534" alt="image" src="https://github.com/user-attachments/assets/427b7191-57db-41ee-8df5-a7598b07f310" />

**Question 9**
---
<img width="1023" alt="image" src="https://github.com/user-attachments/assets/44d1ad11-fa2c-47fc-bd0d-3e45781a5857" />


```sql
-- select (age/5)*5 as age_group,MIN(age) from customer1 group by age_group HAVING MIN(age)<25;
```

**Output:**

<img width="554" alt="image" src="https://github.com/user-attachments/assets/fe28ef41-278f-4704-92b3-27f59c9bd4f7" />

**Question 10**
---
<img width="1011" alt="image" src="https://github.com/user-attachments/assets/91d4faef-0f28-4a7a-9eff-5d593488f930" />


```sql
-- select category_id,sum(price*category_id) as Revenue from products group by category_id having Revenue>25;
```

**Output:**

<img width="561" alt="image" src="https://github.com/user-attachments/assets/cdcdd5e9-eec8-4843-8543-2e4c51ccebed" />





## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
