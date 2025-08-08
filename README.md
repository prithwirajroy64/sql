# Employee & Department Database – SQL Queries

### EMP Table

```sql
CREATE TABLE EMP (empno INT(5) PRIMARY KEY, ename VARCHAR(50), job CHAR(10), mgr INT(5), hiredate DATE, sal float(10, 2), comm float(10, 2), deptno float(3));
```

```sql
INSERT INTO EMP VALUES (7369, 'Smith', 'Clerk', 7902, '1980-12-17', 800, NULL, 20);
INSERT INTO EMP VALUES (7499, 'Allen', 'Salesman', 7698, '1981-02-20', 1600, 300, 30);
INSERT INTO EMP VALUES (7521, 'Ward', 'Salesman', 7698, '1981-02-22', 1250, 500, 30);
INSERT INTO EMP VALUES (7566, 'Jones', 'Manager', 7839, '1981-04-02', 2975, NULL, 20);
INSERT INTO EMP VALUES (7654, 'Martin', 'Salesman', 7698, '1981-09-28', 1250, 1400, 30);
INSERT INTO EMP VALUES (7698, 'Blake', 'Manager', 7839, '1981-05-01', 2850, NULL, 30);
INSERT INTO EMP VALUES (7782, 'Clark', 'Manager', 7839, '1981-06-09', 2450, NULL, 10);
INSERT INTO EMP VALUES (7788, 'Scott', 'Analyst', 7566, '1982-12-09', 3000, NULL, 20);
INSERT INTO EMP VALUES (7839, 'King', 'President', NULL, '1981-11-17', 5000, NULL, 10);
INSERT INTO EMP VALUES (7844, 'Turner', 'Salesman', 7698, '1981-09-08', 1500, 0, 30);
INSERT INTO EMP VALUES (7876, 'Adams', 'Clerk', 7788, '1983-01-12', 1100, NULL, 20);
INSERT INTO EMP VALUES (7900, 'James', 'Clerk', 7698, '1981-12-03', 950, NULL, 30);
INSERT INTO EMP VALUES (7902, 'Ford', 'Analyst', 7566, '1981-12-04', 3000, NULL, 20);
INSERT INTO EMP VALUES (7934, 'Miller', 'Clerk', 7782, '1982-01-23', 1300, NULL, 10);
```

### DEPT Table

```sql
CREATE TABLE DEPT ( deptno INT(3) PRIMARY KEY, dname VARCHAR(50), loc VARCHAR(50));
```

```sql
INSERT INTO DEPT (deptno, dname, loc) VALUES (10, 'Accounting', 'New York');
INSERT INTO DEPT (deptno, dname, loc) VALUES (20, 'Research', 'Dallas');
INSERT INTO DEPT (deptno, dname, loc) VALUES (30, 'Sales', 'Chicago');
INSERT INTO DEPT (deptno, dname, loc) VALUES (40, 'Operations', 'Boston');
```


## 1. Number of employees & average salary in dept 20
```sql
SELECT COUNT(*) AS num_employees,
 AVG(sal) AS avg_salary
FROM EMP
WHERE deptno = 20;
```

## 2. Name, salary & PF (10% of basic salary)
```sql
SELECT ename,
 sal,
 sal * 0.10 AS PF
FROM EMP;
```

## 3. Employees with more than 2 years experience
```sql
SELECT ename, hiredate
FROM EMP
WHERE TIMESTAMPDIFF(YEAR, hiredate, CURDATE()) > 2;
```

## 4. Employee details in ascending order of salary
```sql
SELECT *
FROM EMP
ORDER BY sal ASC;
```

## 5. Employee name & hire date in descending order of hire date
```sql
SELECT ename, hiredate
FROM EMP
ORDER BY hiredate DESC;
```

## 6. Name, salary, PF, HRA, DA & Gross (HRA = 50%, DA = 30%)
```sql
SELECT ename,
 sal,
 sal * 0.10 AS PF,
 sal * 0.50 AS HRA,
 sal * 0.30 AS DA,
 sal + (sal * 0.50) + (sal * 0.30) AS gross
FROM EMP
ORDER BY gross ASC;
```

## 7. Department numbers & number of employees
```sql
SELECT deptno,
 COUNT(*) AS num_employees
FROM EMP
GROUP BY deptno;
```

## 8. Department number & total salary payable
```sql
SELECT deptno,
 SUM(sal) AS total_salary
FROM EMP
GROUP BY deptno;
```

## 9. Jobs & number of employees (descending order)
```sql
SELECT job,
 COUNT(*) AS num_employees
FROM EMP
GROUP BY job
ORDER BY num_employees DESC;
```

## 10. Total, max, min & avg salary — job wise
```sql
SELECT job,
 SUM(sal) AS total_salary,
 MAX(sal) AS max_salary,
 MIN(sal) AS min_salary,
 AVG(sal) AS avg_salary
FROM EMP
GROUP BY job;
```

## 11. Total, max, min & avg salary — for dept 20
```sql
SELECT SUM(sal) AS total_salary,
 MAX(sal) AS max_salary,
 MIN(sal) AS min_salary,
 AVG(sal) AS avg_salary
FROM EMP
WHERE deptno = 20;
```

## 12. Total, max, min & avg salary — job wise, dept 20, avg > 1000
```sql
SELECT job,
 SUM(sal) AS total_salary,
 MAX(sal) AS max_salary,
 MIN(sal) AS min_salary,
 AVG(sal) AS avg_salary
FROM EMP
WHERE deptno = 20
GROUP BY job
HAVING AVG(sal) > 1000;
```

