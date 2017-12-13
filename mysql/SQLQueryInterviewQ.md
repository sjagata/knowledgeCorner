
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


