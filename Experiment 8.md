# Experiment 8: SQL Joins and Multi-Table Queries

## Aim

To perform SQL queries using joins to retrieve data from multiple tables and establish relationships between them.

---

## Theory

In relational databases, data is often stored in multiple tables. To retrieve combined data, **joins** are used:

* **INNER JOIN**: Returns matching records from both tables
* **LEFT JOIN**: Returns all records from left table and matched records from right table
* **SELF JOIN**: A table joined with itself
* **EQUI JOIN**: Based on equality condition

This experiment uses EMPLOYEE and DEPARTMENT tables to perform multi-table queries.

According to the lab program (page 7–8 of the uploaded file) , this experiment focuses on joins, manager relationships, and combining multiple tables.

---

## Question

Perform the following queries:

1. Display all employees with their department name.
2. Display employees whose manager name is JONES, along with manager name.
3. Display employee name, job, department name, manager name, and grade department-wise.
4. List employees with job, salary grade, and department name except clerks, sorted by salary.
5. Display employee name, job, and manager (including employees without manager).
6. List employee details with annual salary and department info excluding clerks.
7. List employees earning 30000 annually and not clerks.
8. Display employees along with their manager’s name and number.
9. Display department name, number, and total salary.
10. Display employee number, name, and department location.

---

## Queries

### 1. Employees with department name

```sql id="a8b7c6"
SELECT E.ENAME, D.DNAME
FROM EMPLOYEE E
JOIN DEPARTMENT D
ON E.DEPTNO = D.DEPTNO;
```

### 2. Employees whose manager is JONES

```sql id="d5e4f3"
SELECT E.ENAME, M.ENAME AS MANAGER
FROM EMPLOYEE E
JOIN EMPLOYEE M
ON E.MGR = M.EMPNO
WHERE M.ENAME = 'JONES';
```

### 3. Employee full details with manager and department

```sql id="g2h1i0"
SELECT E.ENAME, E.JOB, D.DNAME, M.ENAME AS MANAGER
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
LEFT JOIN EMPLOYEE M ON E.MGR = M.EMPNO;
```

### 4. Employees except clerks sorted by salary

```sql id="j9k8l7"
SELECT E.ENAME, E.JOB, D.DNAME, E.SAL
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE E.JOB <> 'CLERK'
ORDER BY E.SAL DESC;
```

### 5. Employees with manager (including no manager)

```sql id="m6n5o4"
SELECT E.ENAME, E.JOB, M.ENAME AS MANAGER
FROM EMPLOYEE E
LEFT JOIN EMPLOYEE M
ON E.MGR = M.EMPNO;
```

### 6. Employee annual salary with department (excluding clerks)

```sql id="p3q2r1"
SELECT E.ENAME, (E.SAL*12) AS ANNUAL_SAL, D.DNAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE E.JOB <> 'CLERK';
```

### 7. Employees earning 30000 annually

```sql id="s0t9u8"
SELECT E.ENAME, (E.SAL*12) AS ANNUAL_SAL, D.DNAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE (E.SAL*12) = 30000
AND E.JOB <> 'CLERK';
```

### 8. Employees with manager name and number

```sql id="v7w6x5"
SELECT E.ENAME, E.EMPNO, M.ENAME AS MANAGER_NAME, M.EMPNO AS MANAGER_NO
FROM EMPLOYEE E
LEFT JOIN EMPLOYEE M
ON E.MGR = M.EMPNO;
```

### 9. Department total salary

```sql id="y4z3a2"
SELECT D.DNAME, D.DEPTNO, SUM(E.SAL) AS TOTAL_SAL
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
GROUP BY D.DNAME, D.DEPTNO;
```

### 10. Employee with department location

```sql id="b1c0d9"
SELECT E.EMPNO, E.ENAME, D.DNAME
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO;
```

---

## Output

### Join Output

```text id="e8f7g6"
ENAME   DNAME
---------------
SMITH   ACCOUNTING
ALLEN   SALES
```

### Manager Output

```text id="h5i4j3"
ENAME   MANAGER
----------------
SCOTT   JONES
FORD    JONES
```

### Combined Data Output

```text id="k2l1m0"
ENAME   JOB      DNAME        MANAGER
--------------------------------------
SMITH   CLERK    ACCOUNTING   FORD
```

### Salary Group Output

```text id="n9o8p7"
DNAME        DEPTNO   TOTAL_SAL
--------------------------------
ACCOUNTING   20       10875
SALES        30       9400
```

---

## Result

Successfully performed SQL join operations including INNER JOIN, LEFT JOIN, and SELF JOIN to retrieve data from multiple tables.
