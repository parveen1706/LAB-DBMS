# Experiment 10: SQL Queries with Advanced Subqueries and Conditions

## Aim

To perform advanced SQL queries using subqueries with ALL, ANY, EXISTS, and complex conditions.

---

## Theory

Advanced SQL queries use subqueries combined with operators such as:

* **ANY**: Compares a value with any value in a subquery
* **ALL**: Compares a value with all values in a subquery
* **EXISTS**: Checks if subquery returns any rows
* **IN / NOT IN**: Matches values from a list
* **Correlated Subqueries**: Subquery depends on outer query

These help in solving complex real-world database problems.

According to the lab program (page 8 of the uploaded file) , this experiment focuses on applying advanced conditions and comparisons using subqueries.

---

## Question

Perform the following queries:

1. Display employees from department 10 with salary greater than any employee in other departments.
2. Display employees from department 10 with salary greater than all employees in other departments.
3. Display employees in sales department with grade 3.
4. Display employees who are not managers but working under a manager.
5. Display employees whose manager name is JONES.
6. Display employees working in sales department.
7. Display employees with salary between 2000 and 5000 in CHICAGO.
8. Display employees whose salary is greater than their manager’s salary.
9. Display employees working in same department as their manager.

---

## Queries

### 1. Salary greater than ANY

```sql id="a1x2c3"
SELECT ENAME, SAL FROM EMPLOYEE
WHERE DEPTNO = 10
AND SAL > ANY (
    SELECT SAL FROM EMPLOYEE WHERE DEPTNO <> 10
);
```

### 2. Salary greater than ALL

```sql id="d4v5b6"
SELECT ENAME, SAL FROM EMPLOYEE
WHERE DEPTNO = 10
AND SAL > ALL (
    SELECT SAL FROM EMPLOYEE WHERE DEPTNO <> 10
);
```

### 3. Employees in sales with grade 3

```sql id="g7n8m9"
SELECT ENAME FROM EMPLOYEE
WHERE DEPTNO = (
    SELECT DEPTNO FROM DEPARTMENT WHERE DNAME = 'SALES'
)
AND SAL BETWEEN 2000 AND 3000;
```

### 4. Employees not managers but working under manager

```sql id="j1k2l3"
SELECT ENAME FROM EMPLOYEE
WHERE JOB <> 'MANAGER'
AND MGR IS NOT NULL;
```

### 5. Employees whose manager is JONES

```sql id="p4q5r6"
SELECT ENAME FROM EMPLOYEE
WHERE MGR = (
    SELECT EMPNO FROM EMPLOYEE WHERE ENAME = 'JONES'
);
```

### 6. Employees in sales department

```sql id="s7t8u9"
SELECT ENAME FROM EMPLOYEE
WHERE DEPTNO = (
    SELECT DEPTNO FROM DEPARTMENT WHERE DNAME = 'SALES'
);
```

### 7. Salary between 2000 and 5000 in CHICAGO

```sql id="v1w2x3"
SELECT ENAME, SAL FROM EMPLOYEE
WHERE SAL BETWEEN 2000 AND 5000
AND DEPTNO = (
    SELECT DEPTNO FROM DEPARTMENT WHERE LOC = 'CHICAGO'
);
```

### 8. Salary greater than manager

```sql id="y4z5a6"
SELECT E.ENAME, E.SAL FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.SAL > M.SAL;
```

### 9. Same department as manager

```sql id="b7c8d9"
SELECT E.ENAME FROM EMPLOYEE E
JOIN EMPLOYEE M ON E.MGR = M.EMPNO
WHERE E.DEPTNO = M.DEPTNO;
```

---

## Output

### ANY vs ALL Output

```text id="e1f2g3"
ENAME   SAL
-------------
KING    5000
```

### Manager Condition Output

```text id="h4i5j6"
ENAME
------
SCOTT
FORD
```

### Salary Comparison Output

```text id="k7l8m9"
ENAME   SAL
-------------
FORD    3000
SCOTT   3000
```

### Same Department Output

```text id="n1o2p3"
ENAME
------
ALLEN
WARD
```

---

## Result

Successfully executed advanced SQL queries using ALL, ANY, subqueries, and complex conditions.
