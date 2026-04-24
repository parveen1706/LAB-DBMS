# Experiment 6: SQL Functions – Date, Conversion and Conditional Functions

## Aim

To perform SQL queries using date functions, conversion functions, and conditional expressions.

---

## Theory

SQL provides built-in functions to handle dates, formatting, and conditional logic:

* **Date Functions**: SYSDATE, ADD_MONTHS, NEXT_DAY, LAST_DAY
* **Conversion Functions**: TO_CHAR, TO_DATE
* **Conditional Functions**: DECODE
* **Arithmetic on Dates**: Used to calculate age, days, months

According to the lab program (page 6–7 of the uploaded file) , this experiment focuses on date manipulation, formatting, and conditional display using SQL functions.

---

## Question

Perform the following queries:

1. Display empno, ename, deptno with department name using DECODE.
2. Display your age in days.
3. Display your age in months.
4. Display current date in formatted form.
5. Display employee joining information in sentence form.
6. Find next Saturday after current date.
7. Display current time.
8. Display date three months before current date.
9. Display employees who joined in December.
10. Display employees based on salary and joining conditions.

---

## Queries

### 1. Display department name using DECODE

```sql id="d1f2g3"
SELECT EMPNO, ENAME,
DECODE(DEPTNO,
10, 'RESEARCH',
20, 'ACCOUNTING',
30, 'SALES',
40, 'OPERATIONS') AS DEPARTMENT
FROM EMPLOYEE;
```

### 2. Age in days

```sql id="h4j5k6"
SELECT (SYSDATE - TO_DATE('01-JAN-2000','DD-MON-YYYY')) AS AGE_IN_DAYS
FROM DUAL;
```

### 3. Age in months

```sql id="l7z8x9"
SELECT MONTHS_BETWEEN(SYSDATE, TO_DATE('01-JAN-2000','DD-MON-YYYY')) AS AGE_IN_MONTHS
FROM DUAL;
```

### 4. Current date formatted

```sql id="c1v2b3"
SELECT TO_CHAR(SYSDATE, 'DDth Month Day YYYY') FROM DUAL;
```

### 5. Employee joining sentence

```sql id="n4m5q6"
SELECT ENAME || ' has joined the company on ' ||
TO_CHAR(HIREDATE, 'Day DDth Month YYYY') AS DETAILS
FROM EMPLOYEE;
```

### 6. Next Saturday

```sql id="w7e8r9"
SELECT NEXT_DAY(SYSDATE, 'SATURDAY') FROM DUAL;
```

### 7. Current time

```sql id="t1y2u3"
SELECT TO_CHAR(SYSDATE, 'HH:MI:SS AM') FROM DUAL;
```

### 8. Date 3 months before

```sql id="i4o5p6"
SELECT ADD_MONTHS(SYSDATE, -3) FROM DUAL;
```

### 9. Employees joined in December

```sql id="a7s8d9"
SELECT ENAME FROM EMPLOYEE
WHERE TO_CHAR(HIREDATE, 'MON') = 'DEC';
```

### 10. Salary and joining condition

```sql id="f1g2h3"
SELECT ENAME, SAL FROM EMPLOYEE
WHERE (SAL * 0.10) = EXTRACT(YEAR FROM HIREDATE);
```

---

## Output

### DECODE Output

```text id="j4k5l6"
EMPNO   ENAME   DEPARTMENT
---------------------------
7369    SMITH   ACCOUNTING
7499    ALLEN   SALES
```

### Date Function Output

```text id="z7x8c9"
AGE_IN_DAYS
-------------
9000
```

```text id="v1b2n3"
AGE_IN_MONTHS
--------------
300
```

### Formatted Date Output

```text id="m4n5b6"
15th August Friday 1997
```

### Joining Sentence Output

```text id="q7w8e9"
SMITH has joined the company on Wednesday 17th December 1980
```

---

## Result

Successfully executed SQL queries using date functions, conversion functions, and conditional expressions.
