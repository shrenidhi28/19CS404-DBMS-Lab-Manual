# Experiment 9: PL/SQL – Procedures and Functions

## AIM
To understand and implement procedures and functions in PL/SQL for performing various operations such as calculations, decision-making, and looping.

---

## THEORY

PL/SQL (Procedural Language/SQL) extends SQL by adding procedural constructs like variables, conditions, loops, procedures, and functions. Procedures and functions are subprograms that help modularize the code and improve reusability.

### **Procedure**
A PL/SQL **procedure** is a subprogram that performs a specific action. It does not return a value directly but can return values using `OUT` parameters.

**Syntax:**
```sql
CREATE OR REPLACE PROCEDURE procedure_name (parameters)
IS
BEGIN
   -- statements
END;
```

To call the procedure

```sql
EXEC procedure_name(arguments);
```

### **Function**
A PL/SQL **function** is a subprogram that returns a single value using the RETURN keyword.

```sql
CREATE OR REPLACE FUNCTION function_name (parameters)
RETURN datatype
IS
BEGIN
   -- statements
   RETURN value;
END;
```

To call the function:

```sql
SELECT function_name(arguments) FROM DUAL;
```

Key Differences:

-A procedure does not return a value, whereas a function must return a value.
-Functions can be called from SQL queries, procedures cannot (in most cases).

## 1. Write a PL/SQL Procedure to Find the Square of a Number

### Steps:
- Create a procedure named `find_square`.
- Declare a parameter to accept a number.
- Inside the procedure, compute the square of the input number.
- Use `DBMS_OUTPUT.PUT_LINE` to display the result.
- Call the procedure with a number as input.

**Expected Output:**  
Square of 6 is 36

---
## Program:

```
-- Enable output display
SET SERVEROUTPUT ON;

-- Create the procedure
CREATE OR REPLACE PROCEDURE find_square(p_number IN NUMBER) AS
    v_square NUMBER;
BEGIN
    v_square := p_number * p_number;
    DBMS_OUTPUT.PUT_LINE('Square of ' || p_number || ' is ' || v_square);
END;
/

-- Call the procedure with input value 6
BEGIN
    find_square(6);
END;
/

```
## Output:
<img width="725" alt="image" src="https://github.com/user-attachments/assets/6bfa3909-fde8-429b-a364-d121f29c67d2" />


## 2. Write a PL/SQL Function to Return the Factorial of a Number

### Steps:
- Create a function named `get_factorial`.
- Declare a parameter to accept a number.
- Use a loop to calculate the factorial.
- Return the result using the `RETURN` statement.
- Call the function using a `SELECT` statement or in an anonymous block.

**Expected Output:**  
Factorial of 5 is 120


---
## Program:

```
-- Enable output
SET SERVEROUTPUT ON;

-- Create the function
CREATE OR REPLACE FUNCTION get_factorial(p_number IN NUMBER) RETURN NUMBER IS
    v_fact NUMBER := 1;
    v_counter NUMBER;
BEGIN
    IF p_number < 0 THEN
        RETURN NULL;  -- Factorial is not defined for negative numbers
    END IF;

    FOR v_counter IN 1 .. p_number LOOP
        v_fact := v_fact * v_counter;
    END LOOP;

    RETURN v_fact;
END;
/

-- Call the function and display the result
BEGIN
    DBMS_OUTPUT.PUT_LINE('Factorial of 5 is ' || get_factorial(5));
END;
/

```
## Output:
<img width="725" alt="image" src="https://github.com/user-attachments/assets/1a920ae0-610d-47e8-bef5-d9d2b1c85dde" />



## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

### Steps:
- Create a procedure named `check_even_odd`.
- Accept an input parameter.
- Use the `MOD` function to check if the number is divisible by 2.
- Display whether it is Even or Odd using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
12 is Even

---
## Program:

```
-- Enable output
SET SERVEROUTPUT ON;

-- Create the procedure
CREATE OR REPLACE PROCEDURE check_even_odd(p_number IN NUMBER) AS
BEGIN
    IF MOD(p_number, 2) = 0 THEN
        DBMS_OUTPUT.PUT_LINE(p_number || ' is Even');
    ELSE
        DBMS_OUTPUT.PUT_LINE(p_number || ' is Odd');
    END IF;
END;
/

-- Call the procedure with an example number
BEGIN
    check_even_odd(12);
END;
/


```
## Output:
<img width="725" alt="image" src="https://github.com/user-attachments/assets/88b1a4ba-5ce3-42d7-b3dc-2243d6b56601" />


## 4. Write a PL/SQL Function to Return the Reverse of a Number

### Steps:
- Create a function named `reverse_number`.
- Accept an input number as parameter.
- Use a loop to reverse the digits of the number.
- Return the reversed number.
- Call the function and display the output.

**Expected Output:**  
Reversed number of 1234 is 4321

---
## Program:

```
-- Enable output
SET SERVEROUTPUT ON;

-- Create the function
CREATE OR REPLACE FUNCTION reverse_number(p_number IN NUMBER) RETURN NUMBER IS
    v_input     NUMBER := p_number;
    v_reversed  NUMBER := 0;
    v_digit     NUMBER;
BEGIN
    WHILE v_input > 0 LOOP
        v_digit := MOD(v_input, 10);               -- Get the last digit
        v_reversed := (v_reversed * 10) + v_digit; -- Append digit
        v_input := TRUNC(v_input / 10);            -- Remove last digit
    END LOOP;

    RETURN v_reversed;
END;
/

-- Call the function and display the output
BEGIN
    DBMS_OUTPUT.PUT_LINE('Reversed number of 1234 is ' || reverse_number(1234));
END;
/

```
## Output:
<img width="725" alt="image" src="https://github.com/user-attachments/assets/6dac7f9f-8594-42d1-bc64-0e0969b2939d" />


## 5. Write a PL/SQL Procedure to Display the Multiplication Table of a Number

### Steps:
- Create a procedure named `print_table`.
- Accept an input number.
- Use a loop from 1 to 10 to multiply the input number.
- Display the multiplication results using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Multiplication table of 5:  
5 x 1 = 5  
5 x 2 = 10  
5 x 3 = 15  
...  
5 x 10 = 50

## Program:

```
-- Enable output
SET SERVEROUTPUT ON;

-- Step 1: Create the employees table
CREATE TABLE employees (
    emp_id     NUMBER PRIMARY KEY,
    emp_name   VARCHAR2(100),
    emp_dept   VARCHAR2(50)
);

-- Step 2: Create the employee_log table
CREATE TABLE employee_log (
    log_id     NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    emp_id     NUMBER,
    emp_name   VARCHAR2(100),
    emp_dept   VARCHAR2(50),
    log_date   DATE DEFAULT SYSDATE
);

-- Step 3: Create the AFTER INSERT trigger
CREATE OR REPLACE TRIGGER trg_log_employee_insert
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
    INSERT INTO employee_log (emp_id, emp_name, emp_dept)
    VALUES (:NEW.emp_id, :NEW.emp_name, :NEW.emp_dept);
END;
/

```
## Output:
<img width="725" alt="image" src="https://github.com/user-attachments/assets/17fdea50-af9c-402f-b658-dd8cc0c9cafc" />


## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.
