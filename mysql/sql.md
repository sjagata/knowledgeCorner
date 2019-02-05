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
 -- Anchor
 Select EmployeeId, EmployeeName, ManagerID
 From Employees
 Where EmployeeId = @ID
 
 UNION ALL
 
 -- Recursive Member
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

<br>
<br>

### 3. How to delete all duplicates rows except one from a SQL Server table?

```sql
WITH EmployeesCTE AS
(
   SELECT *, ROW_NUMBER() OVER (PARTITION BY ID ORDER BY ID) AS RowNumber
   FROM Employees
)
DELETE FROM EmployeesCTE WHERE RowNumber > 1

Select * from EmployeesCTE
```

<br>
<br>

### 4. SQL query to find employees hired in last n months
DATEDIFF(interval, startDate, ending date)

```sql
Select *
FROM Employees
Where DATEDIFF(MONTH, HireDate, GETDATE()) Between 1 and N
```

<br>
<br>

### 5. Write a SQL query to transform rows to columns
* **Pivot is a sql server operator** that can be used to turn **unique values from one column**, into **multiple columns in the output**, there by effectively rotating a table.

```sql
Select SalesCountry, SalesAgent, SUM(SalesAmount) as Total 
from tblProductSales
group by SalesCountry, SalesAgent
order by SalesCountry, SalesAgent

-- to 

Select SalesAgent, India, US, UK 
from tblProductSales
Pivot 
(
   Sum(SalesAmount) for SalesCountry in ([India],[US],[UK])
) as PivotTable
```

[ref](http://csharp-video-tutorials.blogspot.com/2012/10/pivot-operator-in-sql-server-part-54.html)


```sql
Select Country, City1, City2, City3
From
(
  Select Country, City,
    'City'+
      cast(row_number() over(partition by Country order by Country) 
     as varchar(10)) ColumnSequence
  from Countries
) Temp
pivot
(
  max(City)
  for ColumnSequence in (City1, City2, City3)
) Piv
```

<br>
<br>

### 6. Sql query to retrieve rows that contain only numerical data

```sql
SELECT Value FROM TestTable WHERE ISNUMERIC(Value) = 1
```

<br>
<br>

### 7. Sql query to find department with highest number of employees

[Ans](https://www.youtube.com/redirect?redir_token=KEIFNLb5f-DZAOjtBYumr1GBn-t8MTUwOTU4Mzg0NkAxNTA5NDk3NDQ2&event=video_description&v=pYMc_hxUfLQ&q=http%3A%2F%2Fcsharp-video-tutorials.blogspot.com%2F2014%2F06%2Fpart-8-sql-query-to-find-department.html)

<br>
<br>

### 8. Joining 3 tables

```sql
SELECT DepartmentName, Gender, COUNT(*) as TotalEmployees
FROM Employees
JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID
JOIN Genders ON Employees.GenderID = Genders.GenderID
GROUP BY DepartmentName, Gender
ORDER BY DepartmentName, Gender
```

<br>
<br>

### 9. Diff b/w blocking and deadlocking
[Ans](http://csharp-video-tutorials.blogspot.com/2015/09/difference-between-blocking-and.html)


<br>
<br>

### 10. What does UNION do? What is the difference between UNION and UNION ALL?
UNION merges the contents of two structurally-compatible tables into a single combined table. The difference between UNION and UNION ALL is that UNION will omit duplicate records whereas UNION ALL will include duplicate records.

It is important to note that the performance of UNION ALL will typically be better than UNION, since UNION requires the server to do the additional work of removing any duplicates. So, in cases where is is certain that there will not be any duplicates, or where having duplicates is not a problem, use of UNION ALL would be recommended for performance reasons.

<br>
<br>

### 11. List and explain the different types of JOIN clauses supported in ANSI-standard SQL.
ANSI-standard SQL specifies five types of JOIN clauses as follows:

* **INNER JOIN** (a.k.a. “simple join”): Returns all rows for which there is at least one match in BOTH tables. This is the default type of join if no specific JOIN type is specified.
* **LEFT JOIN (or LEFT OUTER JOIN):** Returns all rows from the left table, and the matched rows from the right table; i.e., the results will contain all records from the left table, even if the JOIN condition doesn’t find any matching records in the right table. This means that if the ON clause doesn’t match any records in the right table, the JOIN will still return a row in the result for that record in the left table, but with NULL in each column from the right table.
* **RIGHT JOIN (or RIGHT OUTER JOIN):** Returns all rows from the right table, and the matched rows from the left table. This is the exact opposite of a LEFT JOIN; i.e., the results will contain all records from the right table, even if the JOIN condition doesn’t find any matching records in the left table. This means that if the ON clause doesn’t match any records in the left table, the JOIN will still return a row in the result for that record in the right table, but with NULL in each column from the left table.
* **FULL JOIN (or FULL OUTER JOIN):** Returns all rows for which there is a match in EITHER of the tables. Conceptually, a FULL JOIN combines the effect of applying both a LEFT JOIN and a RIGHT JOIN; i.e., its result set is equivalent to performing a UNION of the results of left and right outer queries.
* **CROSS JOIN:** Returns all records where each row from the first table is combined with each row from the second table (i.e., returns the Cartesian product of the sets of rows from the joined tables). Note that a CROSS JOIN can either be specified using the CROSS JOIN syntax (“explicit join notation”) or (b) listing the tables in the FROM clause separated by commas without using a WHERE clause to supply join criteria (“implicit join notation”).

<br>
<br>

### 12. What is the difference between the RANK() and DENSE_RANK() functions? Provide an example.
The only difference between the RANK() and DENSE_RANK() functions is in cases where there is a “tie”; i.e., in cases where multiple values in a set have the same ranking. In such cases, RANK() will assign non-consecutive “ranks” to the values in the set (resulting in gaps between the integer ranking values when there is a tie), whereas DENSE_RANK() will assign consecutive ranks to the values in the set (so there will be no gaps between the integer ranking values in the case of a tie).

For example, consider the set {25, 25, 50, 75, 75, 100}. For such a set, RANK() will return {1, 1, 3, 4, 4, 6} (note that the values 2 and 5 are skipped), whereas DENSE_RANK() will return {1,1,2,3,3,4}.

<br>
<br>

### 13. What is the difference between the WHERE and HAVING clauses?
When GROUP BY is not used, the WHERE and HAVING clauses are essentially equivalent.

However, when GROUP BY is used:

The WHERE clause is used to filter records from a result. The filtering occurs before any groupings are made.
The HAVING clause is used to filter values from a group (i.e., to check conditions after aggregation into groups has been performed).

* The group by clause combines all those records that have identical values in a particular field or any group of fields.

<br>
<br>

### 14. What is the difference between char and varchar2?
When stored in a database, varchar2 uses only the allocated space. E.g. if you have a varchar2(1999) and put 50 bytes in the table, it will use 52 bytes.

But when stored in a database, char always uses the maximum length and is blank-padded. E.g. if you have char(1999) and put 50 bytes in the table, it will consume 2000 bytes.

<br>
<br>

### 15. an SQL query to transpose text.

```sql
SELECT SUBSTR('CAPONE', LEVEL, 1)
FROM DUAL CONNECT BY LEVEL <= LENGTH('CAPONE');
```


<br>
<br>

### 16. What is the difference between IN and EXISTS?
#### IN:
* Works on List result set
* Doesn’t work on subqueries resulting in Virtual tables with multiple columns
* Compares every value in the result list
* Performance is comparatively SLOW for larger resultset of subquery

#### EXISTS:
* Works on Virtual tables
* Is used with co-related queries
* Exits comparison when match is found
* Performance is comparatively FAST for larger resultset of subquery

`EXISTS` will tell you whether a query returned any results. e.g.:
```sql
SELECT * 
FROM Orders o 
WHERE EXISTS (
    SELECT * 
    FROM Products p 
    WHERE p.ProductNumber = o.ProductNumber)
```
`IN` is used to compare one value to several, and can use literal values, like this:

```sql
SELECT * 
FROM Orders 
WHERE ProductNumber IN (1, 10, 100)
```
You can also use query results with the IN clause, like this:
```sql
SELECT * 
FROM Orders 
WHERE ProductNumber IN (
    SELECT ProductNumber 
    FROM Products 
    WHERE ProductInventoryQuantity > 0)
```

<br>
<br>

### ORDER BY vs GROUP BY 

* **ORDER BY** alters the order in which items are returned.

* **GROUP BY** will aggregate records by the specified columns which allows you to perform aggregation functions on non-grouped columns (such as SUM, COUNT, AVG, etc).

```sql
TABLE:
ID NAME
1  Peter
2  John
3  Greg
4  Peter

SELECT *
FROM TABLE
ORDER BY NAME

= 
3 Greg
2 John
1 Peter
4 Peter

SELECT Count(ID), NAME
FROM TABLE
GROUP BY NAME

= 
1 Greg
1 John 
2 Peter

SELECT NAME
FROM TABLE
GROUP BY NAME
HAVING Count(ID) > 1

=
Peter
```

<br>
<br>

### Primary Key vs Unique Key

**Primary Key:**

* There can only be one primary key in a table
* In some DBMS it cannot be NULL - e.g. MySQL adds NOT NULL
* Primary Key is a unique key identifier of the record

**Unique Key:**

* Can be more than one unique key in one table
* Unique key can have NULL values
* It can be a candidate key
* Unique key can be NULL and may not be unique

**Candidate Key:**

* Minimum set of attributes/coulmns used to uniquely differentiate records of the table.

<br>
<hr>














Refereneces :

* [Ref](https://www.youtube.com/watch?v=Kd3HTph0Mds&index=2&list=PL6n9fhu94yhXcztdLO7i6mdyaegC8CJwR)
* [link](https://www.toptal.com/sql/interview-questions)
