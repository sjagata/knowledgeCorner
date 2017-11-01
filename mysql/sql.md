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

//To find nth highest salary using CTE - Common table expression
//DENSE_RANK() gives rank based on salary. Ex: 80000 - 1, 70000 - 2, 30000 - 3
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

we can use ROW_NUMBER instead of DENSE_RANK if we have no duplicates

<br>
<br>

### 2. SQL query to get the complete organization hierarchy based on an Employee ID
* Joining a table with itself - Self Join
* Self Join can be classified as 
   * Inner Self Join - matched items in both tables
   * Outer Self Join (Left, Right and Full)
   * Cross Self Join - It wont have an ON clause 
   
```sql
Declare @ID int ;
Set @ID = 7;

WITH EmployeeCTE AS
(
 Select EmployeeId, EmployeeName, ManagerID
 From Employees
 Where EmployeeId = @ID
 
 UNION ALL
 
 Select Employees.EmployeeId , Employees.EmployeeName, Employees.ManagerID
 From Employees
 JOIN EmployeeCTE
 ON Employees.EmployeeId = EmployeeCTE.ManagerID
)

Select E1.EmployeeName, ISNULL(E2.EmployeeName, 'No Boss') as ManagerName
From EmployeeCTE E1
LEFT Join EmployeeCTE E2
ON E1.ManagerID = E2.EmployeeId
```














