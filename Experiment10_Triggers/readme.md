# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
**Steps:**
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.

**Expected Output:**
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.

---
## Program:

```
-- Enable output for DBMS_OUTPUT
SET SERVEROUTPUT ON;

-- Step 1: Drop the employees table if it already exists
DROP TABLE employees CASCADE CONSTRAINTS;

-- Step 2: Create the employees table
CREATE TABLE employees (
    emp_id     NUMBER PRIMARY KEY,  -- Employee ID
    emp_name   VARCHAR2(100),       -- Employee Name
    emp_dept   VARCHAR2(50)         -- Employee Department (Ensure the name is correct)
);

-- Step 3: Create the employee_log table to store logs
CREATE TABLE employee_log (
    log_id     NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,  -- Log ID (Auto-incremented)
    emp_id     NUMBER,                                            -- Employee ID
    emp_name   VARCHAR2(100),                                     -- Employee Name
    emp_dept   VARCHAR2(50),                                      -- Employee Department
    log_date   DATE DEFAULT SYSDATE                               -- Log date (default is current date and time)
);

-- Step 4: Create the AFTER INSERT trigger to log new employee data
CREATE OR REPLACE TRIGGER trg_log_employee_insert
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
    -- Insert the new employee's data into the employee_log table
    INSERT INTO employee_log (emp_id, emp_name, emp_dept)
    VALUES (:NEW.emp_id, :NEW.emp_name, :NEW.emp_dept);
END;
/

-- Step 5: Insert a new employee record
INSERT INTO employees (emp_id, emp_name, emp_dept)
VALUES (101, 'Alice Johnson', 'IT');

-- Step 6: Query the employee_log table to verify the log entry
SELECT * FROM employee_log;

```
## Output:
<img width="725" alt="image" src="https://github.com/user-attachments/assets/943f7b78-942d-41d1-9e04-1d466cb32b50" />


## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

**Expected Output:**
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`

---
## Program:

```
-- Step 1: Create the sensitive_data table
CREATE TABLE sensitive_data (
    id          NUMBER PRIMARY KEY,  -- Record ID
    name        VARCHAR2(100),       -- Name
    description VARCHAR2(255)        -- Description of the sensitive data
);

-- Step 2: Insert some sample data into sensitive_data table
INSERT INTO sensitive_data (id, name, description) 
VALUES (1, 'Top Secret', 'Highly sensitive information');
INSERT INTO sensitive_data (id, name, description) 
VALUES (2, 'Confidential', 'Sensitive government data');
COMMIT;

-- Step 3: Create the BEFORE DELETE trigger to prevent deletion
CREATE OR REPLACE TRIGGER trg_prevent_delete
BEFORE DELETE ON sensitive_data
FOR EACH ROW
BEGIN
    -- Raise an application error to prevent deletion
    RAISE_APPLICATION_ERROR(-20001, 'ERROR: Deletion not allowed on this table.');
END;
/

-- Step 4: Try to delete a record from the sensitive_data table (this will fail)
-- This statement should raise the error defined in the trigger
DELETE FROM sensitive_data WHERE id = 1;

```

## Output:

<img width="725" alt="image" src="https://github.com/user-attachments/assets/ead3cbd6-02b1-4e59-971a-c27294b3fd00" />


## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

**Expected Output:**
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.

---
## Program:

```
-- Step 1: Create the products table with a last_modified column
CREATE TABLE products (
    product_id   NUMBER PRIMARY KEY,
    product_name VARCHAR2(100),
    price        NUMBER,
    last_modified TIMESTAMP
);

-- Step 2: Insert some sample data into the products table
INSERT INTO products (product_id, product_name, price) 
VALUES (1, 'Product A', 100);
INSERT INTO products (product_id, product_name, price) 
VALUES (2, 'Product B', 200);
COMMIT;

-- Step 3: Create the BEFORE UPDATE trigger to automatically update the last_modified timestamp
CREATE OR REPLACE TRIGGER trg_update_last_modified
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
    -- Set the last_modified column to the current timestamp whenever a record is updated
    :NEW.last_modified := CURRENT_TIMESTAMP;
END;
/

-- Step 4: Update a product record to test the trigger
UPDATE products 
SET price = 120
WHERE product_id = 1;

-- Step 5: Verify the update and check the last_modified column
SELECT * FROM products;

```
## Output:
<img width="725" alt="image" src="https://github.com/user-attachments/assets/074cb707-2fad-4fac-a3ae-a02d4dcf877f" />



## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

**Expected Output:**
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.

---
## Program:

```
-- Step 1: Create the audit_log table to store the update count
CREATE TABLE audit_log (
    table_name VARCHAR2(50),
    update_count NUMBER
);

-- Step 2: Insert an initial record in the audit_log table to track updates for the customer_orders table
INSERT INTO audit_log (table_name, update_count)
VALUES ('customer_orders', 0);
COMMIT;

-- Step 3: Create the customer_orders table for testing the trigger
CREATE TABLE customer_orders (
    order_id NUMBER PRIMARY KEY,
    customer_id NUMBER,
    order_amount NUMBER,
    order_date DATE
);

-- Step 4: Insert some sample data into the customer_orders table
INSERT INTO customer_orders (order_id, customer_id, order_amount, order_date)
VALUES (1, 101, 500, SYSDATE);
INSERT INTO customer_orders (order_id, customer_id, order_amount, order_date)
VALUES (2, 102, 300, SYSDATE);
COMMIT;

-- Step 5: Create the AFTER UPDATE trigger to track updates on the customer_orders table
CREATE OR REPLACE TRIGGER trg_update_count
AFTER UPDATE ON customer_orders
FOR EACH ROW
BEGIN
    -- Increment the update count for the customer_orders table in the audit_log
    UPDATE audit_log
    SET update_count = update_count + 1
    WHERE table_name = 'customer_orders';
END;
/

-- Step 6: Update a record in the customer_orders table to test the trigger
UPDATE customer_orders
SET order_amount = 550
WHERE order_id = 1;

-- Step 7: Verify the update in the audit_log table
SELECT * FROM audit_log;

```

## Output:
<img width="725" alt="image" src="https://github.com/user-attachments/assets/c326fb4c-1d9f-41fd-9ecc-1a06096bb6d7" />



## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

**Expected Output:**
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`

## Program:

```
-- Step 1: Add the salary column to the employees table
ALTER TABLE employees ADD (salary NUMBER);

-- Step 2: Create the BEFORE INSERT trigger to check the salary condition
CREATE OR REPLACE TRIGGER trg_check_salary
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
    -- Check if the salary is below 3000
    IF :NEW.salary < 3000 THEN
        -- Raise an error if salary is below the threshold
        RAISE_APPLICATION_ERROR(-20001, 'ERROR: Salary below minimum threshold.');
    END IF;
END;
/

-- Step 3: Insert data into the employees table to test the trigger
-- This insert should succeed (salary is 3500, which is above 3000)
INSERT INTO employees (emp_id, emp_name, salary) 
VALUES (101, 'Alice Johnson', 3500);

-- This insert should fail (salary is 2500, which is below 3000)
INSERT INTO employees (emp_id, emp_name, salary) 
VALUES (102, 'Bob Smith', 2500);

-- Step 4: Verify the results by selecting the data in the employees table
SELECT * FROM employees;

```
## Output:
<img width="725" alt="image" src="https://github.com/user-attachments/assets/9b6944a2-f3ab-40aa-8841-fe28dff2909a" />



## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.
