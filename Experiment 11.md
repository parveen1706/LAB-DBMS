# Experiment 11: SQL Queries with Advanced Conditions, Deletion and Analysis

## Aim

To perform SQL queries involving deletion, complex conditions, salary analysis, and ranking.

---

## Theory

SQL provides commands to manipulate and analyze data:

* **DELETE**: Removes records from a table
* **ORDER BY**: Sorts data
* **Aggregate Functions**: Used for analysis (AVG, MAX, MIN)
* **Subqueries**: Used for comparisons and filtering
* **ROWNUM / LIMIT**: Used to find top records

This experiment focuses on combining multiple SQL concepts to solve real-world database problems.

According to the lab program (page 9 of the uploaded file) , this experiment includes deletion, salary comparisons, ranking, and filtering conditions.

---

## Question

Perform the following queries:

1. Delete employees who joined before 31-Dec-1982 and belong to New York or Chicago.
2. Display employee name, job, department name, and location for managers.
3. Display name and salary of FORD if his salary is equal to highest in his grade.
4. Find top 5 earners of the company.
5. Display employees with highest salary.
6. Display employees whose salary is equal to average of max and min salary.
7. Display department names where at least 3 employees are working.
8. Display managers earning more than average salary of company.
9. Display managers earning more than average salary of their employees.
10. Display employees whose net pay is greater than any other employee salary.

---

## Queries

### 1. Delete employees

```sql id="a2b3c4"
DELETE FROM EMPLOYEE
WHERE HIREDATE < '31-DEC-82'
AND DEPTNO IN (
    SELECT DEPTNO FROM DEPARTMENT
    WHERE LOC IN ('NEW YORK','CHICAGO')
);
```

### 2. Managers with department and location

```sql id="d5e6f7"
SELECT E.ENAME, E.JOB, D.DNAME, D.LOC
FROM EMPLOYEE E
JOIN DEPARTMENT D ON E.DEPTNO = D.DEPTNO
WHERE E.JOB = 'MANAGER';
```

### 3. FORD salary check

```sql id="g8h9i0"
SELECT ENAME, SAL FROM EMPLOYEE
WHERE ENAME = 'FORD'
AND SAL = (
    SELECT MAX(SAL) FROM EMPLOYEE WHERE JOB = 'ANALYST'
);
```

### 4. Top 5 earners

```sql id="j1k2l3"
SELECT ENAME, SAL FROM EMPLOYEE
ORDER BY SAL DESC
FETCH FIRST 5 ROWS ONLY;
```

### 5. Highest salary employees

```sql id="m4n5o6"
SELECT ENAME, SAL FROM EMPLOYEE
WHERE SAL = (SELECT MAX(SAL) FROM EMPLOYEE);
```

### 6. Salary equal to average of max and min

```sql id="p7q8r9"
SELECT ENAME, SAL FROM EMPLOYEE
WHERE SAL = (
    (SELECT MAX(SAL) FROM EMPLOYEE) +
    (SELECT MIN(SAL) FROM EMPLOYEE)
)/2;
```

### 7. Departments with at least 3 employees

```sql id="s1t2u3"
SELECT D.DNAME FROM DEPARTMENT D
JOIN EMPLOYEE E ON D.DEPTNO = E.DEPTNO
GROUP BY D.DNAME
HAVING COUNT(*) >= 3;
```

### 8. Managers earning more than average salary

```sql id="v4w5x6"
SELECT ENAME FROM EMPLOYEE
WHERE JOB = 'MANAGER'
AND SAL > (SELECT AVG(SAL) FROM EMPLOYEE);
```

### 9. Managers earning more than their employees

```sql id="y7z8a9"
SELECT M.ENAME FROM EMPLOYEE M
WHERE M.JOB = 'MANAGER'
AND M.SAL > (
    SELECT AVG(E.SAL)
    FROM EMPLOYEE E
    WHERE E.MGR = M.EMPNO
);
```

### 10. Employees with highest net pay

```sql id="b1c2d3"
SELECT ENAME, (SAL + NVL(COMM,0)) AS NET_PAY
FROM EMPLOYEE
WHERE (SAL + NVL(COMM,0)) >= ALL (
    SELECT SAL FROM EMPLOYEE
);
```

---

## Output

### Delete Operation

```text id="e4f5g6"
Rows deleted successfully.
```

### Managers Output

```text id="h7i8j9"
ENAME   JOB      DNAME       LOC
----------------------------------
JONES   MANAGER  ACCOUNTING  NEW YORK
```

### Top Earners

```text id="k1l2m3"
ENAME   SAL
-------------
KING    5000
SCOTT   3000
FORD    3000
```

### Department Count

```text id="n4o5p6"
DNAME
-------
SALES
ACCOUNTING
```

---

## Result

Successfully executed advanced SQL queries involving deletion, ranking, aggregate analysis, and complex conditions.
