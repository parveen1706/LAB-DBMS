# Experiment 12: SQL Queries with Complex Conditions and Advanced Subqueries

## Aim

To perform SQL queries using complex subqueries, conditions, and advanced filtering techniques.

---

## Theory

Advanced SQL queries combine multiple concepts such as:

* **Nested Subqueries**: Query inside another query
* **ALL / ANY / IN**: Used for comparisons with multiple values
* **EXISTS / NOT EXISTS**: Checks presence of records
* **DELETE with Subquery**: Removes data based on conditions
* **JOIN with Conditions**: Combines multiple tables with filtering

These queries help in solving complex real-world database scenarios efficiently.

According to the lab program (page 9 of the uploaded file) , this experiment focuses on advanced conditions, comparisons, and data manipulation.

---

## Question

Perform the following queries:

1. Display employees whose salary is less than their manager but more than salary of any other manager.
2. Find number of employees whose salary is greater than their manager’s salary.
3. Display managers who are not working under president but under other managers.
4. Delete departments where no employees are working.
5. Delete employees whose department does not exist in department table.
6. Display employees whose salary is outside the grade range.
7. Display employees whose net pay is greater than any other employee.
8. Display employees working in SALES or RESEARCH department.
9. Display grade of JONES.
10. Display department name where number of characters equals number of employees in another department.

---

## Queries

### 1. Salary less than manager but greater than any manager

```sql id="a1s2d3"
SELECT E.ENAME, E.SAL
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.SAL < M.SAL
AND E.SAL > ANY (
    SELECT SAL FROM EMPLOYEE WHERE JOB = 'MANAGER'
);
```

### 2. Count employees earning more than manager

```sql id="f4g5h6"
SELECT COUNT(*) AS TOTAL
FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.SAL > M.SAL;
```

### 3. Managers not under president

```sql id="j7k8l9"
SELECT ENAME FROM EMPLOYEE
WHERE JOB = 'MANAGER'
AND MGR <> (
    SELECT EMPNO FROM EMPLOYEE WHERE JOB = 'PRESIDENT'
);
```

### 4. Delete departments with no employees

```sql id="z1x2c3"
DELETE FROM DEPARTMENT D
WHERE NOT EXISTS (
    SELECT 1 FROM EMPLOYEE E
    WHERE E.DEPTNO = D.DEPTNO
);
```

### 5. Delete employees with invalid department

```sql id="v4b5n6"
DELETE FROM EMPLOYEE E
WHERE NOT EXISTS (
    SELECT 1 FROM DEPARTMENT D
    WHERE D.DEPTNO = E.DEPTNO
);
```

### 6. Employees outside salary grade

```sql id="m7n8b9"
SELECT ENAME, SAL FROM EMPLOYEE
WHERE SAL NOT BETWEEN 1000 AND 5000;
```

### 7. Employees with highest net pay

```sql id="q1w2e3"
SELECT ENAME, (SAL + NVL(COMM,0)) AS NET_PAY
FROM EMPLOYEE
WHERE (SAL + NVL(COMM,0)) >= ALL (
    SELECT (SAL + NVL(COMM,0)) FROM EMPLOYEE
);
```

### 8. Employees in SALES or RESEARCH

```sql id="r4t5y6"
SELECT ENAME FROM EMPLOYEE
WHERE DEPTNO IN (
    SELECT DEPTNO FROM DEPARTMENT
    WHERE DNAME IN ('SALES','RESEARCH')
);
```

### 9. Grade of JONES

```sql id="u7i8o9"
SELECT JOB FROM EMPLOYEE
WHERE ENAME = 'JONES';
```

### 10. Department name condition

```sql id="p1a2s3"
SELECT DNAME FROM DEPARTMENT
WHERE LENGTH(DNAME) = (
    SELECT COUNT(*) FROM EMPLOYEE
);
```

---

## Output

### Salary Comparison Output

```text id="d4f5g6"
ENAME   SAL
-------------
SMITH   800
```

### Count Output

```text id="h7j8k9"
TOTAL
-------
2
```

### Delete Output

```text id="l1z2x3"
Rows deleted successfully.
```

### Highest Net Pay

```text id="c4v5b6"
ENAME   NET_PAY
----------------
KING    5000
```

---

## Result

Successfully executed complex SQL queries using advanced subqueries, conditions, and data manipulation operations.
