### 1. How to find nth highest salary in SQL?

```sql
// To find the highest salary it is straight forward. We can simply use the Max() function as shown below.
SELECT Max(Salary) FROM Employees

//To get the second highest salary use a sub query along with Max() function as shown below.
SELECT Max(Salary)
FROM Employees
WHERE Salary < (SELECT Max(Salary) FROM Employees)

//To find nth highest salary using Sub-Query
SELECT TOP 1 SALARY
FROM (
      SELECT DISTINCT TOP N SALARY
      FROM EMPLOYEES
      ORDER BY SALARY DESC
      ) RESULT
ORDER BY SALARY

//To find nth highest salary using CTE
WITH RESULT AS
(
    SELECT SALARY,
           DENSE_RANK() OVER (ORDER BY SALARY DESC) AS DENSERANK
    FROM EMPLOYEES
)
SELECT TOP 1 SALARY
FROM RESULT
WHERE DENSERANK = N

//To find 2nd highest salary we can use any of the above queries. Simple replace N with 2. 

//Similarly, to find 3rd highest salary, simple replace N with 3. 
```
