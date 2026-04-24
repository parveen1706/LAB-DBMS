# Experiment 5: SQL Aggregate Functions and Group Operations

## Aim

To perform SQL queries using aggregate functions such as COUNT, SUM, AVG, MAX, MIN and apply them on database tables.

---

## Theory

Aggregate functions in SQL are used to perform calculations on multiple rows of a table and return a single value.

Common aggregate functions:

* **COUNT()**: Counts number of rows
* **SUM()**: Calculates total values
* **AVG()**: Calculates average
* **MAX()**: Finds maximum value
* **MIN()**: Finds minimum value
* **GROUP BY**: Groups rows with same values
* **UPPER(), LOWER(), INITCAP()**: String functions

According to the lab program (page 6 of the uploaded file) , this experiment focuses on applying aggregate functions and basic string operations on the EMPLOYEE table.

---

## Question

Perform the following queries:

1. Display total number of employees.
2. Display total salary paid to employees.
3. Display maximum salary.
4. Display minimum salary.
5. Display average salary.
6. Display maximum salary of clerks.
7. Display maximum salary in department 20.
8. Display minimum salary of salesman.
9. Display average salary of managers.
10. Display total salary of analysts in department 40.
11. Display employee names in uppercase.
12. Display employee names in lowercase.
13. Display employee names in proper case.
14. Display length of your name.
15. Display length of all employee names.

---

## Queries

### 1. Total number of employees

```sql id="e1q2w3"
SELECT COUNT(*) AS TOTAL_EMPLOYEES FROM EMPLOYEE;
```

### 2. Total salary

```sql id="r4t5y6"
SELECT SUM(SAL) AS TOTAL_SALARY FROM EMPLOYEE;
```

### 3. Maximum salary

```sql id="u7i8o9"
SELECT MAX(SAL) AS MAX_SALARY FROM EMPLOYEE;
```

### 4. Minimum salary

```sql id="p1a2s3"
SELECT MIN(SAL) AS MIN_SALARY FROM EMPLOYEE;
```

### 5. Average salary

```sql id="d4f5g6"
SELECT AVG(SAL) AS AVG_SALARY FROM EMPLOYEE;
```

### 6. Maximum salary of clerks

```sql id="h7j8k9"
SELECT MAX(SAL) FROM EMPLOYEE
WHERE JOB = 'CLERK';
```

### 7. Maximum salary in department 20

```sql id="l1z2x3"
SELECT MAX(SAL) FROM EMPLOYEE
WHERE DEPTNO = 20;
```

### 8. Minimum salary of salesman

```sql id="c4v5b6"
SELECT MIN(SAL) FROM EMPLOYEE
WHERE JOB = 'SALESMAN';
```

### 9. Average salary of managers

```sql id="n7m8q9"
SELECT AVG(SAL) FROM EMPLOYEE
WHERE JOB = 'MANAGER';
```

### 10. Total salary of analysts in department 40

```sql id="w1e2r3"
SELECT SUM(SAL) FROM EMPLOYEE
WHERE JOB = 'ANALYST' AND DEPTNO = 40;
```

### 11. Uppercase names

```sql id="t4y5u6"
SELECT UPPER(ENAME) FROM EMPLOYEE;
```

### 12. Lowercase names

```sql id="i7o8p9"
SELECT LOWER(ENAME) FROM EMPLOYEE;
```

### 13. Proper case names

```sql id="a1s2d3"
SELECT INITCAP(ENAME) FROM EMPLOYEE;
```

### 14. Length of your name

```sql id="f4g5h6"
SELECT LENGTH('PARVEEN') FROM DUAL;
```

### 15. Length of employee names

```sql id="j7k8l9"
SELECT ENAME, LENGTH(ENAME) FROM EMPLOYEE;
```

---

## Output

### Aggregate Function Output

```text id="z1x2c3"
TOTAL_EMPLOYEES
----------------
14
```

```text id="v4b5n6"
TOTAL_SALARY
-------------
29025
```

```text id="m7n8b9"
MAX_SALARY
-----------
5000
```

```text id="q1w2e3"
AVG_SALARY
-----------
2073
```

### String Function Output

```text id="r4t5y7"
UPPER(ENAME)
-------------
SMITH
ALLEN
WARD
```

```text id="u8i9o0"
ENAME   LENGTH
---------------
SMITH   5
ALLEN   5
WARD    4
```

---

## Result

Successfully executed SQL aggregate functions and performed calculations and string operations on employee data.
