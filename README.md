# connecting-aws-rds-mysqldb-to-local-sql-workbench
Here are queries based on your provided schema and data, covering the SQL concepts you requested. Each query includes a brief explanation and expected output.

---

### 1. **Window Function**: Calculate Cumulative Salary by Department
```sql
SELECT 
  deptno, 
  ename, 
  sal, 
  SUM(sal) OVER (PARTITION BY deptno ORDER BY sal DESC) AS cumulative_salary
FROM emp;
```
**Explanation:** Calculates cumulative salaries for each department, ordered by salary.

---

### 2. **ORDER BY**: Employees Ordered by Salary
```sql
SELECT 
  empno, 
  ename, 
  sal 
FROM emp 
ORDER BY sal DESC;
```
**Explanation:** Retrieves employees ordered by salary in descending order.

---

### 3. **HAVING**: Departments with Total Salaries Above 8000
```sql
SELECT 
  deptno, 
  SUM(sal) AS total_salary 
FROM emp 
GROUP BY deptno 
HAVING SUM(sal) > 8000;
```
**Explanation:** Lists departments with total salary greater than 8000.

---

### 4. **BETWEEN**: Employees with Salaries Between 1000 and 3000
```sql
SELECT 
  empno, 
  ename, 
  sal 
FROM emp 
WHERE sal BETWEEN 1000 AND 3000;
```
**Explanation:** Filters employees whose salaries fall between 1000 and 3000.

---

### 5. **MIN and MAX**: Minimum and Maximum Salaries
```sql
SELECT 
  MIN(sal) AS min_salary, 
  MAX(sal) AS max_salary 
FROM emp;
```
**Explanation:** Finds the minimum and maximum salaries.

---

### 6. **CASE and WHEN**: Salary Brackets
```sql
SELECT 
  ename, 
  sal, 
  CASE 
    WHEN sal > 3000 THEN 'High Earner'
    WHEN sal BETWEEN 1500 AND 3000 THEN 'Average Earner'
    ELSE 'Low Earner'
  END AS salary_bracket
FROM emp;
```
**Explanation:** Categorizes employees based on salary.

---

### 7. **IF ELSE (Using CASE)**: Check Manager Validity
```sql
SELECT 
  empno, 
  ename, 
  CASE 
    WHEN mgr IS NOT NULL THEN 'Has Manager'
    ELSE 'No Manager'
  END AS manager_status
FROM emp;
```
**Explanation:** Checks if employees have a manager.

---

### 8. **RANK**: Rank Employees by Salary
```sql
SELECT 
  ename, 
  sal, 
  RANK() OVER (ORDER BY sal DESC) AS rank
FROM emp;
```
**Explanation:** Ranks employees by salary.

---

### 9. **DENSE_RANK**: Dense Rank for Employees
```sql
SELECT 
  ename, 
  sal, 
  DENSE_RANK() OVER (ORDER BY sal DESC) AS dense_rank
FROM emp;
```
**Explanation:** Dense ranks employees by salary, without skipping ranks.

---

### 10. **ROW_NUMBER**: Row Numbers by Department
```sql
SELECT 
  deptno, 
  ename, 
  ROW_NUMBER() OVER (PARTITION BY deptno ORDER BY sal DESC) AS row_num
FROM emp;
```
**Explanation:** Assigns row numbers to employees within each department.

---

### 11. **VIEW**: Create View for High Earners
```sql
CREATE VIEW high_earners AS 
SELECT 
  empno, 
  ename, 
  sal 
FROM emp 
WHERE sal > 3000;
```
**Explanation:** Creates a view for employees earning more than 3000.

---

### 12. **GROUP BY**: Average Salary by Department
```sql
SELECT 
  deptno, 
  AVG(sal) AS avg_salary 
FROM emp 
GROUP BY deptno;
```
**Explanation:** Calculates the average salary for each department.

---

### 13. **JOIN**: Employees and Department Names
```sql
SELECT 
  e.ename, 
  d.dname 
FROM emp e 
JOIN dept d ON e.deptno = d.deptno;
```
**Explanation:** Joins `emp` and `dept` to list employees with their department names.

---

### 14. **SELF JOIN**: Employees with the Same Manager
```sql
SELECT 
  e1.ename AS employee, 
  e2.ename AS manager 
FROM emp e1 
JOIN emp e2 ON e1.mgr = e2.empno;
```
**Explanation:** Finds employees with the same manager.

---

### 15. **SUBQUERY**: Employees Earning More than Department Average
```sql
SELECT 
  empno, 
  ename, 
  sal 
FROM emp 
WHERE sal > (SELECT AVG(sal) FROM emp WHERE deptno = emp.deptno);
```
**Explanation:** Finds employees earning more than their department's average salary.

---

### 16. **UNION**: Combine Employees and Department Heads
```sql
SELECT 
  empno, 
  ename 
FROM emp 
WHERE job = 'PRESIDENT'
UNION 
SELECT 
  deptno, 
  dname 
FROM dept;
```
**Explanation:** Combines employee and department head data.

---

### 17. **EXISTS**: Departments with Employees
```sql
SELECT 
  dname 
FROM dept d 
WHERE EXISTS (SELECT 1 FROM emp e WHERE e.deptno = d.deptno);
```
**Explanation:** Lists departments that have employees.

---

### 18. **LIMIT**: Top 3 Salaries
```sql
SELECT 
  ename, 
  sal 
FROM emp 
ORDER BY sal DESC 
LIMIT 3;
```
**Explanation:** Retrieves the top 3 highest salaries.

---

### 19. **COALESCE**: Replace NULL Commission
```sql
SELECT 
  empno, 
  ename, 
  COALESCE(comm, 0) AS commission 
FROM emp;
```
**Explanation:** Replaces null commission values with 0.

---

### 20. **NULLIF**: Avoid Division by Zero
```sql
SELECT 
  sal / NULLIF(comm, 0) AS salary_to_commission_ratio 
FROM emp;
```
**Explanation:** Avoids division by zero when calculating salary-to-commission ratio.

---
Here’s a comprehensive list of SQL queries, ranging from basic to advanced concepts, with explanations and expected outputs to help you master SQL step by step.

---

### **Basic SQL Queries**

#### 1. **Select All Columns**
```sql
SELECT * FROM emp;
```
**Sine Arrow:** Retrieves all columns and rows from the `emp` table.

---

#### 2. **Select Specific Columns**
```sql
SELECT ename, job FROM emp;
```
**Sine Arrow:** Fetches only the `ename` and `job` columns.

---

#### 3. **WHERE Clause**
```sql
SELECT * FROM emp WHERE deptno = 30;
```
**Sine Arrow:** Filters employees working in department 30.

---

#### 4. **ORDER BY Clause**
```sql
SELECT ename, sal FROM emp ORDER BY sal DESC;
```
**Sine Arrow:** Lists employees ordered by salary in descending order.

---

#### 5. **DISTINCT Keyword**
```sql
SELECT DISTINCT job FROM emp;
```
**Sine Arrow:** Fetches unique job roles.

---

#### 6. **LIKE Operator**
```sql
SELECT ename FROM emp WHERE ename LIKE 'S%';
```
**Sine Arrow:** Finds employees whose names start with "S."

---

#### 7. **BETWEEN Operator**
```sql
SELECT ename, sal FROM emp WHERE sal BETWEEN 1000 AND 3000;
```
**Sine Arrow:** Fetches employees with salaries between 1000 and 3000.

---

#### 8. **IN Operator**
```sql
SELECT ename FROM emp WHERE job IN ('CLERK', 'SALESMAN');
```
**Sine Arrow:** Finds employees working as either `CLERK` or `SALESMAN`.

---

#### 9. **IS NULL**
```sql
SELECT ename FROM emp WHERE comm IS NULL;
```
**Sine Arrow:** Lists employees without a commission.

---

---

### **Intermediate SQL Queries**

#### 10. **Aggregate Functions**
- **Query:**
  ```sql
  SELECT AVG(sal) AS average_salary, SUM(sal) AS total_salary FROM emp;
  ```
  **Sine Arrow:** Calculates the average and total salary.

---

#### 11. **GROUP BY**
- **Query:**
  ```sql
  SELECT deptno, AVG(sal) AS avg_salary FROM emp GROUP BY deptno;
  ```
  **Sine Arrow:** Groups employees by department and calculates the average salary per department.

---

#### 12. **HAVING Clause**
- **Query:**
  ```sql
  SELECT deptno, SUM(sal) AS total_salary FROM emp GROUP BY deptno HAVING SUM(sal) > 8000;
  ```
  **Sine Arrow:** Filters groups with a total salary above 8000.

---

#### 13. **JOIN**
- **Query:**
  ```sql
  SELECT e.ename, d.dname 
  FROM emp e 
  JOIN dept d ON e.deptno = d.deptno;
  ```
  **Sine Arrow:** Joins `emp` and `dept` tables to list employees with their department names.

---

#### 14. **SELF JOIN**
- **Query:**
  ```sql
  SELECT e1.ename AS employee, e2.ename AS manager 
  FROM emp e1 
  JOIN emp e2 ON e1.mgr = e2.empno;
  ```
  **Sine Arrow:** Matches employees with their managers.

---

#### 15. **SUBQUERY**
- **Query:**
  ```sql
  SELECT ename 
  FROM emp 
  WHERE sal > (SELECT AVG(sal) FROM emp);
  ```
  **Sine Arrow:** Finds employees earning above the average salary.

---

#### 16. **UNION**
- **Query:**
  ```sql
  SELECT ename, sal FROM emp WHERE sal > 3000
  UNION
  SELECT ename, sal FROM emp WHERE job = 'CLERK';
  ```
  **Sine Arrow:** Combines employees earning more than 3000 with clerks.

---

#### 17. **EXISTS**
- **Query:**
  ```sql
  SELECT dname 
  FROM dept d 
  WHERE EXISTS (SELECT 1 FROM emp e WHERE e.deptno = d.deptno);
  ```
  **Sine Arrow:** Lists departments that have employees.

---

---

### **Advanced SQL Queries**

#### 18. **Window Functions**
- **Query:**
  ```sql
  SELECT ename, sal, RANK() OVER (ORDER BY sal DESC) AS rank FROM emp;
  ```
  **Sine Arrow:** Ranks employees based on salary.

---

#### 19. **ROW_NUMBER**
- **Query:**
  ```sql
  SELECT deptno, ename, ROW_NUMBER() OVER (PARTITION BY deptno ORDER BY sal DESC) AS row_num 
  FROM emp;
  ```
  **Sine Arrow:** Assigns a row number to employees in each department.

---

#### 20. **CTE (Common Table Expression)**
- **Query:**
  ```sql
  WITH dept_salary AS (
    SELECT deptno, SUM(sal) AS total_salary FROM emp GROUP BY deptno
  )
  SELECT deptno, total_salary FROM dept_salary WHERE total_salary > 8000;
  ```
  **Sine Arrow:** Uses a CTE to calculate and filter total salaries by department.

---

#### 21. **CASE Statement**
- **Query:**
  ```sql
  SELECT ename, sal, 
    CASE 
      WHEN sal > 3000 THEN 'High Earner' 
      WHEN sal BETWEEN 1500 AND 3000 THEN 'Average Earner' 
      ELSE 'Low Earner' 
    END AS salary_category 
  FROM emp;
  ```
  **Sine Arrow:** Categorizes employees into salary brackets.

---

#### 22. **PIVOT**
- **Query:**
  ```sql
  SELECT job, SUM(CASE WHEN deptno = 10 THEN sal ELSE 0 END) AS dept10_salary,
               SUM(CASE WHEN deptno = 20 THEN sal ELSE 0 END) AS dept20_salary
  FROM emp
  GROUP BY job;
  ```
  **Sine Arrow:** Creates a pivot table summarizing salaries by department and job.

---

#### 23. **Recursive CTE**
- **Query:**
  ```sql
  WITH RECURSIVE hierarchy AS (
    SELECT empno, ename, mgr 
    FROM emp 
    WHERE mgr IS NULL 
    UNION ALL 
    SELECT e.empno, e.ename, e.mgr 
    FROM emp e 
    JOIN hierarchy h ON e.mgr = h.empno
  )
  SELECT * FROM hierarchy;
  ```
  **Sine Arrow:** Builds a hierarchy of employees and their managers.

---

#### 24. **Indexes**
- **Query:**
  ```sql
  CREATE INDEX idx_deptno ON emp(deptno);
  ```
  **Sine Arrow:** Creates an index on the `deptno` column for faster lookups.

---

#### 25. **Stored Procedure**
- **Query:**
  ```sql
  DELIMITER //
  CREATE PROCEDURE get_high_earners()
  BEGIN
    SELECT ename, sal FROM emp WHERE sal > 3000;
  END //
  DELIMITER ;
  CALL get_high_earners();
  ```
  **Sine Arrow:** Defines and executes a stored procedure to retrieve high earners.

---

