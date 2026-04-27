# Experiment 1: SQL Table Creation and Basic Operations

## Aim

To create database tables with constraints, insert records, and perform basic SQL operations such as CREATE, INSERT, UPDATE, DELETE, ALTER, and DROP.

---

## Theory

A Database Management System (DBMS) allows users to create, manage, and manipulate data efficiently. SQL (Structured Query Language) is used to interact with databases.

In this experiment:

* Tables are created using **CREATE TABLE** with constraints like Primary Key and Foreign Key.
* Data is inserted using **INSERT INTO**.
* Data manipulation is performed using **UPDATE** and **DELETE**.
* Structure modification is done using **ALTER TABLE**.
* Tables are removed using **DROP TABLE**.

According to the lab program (page 4–5 of the uploaded file) , this experiment focuses on EMPLOYEE and DEPARTMENT tables with given attributes and sample data.

---

## Question

1. Create EMPLOYEE and DEPARTMENT tables with given constraints.
2. Insert records into both tables.
3. Create a new table Employee_master using Employee table.
4. Delete records where DeptNo = 10.
5. Update salary by 10% for DeptNo = 20.
6. Alter SAL column datatype.
7. Drop Employee_master table.

---

## Queries

### 1. Create DEPARTMENT Table

```sql
CREATE TABLE DEPARTMENT (
    DEPTNO NUMBER(2) PRIMARY KEY,
    DNAME VARCHAR2(15) NOT NULL
);
```

### 2. Create EMPLOYEE Table

```sql
CREATE TABLE EMPLOYEE (
    EMPNO NUMBER(4) PRIMARY KEY,
    ENAME VARCHAR2(20) NOT NULL,
    JOB VARCHAR2(20),
    MGR NUMBER(4),
    HIREDATE DATE,
    SAL NUMBER(10),
    COMM NUMBER(7),
    DEPTNO NUMBER(2),
    FOREIGN KEY (DEPTNO) REFERENCES DEPARTMENT(DEPTNO)
);
```

### 3. Insert Values into DEPARTMENT

```sql
INSERT INTO DEPARTMENT VALUES (10, 'RESEARCH');
INSERT INTO DEPARTMENT VALUES (20, 'ACCOUNTING');
INSERT INTO DEPARTMENT VALUES (30, 'SALES');
INSERT INTO DEPARTMENT VALUES (40, 'OPERATIONS');
```

### 4. Insert Values into EMPLOYEE

```sql
INSERT INTO EMPLOYEE VALUES (7369,'SMITH','CLERK',7902,'17-DEC-80',800,NULL,20);
INSERT INTO EMPLOYEE VALUES (7499,'ALLEN','SALESMAN',7698,'20-FEB-81',1600,300,30);
INSERT INTO EMPLOYEE VALUES (7521,'WARD','SALESMAN',7698,'22-FEB-81',1250,300,30);
INSERT INTO EMPLOYEE VALUES (7566,'JONES','MANAGER',7839,'02-APR-81',2975,NULL,20);
```

### 5. Create Employee_master Table

```sql
CREATE TABLE EMPLOYEE_MASTER AS
SELECT * FROM EMPLOYEE;
```

### 6. Delete Records

```sql
DELETE FROM EMPLOYEE_MASTER
WHERE DEPTNO = 10;
```

### 7. Update Salary

```sql
UPDATE EMPLOYEE_MASTER
SET SAL = SAL + (SAL * 0.10)
WHERE DEPTNO = 20;
```

### 8. Alter Table

```sql
ALTER TABLE EMPLOYEE_MASTER
MODIFY SAL NUMBER(10,2);
```

### 9. Drop Table

```sql
DROP TABLE EMPLOYEE_MASTER;
```

---

## Output

### Table Creation

```
Table created.
```

### Insert Operation

```
1 row inserted.
```

### Create Table from Existing Table

```
Table created.
```

### Delete Operation

```
Records deleted successfully.
```

### Update Operation

```
Rows updated.
```

### Alter Table

```
Table altered.
```

### Drop Table

```
Table dropped.
```

---

## Result

Successfully created tables, inserted data, and performed SQL operations such as DELETE, UPDATE, ALTER, and DROP.
