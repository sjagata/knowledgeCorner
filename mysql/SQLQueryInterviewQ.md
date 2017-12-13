
### Table Name : Employee

|Employee_id|	First_name|	Last_name|	Salary	|Joining_date|	Department|
|-----------|-----------|----------|----------|------------|------------|
|1	|John	|Abraham	|1000000|	01-JAN-13 12.00.00 AM	|Banking|
|2	|Michael|	Clarke	|800000|	01-JAN-13 12.00.00 AM|	Insurance|
|3	|Roy|	Thomas|	700000|	01-FEB-13 12.00.00 AM	|Banking|
|4	|Tom|	Jose|	600000|	01-FEB-13 12.00.00 AM	|Insurance|
|5	|Jerry|	Pinto|	650000|	01-FEB-13 12.00.00 AM	|Insurance|
|6|	Philip	|Mathew|	750000|	01-JAN-13 12.00.00 AM	|Services|
|7	|TestName1|	123	|650000	|01-JAN-13 12.00.00 AM	|Services|
|8|	TestName2|	Lname%	|600000|	01-FEB-13 12.00.00 AM	|Insurance|


### Table Name : Incentives

|Employee_ref_id	|Incentive_date|	Incentive_amount|
|-----------|-----------|----------|
|1	|01-FEB-13	|5000|
|2	|01-FEB-13|	3000|
|3	|01-FEB-13|	4000|
|1	|01-JAN-13|	4500|
|2|	01-JAN-13|	3500|

<br>
<br>

### SQL Queries Interview Questions and Answers on "SQL Select"

#### 1.Get all employee details from the employee table
```sql
Select * from employee 
```
#### 2.Get First_Name,Last_Name from employee table
```sql
Select first_name, Last_Name from employee 
```
#### 3. Get First_Name from employee table using alias name “Employee Name”
```sql
Select first_name Employee Name from employee 
```
#### 4.Get First_Name from employee table in upper case
```sql
Select upper(FIRST_NAME) from EMPLOYEE 
```
#### 5.Get First_Name from employee table in lower case
```sql
Select lower(FIRST_NAME) from EMPLOYEE 
```
#### 6.Get unique DEPARTMENT from employee table
```sql
select distinct DEPARTMENT from EMPLOYEE
```
#### 7. Select first 3 characters of FIRST_NAME from EMPLOYEE

* Oracle Equivalent of SQL Server SUBSTRING is SUBSTR, Query : 
```sql
select substr(FIRST_NAME,0,3) from employee
```
* SQL Server Equivalent of Oracle SUBSTR is SUBSTRING, Query : 
```sql
select substring(FIRST_NAME,1,3) from employee
```
* MySQL Server Equivalent of Oracle SUBSTR is SUBSTRING. In MySQL start position is 1, Query : 
```sql
select substring(FIRST_NAME,1,3) from employee
```
#### 8. Get position of 'o' in name 'John' from employee table

* Oracle Equivalent of SQL Server CHARINDEX is INSTR, Query : 
```sql
Select instr(FIRST_NAME,'o') from employee where first_name='John'
```
* SQL Server Equivalent of Oracle INSTR is CHARINDEX, Query: 
```sql
Select CHARINDEX('o',FIRST_NAME,0) from employee where first_name='John'
```
* MySQL Server Equivalent of Oracle INSTR is LOCATE, Query: 
```sql
Select LOCATE('o',FIRST_NAME) from employee where first_name='John'
```
#### 9. Get FIRST_NAME from employee table after removing white spaces from right side
```sql
select RTRIM(FIRST_NAME) from employee
```
#### 10. Get FIRST_NAME from employee table after removing white spaces from left side
```sql
select LTRIM(FIRST_NAME) from employee
```
#### 11. Get length of FIRST_NAME from employee table

* Oracle,MYSQL Equivalent of SQL Server Len is Length , Query :
```sql
select length(FIRST_NAME) from employee
```

* SQL Server Equivalent of Oracle,MYSQL Length is Len, Query :
```sql
select len(FIRST_NAME) from employee
```
#### 12. Get First_Name from employee table after replacing 'o' with '$'
```sql
select REPLACE(FIRST_NAME,'o','$') from employee
```
#### 13. Get First_Name and Last_Name as single column from employee table separated by a '_'

* Oracle Equivalent of MySQL concat is '||', Query : 
```sql
Select FIRST_NAME|| '_' ||LAST_NAME from EMPLOYEE
```
* SQL Server Equivalent of MySQL concat is '+', Query : 
```sql
Select FIRST_NAME + '_' +LAST_NAME from EMPLOYEE
```
* MySQL Equivalent of Oracle '||' is concat, Query : 
```sql
Select concat(FIRST_NAME,'_',LAST_NAME) from EMPLOYEE
```
#### 14. Get FIRST_NAME ,Joining year,Joining Month and Joining Date from employee table

* SQL Queries in Oracle, 
```sql
Select FIRST_NAME, to_char(joining_date,'YYYY') JoinYear , to_char(joining_date,'Mon'), to_char(joining_date,'dd') from EMPLOYEE
```
* SQL Queries in SQL Server, 
```sql
select SUBSTRING (convert(varchar,joining_date,103),7,4) , SUBSTRING (convert(varchar,joining_date,100),1,3) , SUBSTRING (convert(varchar,joining_date,100),5,2) from EMPLOYEE
```
* SQL Queries in MySQL, 
```sql
select year(joining_date),month(joining_date), DAY(joining_date) from EMPLOYEE
```
#### 15. Get all employee details from the employee table order by First_Name Ascending
```sql
Select * from employee order by FIRST_NAME asc
```
#### 16. Get all employee details from the employee table order by First_Name descending
```sql
Select * from employee order by FIRST_NAME desc
 ```
#### 17. Get all employee details from the employee table order by First_Name Ascending and Salary descending
```sql
Select * from employee order by FIRST_NAME asc,SALARY desc
```

<br>
<br>

### "SQL Where Condition" Interview Questions

<hr>

#### 18. Get employee details from employee table whose employee name is “John”
```sql
Select * from EMPLOYEE where FIRST_NAME='John'
```
#### 19. Get employee details from employee table whose employee name are “John” and “Roy”
```sql
Select * from EMPLOYEE where FIRST_NAME in ('John','Roy')
```
#### 20. Get employee details from employee table whose employee name are not “John” and “Roy”
```sql
Select * from EMPLOYEE where FIRST_NAME not in ('John','Roy')
```

<br>
<br>

### "SQL Wild Card Search" Interview Questions

<hr>

#### 21. Get employee details from employee table whose first name starts with 'J'
```sql
Select * from EMPLOYEE where FIRST_NAME like 'J%'
```
#### 22. Get employee details from employee table whose first name contains 'o'
```sql
Select * from EMPLOYEE where FIRST_NAME like '%o%'
```
#### 23. Get employee details from employee table whose first name ends with 'n'
```sql
Select * from EMPLOYEE where FIRST_NAME like '%n'
```

<br>
<br>

### "SQL Pattern Matching" Interview Questions

<hr>

#### 24. Get employee details from employee table whose first name ends with 'n' and name contains 4 letters
```sql
Select * from EMPLOYEE where FIRST_NAME like '___n' (Underscores)
```
#### 25. Get employee details from employee table whose first name starts with 'J' and name contains 4 letters
```sql
Select * from EMPLOYEE where FIRST_NAME like 'J___' (Underscores)
```
#### 26. Get employee details from employee table whose Salary greater than 600000
```sql
Select * from EMPLOYEE where Salary >600000
```
#### 27. Get employee details from employee table whose Salary less than 800000
```sql
Select * from EMPLOYEE where Salary <800000
```
#### 28. Get employee details from employee table whose Salary between 500000 and 800000
```sql
Select * from EMPLOYEE where Salary between 500000 and 800000
```
#### 29. Get employee details from employee table whose name is 'John' and 'Michael'
```sql
Select * from EMPLOYEE where FIRST_NAME in ('John','Michael')
```

<br>
<br>

### Interview Questions on "SQL DATE Functions"

<hr>

#### 30. Get employee details from employee table whose joining year is “2013”
* SQL Queries in Oracle, 
```sql
Select * from EMPLOYEE where to_char(joining_date,'YYYY')='2013'
```
* SQL Queries in SQL Server, 
```sql
Select * from EMPLOYEE where SUBSTRING(convert(varchar,joining_date,103),7,4)='2013'
```
* SQL Queries in MySQL, 
```sql
Select * from EMPLOYEE where year(joining_date)='2013'
```
#### 31. Get employee details from employee table whose joining month is “January”
* SQL Queries in Oracle, 
```sql
Select * from EMPLOYEE where to_char(joining_date,'MM')='01' or Select * from EMPLOYEE where to_char(joining_date,'Mon')='Jan'
```
* SQL Queries in SQL Server, 
```sql
Select * from EMPLOYEE where SUBSTRING(convert(varchar,joining_date,100),1,3)='Jan'
```
* SQL Queries in MySQL, 
```sql
Select * from EMPLOYEE where month(joining_date)='01'
```
#### 32. Get employee details from employee table who joined before January 1st 2013
* SQL Queries in Oracle, 
```sql
Select * from EMPLOYEE where JOINING_DATE <to_date('01/01/2013','dd/mm/yyyy')
```
* SQL Queries in SQL Server (Format - “MM/DD/YYYY”), 
```sql
Select * from EMPLOYEE where joining_date <'01/01/2013'
```
* SQL Queries in MySQL (Format - “YYYY-DD-MM”), 
```sql
Select * from EMPLOYEE where joining_date <'2013-01-01'
```
#### 33. Get employee details from employee table who joined after January 31st
* SQL Queries in Oracle, 
```sql
Select * from EMPLOYEE where JOINING_DATE >to_date('31/01/2013','dd/mm/yyyy')
```
* SQL Queries in SQL Server and MySQL (Format - “MM/DD/YYYY”), 
```sql
Select * from EMPLOYEE where joining_date >'01/31/2013'
```
* SQL Queries in MySQL (Format - “YYYY-DD-MM”), 
```sql
Select * from EMPLOYEE where joining_date >'2013-01-31'
```
#### 35. Get Joining Date and Time from employee table
* SQL Queries in Oracle, 
```sql
select to_char(JOINING_DATE,'dd/mm/yyyy hh:mi:ss') from EMPLOYEE
```
* SQL Queries in SQL Server, 
```sql
Select convert(varchar(19),joining_date,121) from EMPLOYEE
```
* SQL Queries in MySQL, 
```sql
Select CONVERT(DATE_FORMAT(joining_date,'%Y-%m-%d-%H:%i:00'),DATETIME) from EMPLOYEE
```
#### 36. Get Joining Date,Time including milliseconds from employee table
* SQL Queries in Oracle, 
```sql
select to_char(JOINING_DATE,'dd/mm/yyyy HH:mi:ss.ff') from EMPLOYEE . Column Data Type should be “TimeStamp”
```
* SQL Queries in SQL Server, 
```sql
select convert(varchar,joining_date,121) from EMPLOYEE
```
* SQL Queries in MySQL, 
```sql
Select MICROSECOND(joining_date) from EMPLOYEE
```
#### 37. Get difference between JOINING_DATE and INCENTIVE_DATE from employee and incentives table
```sql
Select FIRST_NAME,INCENTIVE_DATE - JOINING_DATE from employee a inner join incentives B on A.EMPLOYEE_ID=B.EMPLOYEE_REF_ID
```
#### 38. Get database date
* SQL Queries in Oracle, 
```sql
select sysdate from dual
```
* SQL Queries in SQL Server, 
```sql
select getdate()
```
* SQL Query in MySQL, 
```sql
select now()
```

<br>
<br>

### "SQL Escape Characters" Interview Questions

<hr>

#### 39. Get names of employees from employee table who has '%' in Last_Name. Tip : Escape character for special characters in a query.

* SQL Queries in Oracle, 
```sql
Select FIRST_NAME from employee where Last_Name like '%?%%'
```
* SQL Queries in SQL Server, 
```sql
Select FIRST_NAME from employee where Last_Name like '%[%]%'
```
* SQL Queries in MySQL, 
```sql
Select FIRST_NAME from employee where Last_Name like '%\%%'
```
#### 40. Get Last Name from employee table after replacing special character with white space
* SQL Queries in Oracle, 
```sql
Select translate(LAST_NAME,'%',' ') from employee
```
* SQL Queries in SQL Server and MySQL, 
```sql
Select REPLACE(LAST_NAME,'%',' ') from employee
```


<br>
<br>

### "SQL Group By Query" Interview Questions and Answers

<hr>

#### 41. Get department,total salary with respect to a department from employee table.
```sql
Select DEPARTMENT,sum(SALARY) Total_Salary from employee group by department
```
#### 42. Get department,total salary with respect to a department from employee table order by total salary descending
```sql
Select DEPARTMENT,sum(SALARY) Total_Salary from employee group by DEPARTMENT order by Total_Salary descending
```


<br>
<br>

### SQL Queries Interview Questions and Answers on "SQL Mathematical Operations using Group By"

<hr>

#### 43. Get department,no of employees in a department,total salary with respect to a department from employee table order by total salary descending
```sql
Select DEPARTMENT,count(FIRST_NAME),sum(SALARY) Total_Salary from employee group by DEPARTMENT order by Total_Salary descending
```
#### 44. Get department wise average salary from employee table order by salary ascending
```sql
select DEPARTMENT,avg(SALARY) AvgSalary from employee group by DEPARTMENT order by AvgSalary asc
```
#### 45. Get department wise maximum salary from employee table order by salary ascending
```sql
select DEPARTMENT,max(SALARY) MaxSalary from employee group by DEPARTMENT order by MaxSalary asc
```
#### 46. Get department wise minimum salary from employee table order by salary ascending
```sql
select DEPARTMENT,min(SALARY) MinSalary from employee group by DEPARTMENT order by MinSalary asc
```
#### 47. Select no of employees joined with respect to year and month from employee table
* SQL Queries in Oracle, 
```sql
select to_char (JOINING_DATE,'YYYY') Join_Year,to_char (JOINING_DATE,'MM') Join_Month,count(*) Total_Emp from employee group by to_char (JOINING_DATE,'YYYY'),to_char(JOINING_DATE,'MM')
```
* SQL Queries in SQL Server, 
```sql
select datepart (YYYY,JOINING_DATE) Join_Year,datepart (MM,JOINING_DATE) Join_Month,count(*) Total_Emp from employee group by datepart(YYYY,JOINING_DATE), datepart(MM,JOINING_DATE)
```
* SQL Queries in MySQL, 
```sql
select year (JOINING_DATE) Join_Year,month (JOINING_DATE) Join_Month,count(*) Total_Emp from employee group by year(JOINING_DATE), month(JOINING_DATE)
```
#### 48. Select department,total salary with respect to a department from employee table where total salary greater than 800000 order by Total_Salary descending
```sql
Select DEPARTMENT,sum(SALARY) Total_Salary from employee group by DEPARTMENT having sum(SALARY) >800000 order by Total_Salary desc
```

<br>
<br>
<br>

### Advanced SQL Queries Interview Questions and Answers

<hr>

#### 49. Select employee details from employee table if data exists in incentive table ?
```sql
select * from EMPLOYEE where exists (select * from INCENTIVES)
```
**Explanation :** Here "exists" statement helps us to do the job of If statement. Main query will get executed if the sub query returns at least one row. So we can consider the sub query as "If condition" and the main query as "code block" inside the If condition. We can use any SQL commands (Joins, Group By , having etc) in sub query. This command will be useful in queries which need to detect an event and do some activity.

#### 50. How to fetch data that are common in two query results ?
```sql
select * from EMPLOYEE where EMPLOYEE_ID INTERSECT select * from EMPLOYEE where EMPLOYEE_ID < 4
```
**Explanation :** Here "INTERSECT" command is used to fetch data that are common in 2 queries. In this example, we had taken EMPLOYEE table in both the queries.We can apply INTERSECT command on different tables. The result of the above query will return employee details of "ROY" because, employee id of ROY is 3, and both query results have the information about ROY.

#### 51. Get Employee ID's of those employees who didn't receive incentives without using sub query ?
```sql
select EMPLOYEE_ID from EMPLOYEE
MINUS
select EMPLOYEE_REF_ID from INCENTIVES
```
**Explanation :** To filter out certain information we use MINUS command. What MINUS Command odes is that, it returns all the results from the first query, that are not part of the second query. In our example, first three employees received the incentives. So query will return employee id's 4 to 8.

#### 52. Select 20 % of salary from John , 10% of Salary for Roy and for other 15 % of salary from employee table
```sql
SELECT FIRST_NAME, CASE FIRST_NAME 
WHEN 'John' 
THEN SALARY * .2 
WHEN 'Roy' 
THEN SALARY * .10 
ELSE 
SALARY * .15 
END "Deduced_Amount" FROM EMPLOYEE
```
**Explanation :** Here, we are using "SQL CASE" statement to achieve the desired results. After case statement, we had to specify the column on which filtering is applied. In our case it is "FIRST_NAME". And in then condition, specify the name of filter like John, Roy etc. To handle conditions outside our filter, use else block where every one other than John and Roy enters.

#### 53. Select Banking as 'Bank Dept', Insurance as 'Insurance Dept' and Services as 'Services Dept' from employee table
* SQL Queries in Oracle, 
```sql
SELECT distinct 
DECODE (DEPARTMENT, 'Banking', 'Bank Dept', 'Insurance', 'Insurance Dept', 'Services', 'Services Dept') 
FROM EMPLOYEE
```
* SQL Queries in SQL Server and MySQL, 
```sql
SELECT case DEPARTMENT 
when 'Banking' 
then 'Bank Dept' 
when 'Insurance' 
then 'Insurance Dept' 
when 'Services' 
then 'Services Dept' 
end FROM EMPLOYEE
```
**Explanation :** Here "DECODE" keyword is used to specify the alias name. In oracle we had specify, Column Name followed by Actual Name and Alias Name as arguments. In SQL Server and MySQL, we can use the earlier switch case statements for alias names.
#### 54. Delete employee data from employee table who got incentives in incentive table
```sql
delete from EMPLOYEE 
where EMPLOYEE_ID in (select EMPLOYEE_REF_ID from INCENTIVES)
```
**Explanation :** Trick about this question is that we can't delete data from a table based on some condition in another table by joining them. Here to delete multiple entries from EMPLOYEE table, we need to use Subquery. Entries will get deleted based on the result of Subquery.
#### 55. Insert into employee table Last Name with " ' " (Single Quote - Special Character)
Tip - Use another single quote before special character
```sql
Insert into employee (LAST_NAME) values ('Test''')
```
#### 56. Select Last Name from employee table which contain only numbers
```sql
Select * from EMPLOYEE where lower(LAST_NAME)=upper(LAST_NAME)
```
**Explanation :** In order to achieve the desired result, we use "ASCII" property of the database. If we get results for a column using Lower and Upper commands, ASCII of both results will be same for numbers. If there is any alphabets in the column, results will differ.
#### 57. Write a query to rank employees based on their incentives for a month
```sql
select FIRST_NAME, INCENTIVE_AMOUNT, 
DENSE_RANK() OVER (PARTITION BY INCENTIVE_DATE ORDER BY INCENTIVE_AMOUNT DESC) AS Rank 
from EMPLOYEE a, INCENTIVES b 
where a.EMPLOYEE_ID=b.EMPLOYEE_REF_ID
```
**Explanation :** In order to rank employees based on their rank for a month, "DENSE_RANK" keyword is used. Here partition by keyword helps us to sort the column with which filtering is done. Rank is provided to the column specified in the order by statement. The above query ranks employees with respect to their incentives for a given month.
#### 58. Update incentive table where employee name is 'John'
```sql
update INCENTIVES set INCENTIVE_AMOUNT='9000' 
where EMPLOYEE_REF_ID = (select EMPLOYEE_ID from EMPLOYEE where FIRST_NAME='John' )
```
**Explanation :** We need to join Employee and Incentive Table for updating the incentive amount. But for update statement joining query wont work. We need to use sub query to update the data in the incentive table. SQL Query is as shown below.


<br>
<br>

### "SQL Join" Interview Questions

<hr>

#### 59. Select first_name, incentive amount from employee and incentives table for those employees who have incentives
```sql
Select FIRST_NAME,INCENTIVE_AMOUNT 
from employee a inner join incentives B on A.EMPLOYEE_ID=B.EMPLOYEE_REF_ID
 ```
#### 60. Select first_name, incentive amount from employee and incentives table for those employees who have incentives and incentive amount greater than 3000
```sql
Select FIRST_NAME,INCENTIVE_AMOUNT 
from employee a inner join incentives B on A.EMPLOYEE_ID = B.EMPLOYEE_REF_ID and INCENTIVE_AMOUNT >3000
```
#### 61. Select first_name, incentive amount from employee and incentives table for all employes even if they didn't get incentives
```sql
Select FIRST_NAME,INCENTIVE_AMOUNT 
from employee a left join incentives B on A.EMPLOYEE_ID = B.EMPLOYEE_REF_ID
```
#### 62. Select first_name, incentive amount from employee and incentives table for all employees even if they didn't get incentives and set incentive amount as 0 for those employees who didn't get incentives.
* SQL Queries in Oracle, 
```sql
Select FIRST_NAME,nvl(INCENTIVE_AMOUNT,0) 
from employee a left join incentives B on A.EMPLOYEE_ID=B.EMPLOYEE_REF_ID
```
* SQL Queries in SQL Server, 
```sql
Select FIRST_NAME, ISNULL(INCENTIVE_AMOUNT,0) 
from employee a left join incentives B on A.EMPLOYEE_ID=B.EMPLOYEE_REF_ID
```
* SQL Queries in MySQL, 
```sql
Select FIRST_NAME, IFNULL(INCENTIVE_AMOUNT,0) 
from employee a left join incentives B on A.EMPLOYEE_ID=B.EMPLOYEE_REF_ID
```
#### 63. Select first_name, incentive amount from employee and incentives table for all employees who got incentives using left join
* SQL Queries in Oracle, 
```sql
Select FIRST_NAME,nvl(INCENTIVE_AMOUNT,0) 
from employee a right join incentives B on A.EMPLOYEE_ID=B.EMPLOYEE_REF_ID
```
* SQL Queries in SQL Server, 
```sql
Select FIRST_NAME, isnull(INCENTIVE_AMOUNT,0) 
from employee a right join incentives B on A.EMPLOYEE_ID=B.EMPLOYEE_REF_ID
```
* SQL Queries in MySQL, 
```sql
Select FIRST_NAME, IFNULL(INCENTIVE_AMOUNT,0) 
from employee a right join incentives B on A.EMPLOYEE_ID=B.EMPLOYEE_REF_ID
```
#### 64. Select max incentive with respect to employee from employee and incentives table using sub query
* SQL Queries in Oracle, 
```sql
select DEPARTMENT,(select nvl(max(INCENTIVE_AMOUNT),0) from INCENTIVES 
where EMPLOYEE_REF_ID=EMPLOYEE_ID) Max_incentive from EMPLOYEE
```
* SQL Queries in SQL Server, 
```sql
select DEPARTMENT,(select ISNULL(max(INCENTIVE_AMOUNT),0) 
from INCENTIVES where EMPLOYEE_REF_ID=EMPLOYEE_ID) Max_incentive from EMPLOYEE
```
* SQL Queries in SQL Server, 
```sql
select DEPARTMENT,(select IFNULL (max(INCENTIVE_AMOUNT),0) 
from INCENTIVES where EMPLOYEE_REF_ID=EMPLOYEE_ID) Max_incentive from EMPLOYEE
``` 

<br>
<br>

### "Top N Salary" SQL Interview Questions and Answers

<hr>

#### 65. Select TOP 2 salary from employee table

* SQL Queries in Oracle, 
```sql
select * from (select * from employee order by SALARY desc) where rownum <3
```
* SQL Queries in SQL Server, 
```sql
select top 2 * from employee order by salary desc
```
* SQL Queries in MySQL, 
```sql
select * from employee order by salary desc limit 2
```
#### 66. Select TOP N salary from employee table
* SQL Queries in Oracle, 
```sql
select * from (select * from employee order by SALARY desc) where rownum <N + 1
```
* SQL Queries in SQL Server, 
```sql
select top N * from employee
```
* SQL Queries in MySQL, 
```sql
select * from employee order by salary desc limit N
```
#### 67. Select 2nd Highest salary from employee table

* SQL Queries in Oracle, 
```sql
select min(salary) from (select * from (select * from employee order by SALARY desc) where rownum <3)
```
* SQL Queries in SQL Server, 
```sql
select min(SALARY) from (select top 2 * from employee) a
```
* SQL Queries in MySQL, 
```sql
select min(SALARY) from (select * from employee order by salary desc limit 2) a
```
#### 68. Select Nth Highest salary from employee table

* SQL Queries in Oracle, 
```sql
select min(salary) from (select * from (select * from employee order by SALARY desc) where rownum <N + 1)
```
* SQL Queries in SQL Server, 
```sql
select min(SALARY) from (select top N * from employee) a
```
* SQL Queries in MySQL, 
```sql
select min(SALARY) from (select * from employee order by salary desc limit N) a
```

<br>
<br>

### "SQL Union" Query Interview Questions

<br>

#### 69. Select First_Name,LAST_NAME from employee table as separate rows
```sql
select FIRST_NAME from EMPLOYEE union select LAST_NAME from EMPLOYEE
```
#### 70. What is the difference between UNION and UNION ALL ?
Both UNION and UNION ALL is used to select information from structurally similar tables. That means corresponding columns specified in the union should have same data type. For example, in the above query, if FIRST_NAME is DOUBLE and LAST_NAME is STRING above query wont work. Since the data type of both the columns are VARCHAR, union is made possible. Difference between UNION and UNION ALL is that , UNION query return only distinct values. 



<br>
<br>

### SQL Interview Questions on "SQL Table Scripts"

<hr>

#### 71. Write create table syntax for employee table
```sql
Oracle -CREATE TABLE EMPLOYEE (
EMPLOYEE_ID NUMBER,
FIRST_NAME VARCHAR2(20 BYTE),
LAST_NAME VARCHAR2(20 BYTE),
SALARY FLOAT(126),
JOINING_DATE TIMESTAMP (6) DEFAULT sysdate,
DEPARTMENT VARCHAR2(30 BYTE) )
SQL Server -CREATE TABLE EMPLOYEE(
EMPLOYEE_ID int NOT NULL,
FIRST_NAME varchar(50) NULL,
LAST_NAME varchar(50) NULL,
SALARY decimal(18, 0) NULL,
JOINING_DATE datetime2(7) default getdate(),
DEPARTMENT varchar(50) NULL)
```

#### 72. Write syntax to delete table employee
```sql
DROP table employee;
```
#### 73. Write syntax to set EMPLOYEE_ID as primary key in employee table
```sql
ALTER TABLE EMPLOYEE add CONSTRAINT EMPLOYEE_PK PRIMARY KEY(EMPLOYEE_ID)
```
#### 74. Write syntax to set 2 fields(EMPLOYEE_ID,FIRST_NAME) as primary key in employee table
```sql
ALTER TABLE EMPLOYEE add CONSTRAINT EMPLOYEE_PK PRIMARY KEY(EMPLOYEE_ID,FIRST_NAME)
```
#### 75. Write syntax to drop primary key on employee table
```sql
Alter TABLE EMPLOYEE drop CONSTRAINT EMPLOYEE_PK;
```
#### 76. Write Sql Syntax to create EMPLOYEE_REF_ID in INCENTIVES table as foreign key with respect to EMPLOYEE_ID in employee table
```sql
ALTER TABLE INCENTIVES ADD CONSTRAINT INCENTIVES_FK FOREIGN KEY (EMPLOYEE_REF_ID) REFERENCES EMPLOYEE(EMPLOYEE_ID)
```
#### 77. Write SQL to drop foreign key on employee table
```sql
ALTER TABLE INCENTIVES drop CONSTRAINT INCENTIVES_FK;
```
#### 78. Write SQL to create Orcale Sequence
```sql
CREATE SEQUENCE EMPLOYEE_ID_SEQ START WITH 0 NOMAXVALUE MINVALUE 0 NOCYCLE NOCACHE NOORDER;
```
#### 79. Write Sql syntax to create Oracle Trigger before insert of each row in employee table
```sql
CREATE OR REPLACE TRIGGER EMPLOYEE_ROW_ID_TRIGGER
BEFORE INSERT ON EMPLOYEE FOR EACH ROW
DECLARE
seq_no number(12);
BEGIN
select EMPLOYEE_ID_SEQ.nextval into seq_no from dual ;
:new EMPLOYEE_ID :=seq_no;
END;
SHOW ERRORS;
```
#### 80. Oracle Procedure81. Oracle View

An example oracle view script is given below
```sql
create view Employee_Incentive as 
select FIRST_NAME,max(INCENTIVE_AMOUNT) INCENTIVE_AMOUNT 
from EMPLOYEE a, INCENTIVES b 
where a.EMPLOYEE_ID=b.EMPLOYEE_REF_ID 
group by FIRST_NAME
```
#### 82. Oracle materialized view - Daily Auto Refresh
```sql
CREATE MATERIALIZED VIEW Employee_Incentive
REFRESH COMPLETE
START WITH SYSDATE
NEXT SYSDATE + 1 AS
select FIRST_NAME,INCENTIVE_DATE,INCENTIVE_AMOUNT from EMPLOYEE a, INCENTIVES b 
where a.EMPLOYEE_ID=b.EMPLOYEE_REF_ID
```
#### 83. Oracle materialized view - Fast Refresh on Commit

Create materialized view log for fast refresh. Following materialized view script wont get executed if materialized view log doesn't exists
```sql
CREATE MATERIALIZED VIEW MAT_Employee_Incentive_Refresh
BUILD IMMEDIATE
REFRESH FAST ON COMMIT AS
select FIRST_NAME,max(INCENTIVE_AMOUNT) from EMPLOYEE a, INCENTIVES b
where a.EMPLOYEE_ID=b.EMPLOYEE_REF_ID group by FIRST_NAME
```
#### 84. What is SQL Injection ?

SQL Injection is one of the the techniques uses by hackers to hack a website by injecting SQL commands in data fields.
