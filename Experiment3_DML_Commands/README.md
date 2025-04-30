# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
---
<img width="905" alt="image" src="https://github.com/user-attachments/assets/6e6fb64b-20c6-4213-a5cd-85dcbaf9a5c6" />


```sql
-- select InsuranceCompany,avg(-StartDate+EndDate) as AvgCoverageDurationDays from Insurance group by InsuranceCompany;
```

**Output:**

<img width="905" alt="image" src="https://github.com/user-attachments/assets/98c70812-607f-4123-a7ba-d1840d707ef2" />


**Question 2**
---
 <img width="504" alt="image" src="https://github.com/user-attachments/assets/964dfa6f-42b8-4342-a9d2-fde196e6a355" />


```sql
-- select date(AppointmentDateTime) as AppointmentDate,count(AppointmentDateTime) as TotalAppointments from Appointments group by AppointmentDateTime; 
```

**Output:**

<img width="677" alt="image" src="https://github.com/user-attachments/assets/9e118832-f286-430b-81e9-5efa4ec6c1aa" />


**Question 3**
---
<img width="814" alt="image" src="https://github.com/user-attachments/assets/ee59c27d-0acf-4847-bb2e-855c8c1f2941" />


```sql
-- select PatientID,count(Medications) as AvgMedications from MedicalRecords group by PatientId; 
```

**Output:**

<img width="541" alt="image" src="https://github.com/user-attachments/assets/3d88068d-477b-4ea0-ad75-e24103153dca" />


**Question 4**
---
<img width="541" alt="image" src="https://github.com/user-attachments/assets/c337fb32-1ee0-4b1c-ad0b-17c7ab3e548a" />


```sql
-- select max(purch_amt) as MAXIMUM from orders;
```

**Output:**

<img width="921" alt="image" src="https://github.com/user-attachments/assets/efe72bd8-b42c-4210-b41e-d96113c9708e" />



**Question 5**
---
<img width="643" alt="image" src="https://github.com/user-attachments/assets/65e3d525-e7c8-4817-b093-dff78d0de973" />


```sql
-- select count(name) as employees_count from employee;
```

**Output:**

<img width="476" alt="image" src="https://github.com/user-attachments/assets/2ba1bfab-3a4c-4622-b25f-f869f424ea87" />


**Question 6**
---
<img width="815" alt="image" src="https://github.com/user-attachments/assets/2eb98fc3-0097-47ac-914c-d707bded1518" />


```sql
-- select sum(inventory) as total_available_amount from fruits where price>0.5;
```

**Output:**

<img width="563" alt="image" src="https://github.com/user-attachments/assets/978056c6-7651-47ad-9392-c0baacfb0ca2" />


**Question 7**
---
<img width="804" alt="image" src="https://github.com/user-attachments/assets/43b80765-adf9-4bc8-a712-a212f48e6b89" />


```sql
-- select sum(purch_amt) as TOTAL from orders;
```

**Output:**

<img width="804" alt="image" src="https://github.com/user-attachments/assets/aaefe045-f176-47f6-86c0-307fab9c227a" />


**Question 8**
---
<img width="848" alt="image" src="https://github.com/user-attachments/assets/b2459566-efd5-41fc-b2f5-dff9e70d573b" />


```sql
-- select occupation,avg(workhour) as 'AVG(workhour)' from employee1 group by occupation having avg(workhour) between 10 and 12;
```

**Output:**

<img width="848" alt="image" src="https://github.com/user-attachments/assets/0aecd53e-8ee4-401f-bd40-8fc5702c6aee" />


**Question 9**
---
<img width="904" alt="image" src="https://github.com/user-attachments/assets/954c30d0-a2d4-4edf-bde9-60935a08737a" />


```sql
-- select jdate,min(workhour) as 'MIN(workhour)' from employee1 group by jdate having min(workhour)<10;
```

**Output:**

<img width="673" alt="image" src="https://github.com/user-attachments/assets/91d6b983-9a05-46f3-a445-86993a6fedef" />


**Question 10**
---
-- <img width="901" alt="image" src="https://github.com/user-attachments/assets/f57fe41e-f75d-40a3-847f-b594f6bab0e2" />


```sql
-- select (age/5)*5 as age_group,sum(salary) as 'SUM(salary)' from customer1 group by (age/5)*5 having sum(salary)>5000;
```

**Output:**

<img width="842" alt="image" src="https://github.com/user-attachments/assets/92678906-d499-451f-a0bc-7e4eef038db0" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
