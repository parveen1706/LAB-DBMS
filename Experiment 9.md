# Experiment 9: SQL Subqueries and Nested Queries

## Aim

To perform SQL queries using subqueries (nested queries) for advanced data retrieval.

---

## Theory

A **subquery** is a query inside another SQL query. It is used to perform operations that depend on the result of another query.

Types of subqueries:

* **Single-row subquery**: Returns one value
* **Multi-row subquery**: Returns multiple values
* **Correlated subquery**: Depends on outer query

Operators used with subqueries:

* **IN, ANY, ALL**
* **=, >, <**
* **EXISTS**

According to the lab program (page 8 of the uploaded file) , this experiment focuses on retrieving data using nested queries and comparisons.

---

## Question

Perform the following queries:

1. Display the employee who earns highest salary.
2. Display employee number and name of clerk with highest salary.
3. Display salesmen earning more than highest salary of any clerk.
4. Display clerks earning more than JAMES and less than SCOTT.
5. Display employees earning more than JAMES or SCOTT.
6. Display employees earning highest salary in each department.
7. Display employees earning highest salary in each job group.
8. Display employees working in ACCOUNTING department.
9. Display employees working in CHICAGO.
10. Display job groups having total salary greater than maximum salary of managers.

---

## Queries

### 1. Employee with highest salary

```sql id="a9b8c7"
SELECT ENAME, SAL FROM EMPLOYEE
WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE);
```

### 2. Highest paid clerk

```sql id="d6e5f4"
SELECT EMPNO, ENAME FROM EMPLOYEE
WHERE JOB = 'CLERK'
AND SAL = (SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = 'CLERK');
```

### 3. Salesmen earning more than any clerk

```sql id="g3h2i1"
SELECT ENAME FROM EMPLOYEE
WHERE JOB = 'SALESMAN'
AND SAL > (SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = 'CLERK');
```

### 4. Clerks earning between JAMES and SCOTT

```sql id="j0k9l8"
SELECT ENAME FROM EMPLOYEE
WHERE JOB = 'CLERK'
AND SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'JAMES')
AND SAL < (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'SCOTT');
```

### 5. Employees earning more than JAMES or SCOTT

```sql id="m7n6o5"
SELECT ENAME FROM EMPLOYEE
WHERE SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'JAMES')
OR SAL > (SELECT SAL FROM EMPLOYEE WHERE ENAME = 'SCOTT');
```

### 6. Highest salary in each department

```sql id="p4q3r2"
SELECT ENAME, SAL, DEPTNO FROM EMPLOYEE E
WHERE SAL = (
    SELECT MAX(SAL) FROM EMPLOYEE
    WHERE DEPTNO = E.DEPTNO
);
```

### 7. Highest salary in each job group

```sql id="s1t0u9"
SELECT ENAME, SAL, JOB FROM EMPLOYEE E
WHERE SAL = (
    SELECT MAX(SAL) FROM EMPLOYEE
    WHERE JOB = E.JOB
);
```

### 8. Employees in ACCOUNTING department

```sql id="v8w7x6"
SELECT ENAME FROM EMPLOYEE
WHERE DEPTNO = (
    SELECT DEPTNO FROM DEPARTMENT
    WHERE DNAME = 'ACCOUNTING'
);
```

### 9. Employees working in CHICAGO

```sql id="y5z4a3"
SELECT ENAME FROM EMPLOYEE
WHERE DEPTNO = (
    SELECT DEPTNO FROM DEPARTMENT
    WHERE LOC = 'CHICAGO'
);
```

### 10. Job groups with high total salary

```sql id="b2c1d0"
SELECT JOB, SUM(SAL) FROM EMPLOYEE
GROUP BY JOB
HAVING SUM(SAL) > (
    SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = 'MANAGER'
);
```

---

## Output

### Highest Salary

```text id="e9f8g7"
ENAME   SAL
-------------
KING    5000
```

### Highest Paid Clerk

```text id="h6i5j4"
EMPNO   ENAME
---------------
7934    MILLER
```

### Salesmen Output

```text id="k3l2m1"
ENAME
------
ALLEN
WARD
```

### Department-wise Highest Salary

```text id="n0o9p8"
ENAME   SAL   DEPTNO
----------------------
KING    5000  10
SCOTT   3000  20
BLAKE   2850  30
```

---

## Result

Successfully executed SQL subqueries and nested queries for advanced data retrieval and comparison.
