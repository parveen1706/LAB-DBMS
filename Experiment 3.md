# Experiment 3: SQL Queries with Sorting, Pattern Matching and Calculations

## Aim

To perform SQL queries using ORDER BY, pattern matching (LIKE), logical conditions, and arithmetic operations on table data.

---

## Theory

SQL provides advanced features for organizing and filtering data:

* **ORDER BY**: Used to sort the result in ascending or descending order.
* **LIKE**: Used for pattern matching with wildcards (`%`, `_`).
* **IN / OR**: Used to match multiple values.
* **Arithmetic Operations**: Used to calculate values such as total salary.
* **IS NOT NULL**: Used to check non-null values.

According to the lab program (page 5–6 of the uploaded file) , this experiment focuses on sorting, filtering, and performing calculations on employee data.

---

## Question

Perform the following queries:

1. List employees and jobs in Department 30 in descending order of salary.
2. List job and department number of employees whose name has 5 letters, starts with 'A' and ends with 'N'.
3. Display employees whose names start with 'S'.
4. Display employees whose names end with 'S'.
5. Display employees working in departments 10, 20, 40 or working as clerk, salesman, analyst.
6. Display employee number and names for employees who earn commission.
7. Display employee number and total salary for each employee.

---

## Queries

### 1. Employees in Department 30 (Descending Salary)

```sql id="v3mf1x"
SELECT ENAME, JOB, SAL 
FROM EMPLOYEE
WHERE DEPTNO = 30
ORDER BY SAL DESC;
```

### 2. Name with 5 letters (A___N)

```sql id="1c6g9o"
SELECT JOB, DEPTNO 
FROM EMPLOYEE
WHERE ENAME LIKE 'A___N';
```

### 3. Names starting with 'S'

```sql id="3r9xg2"
SELECT ENAME 
FROM EMPLOYEE
WHERE ENAME LIKE 'S%';
```

### 4. Names ending with 'S'

```sql id="x8k2df"
SELECT ENAME 
FROM EMPLOYEE
WHERE ENAME LIKE '%S';
```

### 5. Employees in specific departments or jobs

```sql id="l2y3pq"
SELECT ENAME 
FROM EMPLOYEE
WHERE DEPTNO IN (10,20,40)
OR JOB IN ('CLERK','SALESMAN','ANALYST');
```

### 6. Employees earning commission

```sql id="7avk1d"
SELECT EMPNO, ENAME 
FROM EMPLOYEE
WHERE COMM IS NOT NULL;
```

### 7. Total salary of employees

```sql id="w2k9mz"
SELECT EMPNO, (SAL + NVL(COMM,0)) AS TOTAL_SALARY
FROM EMPLOYEE;
```

---

## Output

### Sorted Employees

```text id="c5r4az"
ENAME   JOB       SAL
----------------------
ALLEN   SALESMAN  1600
WARD    SALESMAN  1250
MARTIN  SALESMAN  1250
```

### Pattern Matching Output

```text id="x7m1np"
ENAME
------
SMITH
SCOTT
```

```text id="z2p8ru"
ENAME
------
JAMES
```

### Employees with Commission

```text id="f6y3rt"
EMPNO   ENAME
--------------
7499    ALLEN
7521    WARD
7654    MARTIN
```

### Total Salary Calculation

```text id="k4n2ls"
EMPNO   TOTAL_SALARY
----------------------
7499    1900
7521    1550
7654    2650
```

---

## Result

Successfully performed SQL queries using sorting, pattern matching, logical conditions, and arithmetic operations on employee data.
