# Experiment 7: PL/SQL – Variables, Control Structures and Loops

## AIM
To write and execute simple PL/SQL programs using variables, loops, and conditional statements.


## THEORY

PL/SQL, which stands for Procedural Language extensions to the Structured Query Language (SQL). It is a combination of SQL along with the procedural features of programming languages.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:
- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

# PL/SQL Programs – Steps and Expected Output

## 1. Write a PL/SQL program to find the Greatest of Two Numbers

### Steps:
- Declare two numeric variables and initialize them.
- Use an `IF` statement to compare the values.
- Display the greater number using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Greater number is: 80

## Program:

```
DECLARE
  num1 NUMBER := 70; 
  num2 NUMBER := 80;
BEGIN 
  IF num1>num2 then
    dbms_output.put_line('The greatest number is: ' || num1); 
  else
    dbms_output.put_line('The greatest number is: ' || num2); 
    
  end if;
END;
/

```
## Output:

<img width="578" alt="image" src="https://github.com/user-attachments/assets/f80d4119-0da0-467a-b24f-896df27beee0" />

---

## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

### Steps:
- Declare a variable `n` and assign a value (e.g., 10).
- Initialize a `sum` variable to 0.
- Use a `WHILE` loop to iterate from 1 to `n`, adding each number to the sum.
- Display the result using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Sum of first 10 natural numbers is: 55

## Program:

```

DECLARE
  n NUMBER :=10;
  sum NUMBER :=0;
  i NUMBER :=1;
BEGIN 
  while i<=n LOOP
    sum := sum+i;
    i :=i+1;
  end LOOP;
  DBMS_OUTPUT.PUT_LINE('The sum of first ' || n || ' natural numbers is: ' || sum);
  
END;
/

```

## Output:
<img width="578" alt="image" src="https://github.com/user-attachments/assets/f9db3789-530e-4b7f-9c2a-14a72e334b73" />


---

## 3. Write a PL/SQL program to generate Fibonacci series

### Steps:
- Declare the variable `n` to indicate how many terms to generate.
- Initialize the first two Fibonacci numbers (0 and 1).
- Use a loop to generate the next terms using the formula `c = a + b`.
- Print each term in the series.

**Expected Output:**  
n = 7  
Fibonacci sequence: 0, 1, 1, 2, 3, 5, 8

## Program:

```
DECLARE
  n NUMBER :=7;
  a NUMBER :=0;
  b NUMBER :=1;
  c NUMBER;        -- Next term
  i NUMBER := 1;
  
BEGIN 
   DBMS_OUTPUT.PUT_LINE('Fibonacci Series:');
   WHILE i <= n LOOP
      DBMS_OUTPUT.PUT_LINE(a);   -- Print current term
      
      c := a + b;                -- Calculate next term
      a := b;                    -- Shift values for next iteration
      b := c;
      
      i := i + 1;
   END LOOP;
   
END;
/

```

## Output:
<img width="578" alt="image" src="https://github.com/user-attachments/assets/8222854d-46a1-4f10-9db6-f8c532c62c7a" />


---

## 4. Write a PL/SQL Program to display the number in Reverse Order

### Steps:
- Declare a variable `n` and assign a value (e.g., 1535).
- Use a loop to extract each digit using modulo and reverse the number.
- Display the reversed number.

**Expected Output:**  
n = 1535  
Reversed number is 5351

## Program:

```
DECLARE
   n NUMBER := 1535;       -- Original number
   digit NUMBER;
   reversed NUMBER := 0;   -- To store the reversed number
   temp NUMBER;
BEGIN
   temp := n;  -- Store original number in a temporary variable
   
   WHILE temp > 0 LOOP
      digit := MOD(temp, 10);                 -- Extract last digit
      reversed := (reversed * 10) + digit;    -- Build reversed number
      temp := TRUNC(temp / 10);               -- Remove last digit
   END LOOP;
   
   DBMS_OUTPUT.PUT_LINE('Original Number: ' || n);
   DBMS_OUTPUT.PUT_LINE('Reversed Number: ' || reversed);
END;
/


```

## Output:
<img width="413" alt="image" src="https://github.com/user-attachments/assets/e6ff2aca-af94-4433-a6d9-bf6bfdfeb187" />


---

## 5. Write a PL/SQL program to find the largest of three numbers

### Steps:
- Declare three numeric variables `a`, `b`, and `c`.
- Use nested `IF-ELSIF-ELSE` conditions to find the largest among the three.
- Display the largest number.

**Expected Output:**  
a = 10, b = 9, c = 15  
Largest of three number is 15

## Program:

```
DECLARE
   a NUMBER := 10;
   b NUMBER := 9;
   c NUMBER := 15;
   largest NUMBER;
BEGIN
   IF a >= b AND a >= c THEN
      largest := a;
   ELSIF b >= a AND b >= c THEN
      largest := b;
   ELSE
      largest := c;
   END IF;

   DBMS_OUTPUT.PUT_LINE('a = ' || a || ', b = ' || b || ', c = ' || c);
   DBMS_OUTPUT.PUT_LINE('Largest of three numbers is ' || largest);
END;
/


```

## Output:
<img width="413" alt="image" src="https://github.com/user-attachments/assets/a1709484-9a9a-40ab-a565-74acd0a993fd" />


## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.
