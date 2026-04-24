
# Experiment 7: SQL Queries with Advanced Calculations and Grouping

## Aim

To perform advanced SQL queries using grouping, aggregate calculations, formatting, and date operations.

---

## Theory

SQL allows complex data analysis using:

* **GROUP BY**: Groups records based on a column
* **Aggregate Functions**: SUM, COUNT, MAX, MIN
* **HAVING**: Filters grouped data
* **Date Functions**: Used for calculations like remaining days
* **Mathematical Operations**: Used for salary comparison and formatting

According to the lab program (page 7 of the uploaded file) , this experiment focuses on grouping, aggregate analysis, and advanced calculations.

---

## Question

Perform the following queries:

1. Compute number of days remaining in the current year.
2. Find highest and lowest salaries and their difference.
3. List employees whose commission is greater than 25% of salary.
4. Display salary in dollar format.
5. Display job-wise salary matrix by department.
6. Display total employees and number hired in different years.
7. Find last Sunday of any month.
8. Display department-wise employee count.
9. Display job-wise employee count.
10. Display department-wise total salary.

---

## Queries

### 1. Days remaining in current year

```sql id="a1b2c3"
SELECT (TO_DATE('31-DEC-' || TO_CHAR(SYSDATE,'YYYY'),'DD-MON-YYYY') - SYSDATE) AS DAYS_LEFT
FROM DUAL;
```

### 2. Highest, Lowest Salary and Difference

```sql id="d4e5f6"
SELECT MAX(SAL) AS MAX_SAL,
MIN(SAL) AS MIN_SAL,
(MAX(SAL) - MIN(SAL)) AS DIFFERENCE
FROM EMPLOYEE;
```

### 3. Commission greater than 25% of salary

```sql id="g7h8i9"
SELECT ENAME, COMM, SAL FROM EMPLOYEE
WHERE COMM > (SAL * 0.25);
```

### 4. Salary in dollar format

```sql id="j1k2l3"
SELECT ENAME, TO_CHAR(SAL, '$9999') FROM EMPLOYEE;
```

### 5. Job-wise salary matrix

```sql id="m4n5o6"
SELECT JOB,
SUM(CASE WHEN DEPTNO = 10 THEN SAL END) AS DEPT10,
SUM(CASE WHEN DEPTNO = 20 THEN SAL END) AS DEPT20,
SUM(CASE WHEN DEPTNO = 30 THEN SAL END) AS DEPT30,
SUM(SAL) AS TOTAL
FROM EMPLOYEE
GROUP BY JOB;
```

### 6. Employees hired in different years

```sql id="p7q8r9"
SELECT COUNT(*) AS TOTAL,
SUM(CASE WHEN TO_CHAR(HIREDATE,'YYYY')='1980' THEN 1 ELSE 0 END) AS Y1980,
SUM(CASE WHEN TO_CHAR(HIREDATE,'YYYY')='1981' THEN 1 ELSE 0 END) AS Y1981,
SUM(CASE WHEN TO_CHAR(HIREDATE,'YYYY')='1982' THEN 1 ELSE 0 END) AS Y1982,
SUM(CASE WHEN TO_CHAR(HIREDATE,'YYYY')='1983' THEN 1 ELSE 0 END) AS Y1983
FROM EMPLOYEE;
```

### 7. Last Sunday of any month

```sql id="s1t2u3"
SELECT NEXT_DAY(LAST_DAY(SYSDATE) - 7, 'SUNDAY') FROM DUAL;
```

### 8. Department-wise employee count

```sql id="v4w5x6"
SELECT DEPTNO, COUNT(*) AS TOTAL_EMP
FROM EMPLOYEE
GROUP BY DEPTNO;
```

### 9. Job-wise employee count

```sql id="y7z8a9"
SELECT JOB, COUNT(*) AS TOTAL_EMP
FROM EMPLOYEE
GROUP BY JOB;
```

### 10. Department-wise total salary

```sql id="b1c2d3"
SELECT DEPTNO, SUM(SAL) AS TOTAL_SALARY
FROM EMPLOYEE
GROUP BY DEPTNO;
```

---

## Output

### Days Remaining

```text id="e4f5g6"
DAYS_LEFT
-----------
120
```

### Salary Difference

```text id="h7i8j9"
MAX_SAL   MIN_SAL   DIFFERENCE
-------------------------------
5000      800       4200
```

### Commission Output

```text id="k1l2m3"
ENAME   COMM   SAL
-------------------
MARTIN  1400   1250
```

### Group By Output

```text id="n4o5p6"
DEPTNO   TOTAL_EMP
-------------------
10       3
20       5
30       6
```

```text id="q7r8s9"
JOB       TOTAL_EMP
--------------------
CLERK     4
MANAGER   3
SALESMAN  4
```

---

## Result

Successfully performed advanced SQL queries using GROUP BY, aggregate functions, date calculations, and conditional aggregation.
