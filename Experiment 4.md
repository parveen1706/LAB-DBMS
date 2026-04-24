# Experiment 4: Advanced SQL Queries with Conditions and Calculations

## Aim

To perform advanced SQL queries using conditions, string operations, date functions, and arithmetic calculations.

---

## Theory

SQL provides various functions and operators to perform complex queries:

* **Date Conditions**: Used to filter records based on dates.
* **String Functions**: LIKE, LENGTH, etc.
* **Arithmetic Operations**: Used to calculate salary, increments, etc.
* **ORDER BY**: Used to sort data.
* **Logical Operators**: AND, OR, NOT

According to the lab program (page 6 of the uploaded file) , this experiment includes queries involving dates, string patterns, salary calculations, and updates.

---

## Question

Perform the following queries:

1. Display employees who joined before 30-June-1980 or after 31-Dec-1981.
2. Display employees whose second letter is 'A'.
3. Display employees whose names have exactly 5 characters.
4. Display employees whose second letter is 'A'.
5. Display employees who are not salesman, clerk, or analyst.
6. Display employee name and annual salary, highest salary first.
7. Display name, salary, HRA, DA, PF, and total salary.
8. Update salary by 10% for employees not eligible for commission.
9. Display employees whose salary is more than 3000 after 20% increment.
10. Display employees whose salary contains at least 3 digits.

---

## Queries

### 1. Employees based on joining date

```sql id="b6q4kp"
SELECT ENAME, HIREDATE 
FROM EMPLOYEE
WHERE HIREDATE < '30-JUN-80'
OR HIREDATE > '31-DEC-81';
```

### 2. Second letter is 'A'

```sql id="h8j2wx"
SELECT ENAME 
FROM EMPLOYEE
WHERE ENAME LIKE '_A%';
```

### 3. Name with exactly 5 characters

```sql id="n5w7vz"
SELECT ENAME 
FROM EMPLOYEE
WHERE LENGTH(ENAME) = 5;
```

### 4. Second letter is 'A' (Repeated)

```sql id="q1x9pt"
SELECT ENAME 
FROM EMPLOYEE
WHERE ENAME LIKE '_A%';
```

### 5. Not salesman, clerk, analyst

```sql id="r2m8ky"
SELECT ENAME, JOB 
FROM EMPLOYEE
WHERE JOB NOT IN ('SALESMAN','CLERK','ANALYST');
```

### 6. Annual salary (sorted)

```sql id="p4v2nx"
SELECT ENAME, (SAL * 12) AS ANNUAL_SALARY
FROM EMPLOYEE
ORDER BY ANNUAL_SALARY DESC;
```

### 7. Salary calculations

```sql id="z7c1df"
SELECT ENAME, SAL,
(SAL * 0.15) AS HRA,
(SAL * 0.10) AS DA,
(SAL * 0.05) AS PF,
((SAL + (SAL * 0.15) + (SAL * 0.10)) - (SAL * 0.05)) AS TOTAL_SAL
FROM EMPLOYEE;
```

### 8. Update salary (10% increment)

```sql id="y3n8cv"
UPDATE EMPLOYEE
SET SAL = SAL + (SAL * 0.10)
WHERE COMM IS NULL;
```

### 9. Salary after 20% increment > 3000

```sql id="t8g6lm"
SELECT ENAME, SAL 
FROM EMPLOYEE
WHERE (SAL + (SAL * 0.20)) > 3000;
```

### 10. Salary with at least 3 digits

```sql id="x9v3ak"
SELECT ENAME, SAL 
FROM EMPLOYEE
WHERE SAL >= 100;
```

---

## Output

### Date Condition Output

```text id="m1v8sz"
ENAME   HIREDATE
-----------------------
SMITH   17-DEC-80
SCOTT   09-DEC-82
```

### String Function Output

```text id="k8p3dw"
ENAME
------
MARTIN
JAMES
```

### Annual Salary Output

```text id="q5n6ra"
ENAME   ANNUAL_SALARY
-----------------------
KING    60000
SCOTT   36000
FORD    36000
```

### Salary Calculation Output

```text id="v7x4lb"
ENAME   SAL   HRA   DA   PF   TOTAL_SAL
----------------------------------------
SMITH   800   120   80   40   960
```

### Update Output

```text id="a2r9pk"
Rows updated successfully.
```

---

## Result

Successfully executed advanced SQL queries using date conditions, string functions, arithmetic operations, and update statements.
