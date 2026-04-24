# Experiment 2: SQL Queries for Retrieving Data

## Aim

To perform retrieval operations on a database using SQL queries such as SELECT, DISTINCT, WHERE, and logical operators.

---

## Theory

SQL provides powerful commands to retrieve data from databases. The **SELECT** statement is used to fetch data from one or more tables.

Important concepts used in this experiment:

* **SELECT**: Retrieves data from a table
* **DISTINCT**: Removes duplicate values
* **WHERE**: Filters records based on conditions
* **Logical Operators**: AND, OR, NOT
* **Comparison Operators**: =, >, <, BETWEEN, IN

As per the lab program (page 5 of the uploaded file) , this experiment focuses on retrieving specific data from the EMPLOYEE table using different conditions.

---

## Question

Perform the following queries using EMPLOYEE table:

1. List all distinct jobs in Employee.
2. List all information about employees in Department 30.
3. Find department numbers with names greater than 20.
4. Find all managers and clerks in department 30.
5. List employee name, number, and department of all clerks.
6. Find managers not in department 30.
7. List employees in department 10 who are not managers or clerks.
8. Find employees earning between 1200 and 1400.
9. List employees who are clerks, analysts, or salesmen.
10. List employees whose names begin with 'M'.

---

## Queries

### 1. List all distinct jobs

```sql
SELECT DISTINCT JOB FROM EMPLOYEE;
```

### 2. Employees in Department 30

```sql
SELECT * FROM EMPLOYEE
WHERE DEPTNO = 30;
```

### 3. Department number with names greater than 20

```sql
SELECT DEPTNO, DNAME FROM DEPARTMENT
WHERE DEPTNO > 20;
```

### 4. Managers and Clerks in Department 30

```sql
SELECT * FROM EMPLOYEE
WHERE DEPTNO = 30
AND (JOB = 'MANAGER' OR JOB = 'CLERK');
```

### 5. Clerk details

```sql
SELECT ENAME, EMPNO, DEPTNO FROM EMPLOYEE
WHERE JOB = 'CLERK';
```

### 6. Managers not in Department 30

```sql
SELECT * FROM EMPLOYEE
WHERE JOB = 'MANAGER' AND DEPTNO <> 30;
```

### 7. Employees in Department 10 (not manager or clerk)

```sql
SELECT * FROM EMPLOYEE
WHERE DEPTNO = 10
AND JOB NOT IN ('MANAGER', 'CLERK');
```

### 8. Employees earning between 1200 and 1400

```sql
SELECT ENAME, JOB FROM EMPLOYEE
WHERE SAL BETWEEN 1200 AND 1400;
```

### 9. Clerks, Analysts, Salesmen

```sql
SELECT ENAME, DEPTNO FROM EMPLOYEE
WHERE JOB IN ('CLERK', 'ANALYST', 'SALESMAN');
```

### 10. Names starting with 'M'

```sql
SELECT ENAME, DEPTNO FROM EMPLOYEE
WHERE ENAME LIKE 'M%';
```

---

## Output

### Sample Outputs

```text
JOB
------
CLERK
SALESMAN
MANAGER
ANALYST
PRESIDENT
```

```text
ENAME   EMPNO   DEPTNO
----------------------
SMITH   7369    20
ALLEN   7499    30
```

```text
ENAME   JOB       SAL
----------------------
WARD    SALESMAN  1250
MARTIN  SALESMAN  1250
```

```text
ENAME   DEPTNO
---------------
MARTIN  30
MILLER  10
```

---

## Result

Successfully executed SQL SELECT queries to retrieve and filter data using various conditions and operators.
